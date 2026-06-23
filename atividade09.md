<div align="center">

# Trabalho 09 - Casos de Teste para Funcionalidades

## Universidade Federal do Pará (UFPA)

### Instituto de Ciências Exatas e Naturais (ICEN)

#### Bacharelado em Ciência da Computação

| Alunos | Matrículas |
| --- | :-: |
| **Alessandro Reali Lopes Silva** | 202304940049 |
| **Felipe Lisboa Brasil** | 202404940029 |

---

</div>

## Instruções

A partir dos requisitos listados e especificados na [Prática 5](https://docs.google.com/document/d/1GsnwbizGQO-j8Atvnh9J6qYrmessHYBtOcvFYvkxhY4/edit?tab=t.0), gere 5 Casos de Teste para as Funcionalidades, contendo:

- Título do Caso de Teste
- Objetivo
- Pré-Condição
- Dados de Entrada
- Ações do Passo (Cenários)
- Resultados Esperados

---

## 1. Validar cadastro de contrato público

### 1.1. Pré-Condição

1. Usuário autenticado com o perfil de Gestor de Contratos;
2. Banco de dados operacional e com conectividade disponível;
3. Gestor dispõe dos dados do contrato a ser cadastrado.

---

#### Subteste 1.1 — Cadastro com dados válidos

##### Objetivo

Verificar se o sistema realiza o cadastro de um novo contrato público após o preenchimento correto de todas as informações obrigatórias.

##### Dados de Entrada

```json
{
  "Número do Processo": "PGE-PA-2026/04",
  "Data de Assinatura": "21/06/2026",
  "Descrição do Objeto": "Prestação de serviços de manutenção de rede interna.",
  "Fiscal Responsável": "Felipe Brasil"
}
```

##### Ações do Passo

1. Acessar o módulo de contratos e clicar no botão `ADICIONAR CONTRATO`.
2. Preencher os campos obrigatórios com os dados de entrada fornecidos.
3. Clicar no botão `CONFIRMAR`.

##### Resultados Esperados

1. Sistema executa a validação dos campos sem apontar inconsistências.
2. O registro é persistido com sucesso no banco de dados.
3. Sistema apresenta a mensagem de confirmação: `Contrato cadastrado com sucesso!`

---

#### Subteste 1.2 — Cadastro com campos obrigatórios ausentes

##### Objetivo

Verificar se o sistema bloqueia o cadastro e exibe mensagem de erro quando campos obrigatórios não são preenchidos.

##### Dados de Entrada

```json
{
  "Número do Processo": "PGE-PA-2026/05",
  "Data de Assinatura": "",
  "Descrição do Objeto": "",
  "Fiscal Responsável": "Felipe Brasil"
}
```

##### Ações do Passo

1. Acessar o módulo de contratos e clicar no botão `ADICIONAR CONTRATO`.
2. Preencher apenas os campos `Número do Processo` e `Fiscal Responsável`, deixando os demais em branco.
3. Clicar no botão `CONFIRMAR`.

##### Resultados Esperados

1. Sistema identifica os campos obrigatórios ausentes durante a validação.
2. Nenhum registro é persistido no banco de dados.
3. Sistema exibe a mensagem de erro: `Erro interno: Campo [Data de Assinatura] é obrigatório. Por favor, preencha corretamente todos os campos obrigatórios.`
4. Sistema mantém o gestor na página de preenchimento com os dados já digitados preservados.

---

#### Subteste 1.3 — Falha de persistência no banco de dados

##### Objetivo

Verificar se o sistema cancela a transação e exibe mensagem de erro adequada quando ocorre uma falha interna no banco de dados durante o salvamento.

##### Dados de Entrada

```json
{
  "Número do Processo": "PGE-PA-2026/06",
  "Data de Assinatura": "21/06/2026",
  "Descrição do Objeto": "Aquisição de equipamentos de informática.",
  "Fiscal Responsável": "Alessandro Silva"
}
```

##### Ações do Passo

1. Acessar o módulo de contratos e clicar no botão `ADICIONAR CONTRATO`.
2. Preencher todos os campos obrigatórios corretamente com os dados de entrada.
3. Clicar no botão `CONFIRMAR` com o banco de dados simulando falha no INSERT.

##### Resultados Esperados

1. Sistema executa a validação dos campos sem identificar inconsistências.
2. O banco de dados aborta a operação de inserção e não persiste os dados.
3. Sistema cancela a transação para evitar dados corrompidos.
4. Sistema exibe a mensagem de erro: `Erro interno: Não foi possível salvar o contrato. Por favor, tente novamente mais tarde ou contate o suporte.`
5. Sistema mantém o gestor na página de preenchimento com os dados já digitados preservados.

---

## 2. Validar upload de arquivo

### 2.1. Pré-Condição

1. Usuário autenticado no sistema com permissão de escrita;
2. Sistema de armazenamento operacional e com conectividade disponível;
3. Usuário posicionado na interface de upload de arquivos.

---

#### Subteste 2.1 — Upload com extensão inválida

##### Objetivo

Verificar se o sistema impede o upload de documentos que não estejam nos formatos permitidos (`.pdf` ou `.docx`).

##### Dados de Entrada

`Arquivo = "planilha_custos_pge.xlsx"` (extensão inválida)

##### Ações do Passo

1. Clicar na zona de seleção de arquivos ou no botão de upload.
2. Selecionar o arquivo `planilha_custos_pge.xlsx` a partir do dispositivo local.

##### Resultados Esperados

1. Sistema intercepta o arquivo durante a validação de formato.
2. Sistema exibe a mensagem de erro: `Formato de arquivo inválido. Apenas PDF e DOCX são aceitos.`
3. A área temporária do servidor permanece limpa e sem resíduos do arquivo rejeitado.

---

#### Subteste 2.2 — Upload com tamanho acima do limite permitido

##### Objetivo

Verificar se o sistema rejeita arquivos que ultrapassem o limite máximo de 5 MB, exibindo o tamanho real do arquivo na mensagem de erro.

##### Dados de Entrada

`Arquivo = "contrato_digitalizado_alta_resolucao.pdf"` — tamanho: `8,4 MB`

##### Ações do Passo

1. Clicar na zona de seleção de arquivos ou no botão de upload.
2. Selecionar o arquivo `.pdf` com 8,4 MB a partir do dispositivo local.

##### Resultados Esperados

1. Sistema valida a extensão com sucesso e em seguida verifica o tamanho do arquivo.
2. Sistema identifica que o arquivo excede o limite de 5 MB.
3. Sistema exibe a mensagem de erro: `Arquivo muito grande. O tamanho máximo permitido é 5MB. Seu arquivo possui 8,4MB.`
4. Nenhum dado é transferido para a área temporária do servidor.

---

#### Subteste 2.3 — Upload com arquivo válido

##### Objetivo

Verificar se o sistema realiza com sucesso o upload de um arquivo válido, persistindo o documento no repositório e vinculando-o ao registro da tela atual.

##### Dados de Entrada

`Arquivo = "minuta_contrato_servicos.pdf"` — tamanho: `2,1 MB`

##### Ações do Passo

1. Clicar na zona de seleção de arquivos ou no botão de upload.
2. Selecionar o arquivo `minuta_contrato_servicos.pdf` de 2,1 MB.
3. Aguardar a exibição do nome e tamanho do arquivo na tela para revisão.
4. Clicar em `CONFIRMAR`.

##### Resultados Esperados

1. Sistema valida extensão e tamanho com sucesso e exibe barra de progresso durante a transferência.
2. Sistema exibe o nome e tamanho do arquivo na tela para revisão.
3. Sistema move o arquivo para o repositório definitivo, gera UUID e registra os metadados no banco de dados.
4. Sistema limpa a área temporária do servidor e exibe: `Documento salvo e vinculado com sucesso!`

---

## 3. Validar exibição de alerta visual de contrato a vencer

### 3.1. Pré-Condição

1. Usuário autenticado com perfil de leitura de contratos;
2. Contratos previamente cadastrados com datas de vigência preenchidas;
3. Usuário posicionado na tela de Gestão de Prazos.

---

#### Subteste 3.1 — Alerta amarelo para contrato a vencer em até 30 dias

##### Objetivo

Verificar se o sistema calcula o tempo restante de vigência e renderiza o alerta visual na cor amarela para contratos que vencem em até 30 dias.

##### Dados de Entrada

- `Data Atual = "21/06/2026"`
- `Data de Vencimento do Contrato Alvo = "06/07/2026"` (intervalo de 15 dias)

##### Ações do Passo

1. Acessar o menu `Contratos` e selecionar a opção `Gestão de Prazos`.
2. Localizar o contrato alvo na listagem de prazos apresentada.

##### Resultados Esperados

1. Sistema realiza a consulta e calcula o tempo de vigência restante com precisão.
2. O status do registro atualiza para `A Vencer`.
3. A interface exibe o card do contrato com alerta visual na cor **amarela**.

---

#### Subteste 3.2 — Alerta vermelho para contrato vencido

##### Objetivo

Verificar se o sistema identifica contratos com data de término ultrapassada e renderiza o alerta visual na cor vermelha.

##### Dados de Entrada

- `Data Atual = "21/06/2026"`
- `Data de Vencimento do Contrato Alvo = "10/06/2026"` (11 dias no passado)

##### Ações do Passo

1. Acessar o menu `Contratos` e selecionar a opção `Gestão de Prazos`.
2. Localizar o contrato alvo na listagem de prazos apresentada.

##### Resultados Esperados

1. Sistema calcula que a data de vencimento já foi ultrapassada.
2. O status do registro atualiza para `Vencido`.
3. A interface exibe o card do contrato com alerta visual na cor **vermelha**.

---

#### Subteste 3.3 — Aviso para contrato sem datas de vigência cadastradas

##### Objetivo

Verificar se o sistema exibe mensagem de aviso adequada quando um contrato selecionado não possui datas de vigência cadastradas, sem gerar erro crítico na interface.

##### Dados de Entrada

- `Contrato = "PGE-PA-2026/09"` (sem datas de vigência preenchidas)

##### Ações do Passo

1. Acessar o menu `Contratos` e selecionar a opção `Gestão de Prazos`.
2. Localizar e selecionar o contrato `PGE-PA-2026/09` na listagem.

##### Resultados Esperados

1. Sistema detecta a ausência de datas de vigência para o contrato selecionado.
2. Sistema não exibe status de prazo nem alerta colorido.
3. Sistema exibe a mensagem de aviso: `As datas de vigência deste contrato não foram preenchidas. Contate o gestor responsável para completar os dados.`
4. Sistema oferece link direto para edição do contrato.

---

## 4. Validar delegação de contrato

### 4.1. Pré-Condição

1. Usuário delegante autenticado com permissão de escrita no módulo de contratos;
2. Contrato selecionado em status ativo ou vigente;
3. Usuário destinatário existente na base de dados do sistema.

---

#### Subteste 4.1 — Delegação para usuário sem permissão de gerência

##### Objetivo

Verificar se o mecanismo de proteção bloqueia a delegação temporária de responsabilidade para usuários que não possuem perfil de gerência homologado.

##### Dados de Entrada

```json
{
  "Contrato Selecionado": "PGE-PA-2026/04",
  "Usuário Destinatário": "João Silva (Perfil: Consulta Geral)",
  "Motivo": "Afastamento médico do titular por 5 dias."
}
```

##### Ações do Passo

1. Selecionar o contrato na listagem e clicar na opção `DELEGAR RESPONSABILIDADE`.
2. Preencher o campo de usuário com o nome do funcionário sem permissão.
3. Inserir as datas, preencher a justificativa obrigatória e clicar em `CONFIRMAR DELEGAÇÃO`.

##### Resultados Esperados

1. Sistema interrompe a operação durante a validação de regras de negócio.
2. O banco de dados não registra nenhum evento de delegação.
3. A interface apresenta o alerta de bloqueio: `O usuário selecionado não possui permissão para gerenciar contratos. Selecione um usuário com as permissões necessárias.`

---

#### Subteste 4.2 — Delegação com data de término anterior à data de início

##### Objetivo

Verificar se o sistema rejeita a delegação quando a data de término informada é anterior à data de início do período delegado.

##### Dados de Entrada

```json
{
  "Contrato Selecionado": "PGE-PA-2026/04",
  "Usuário Destinatário": "Maria Souza (Perfil: Gestor de Contratos)",
  "Data Início da Delegação": "30/06/2026",
  "Data Término da Delegação": "20/06/2026",
  "Motivo": "Férias do titular."
}
```

##### Ações do Passo

1. Selecionar o contrato na listagem e clicar na opção `DELEGAR RESPONSABILIDADE`.
2. Selecionar `Maria Souza` como destinatária.
3. Preencher `Data Início = 30/06/2026` e `Data Término = 20/06/2026`.
4. Preencher o motivo e clicar em `CONFIRMAR DELEGAÇÃO`.

##### Resultados Esperados

1. Sistema detecta inconsistência no intervalo de datas durante a validação.
2. Nenhuma delegação é registrada no banco de dados.
3. Sistema exibe a mensagem de erro: `A data de término deve ser posterior à data de início.`

---

#### Subteste 4.3 — Delegação com período superior a 365 dias

##### Objetivo

Verificar se o sistema recusa a criação de delegação cujo período ultrapassa o limite máximo de 365 dias.

##### Dados de Entrada

```json
{
  "Contrato Selecionado": "PGE-PA-2026/04",
  "Usuário Destinatário": "Carlos Mendes (Perfil: Gestor de Contratos)",
  "Data Início da Delegação": "21/06/2026",
  "Data Término da Delegação": "22/06/2027",
  "Motivo": "Transferência temporária para outra unidade."
}
```

##### Ações do Passo

1. Selecionar o contrato na listagem e clicar na opção `DELEGAR RESPONSABILIDADE`.
2. Selecionar `Carlos Mendes` como destinatário.
3. Preencher `Data Início = 21/06/2026` e `Data Término = 22/06/2027` (366 dias).
4. Preencher o motivo e clicar em `CONFIRMAR DELEGAÇÃO`.

##### Resultados Esperados

1. Sistema calcula a duração do período e identifica que ultrapassa 365 dias.
2. Nenhuma delegação é registrada no banco de dados.
3. Sistema exibe o aviso: `O período de delegação não pode ultrapassar 365 dias. Reduza o período e tente novamente.`

---

## 5. Validar assinatura eletrônica de contrato

### 5.1. Pré-Condição

1. Contrato com arquivo PDF gerado e status `Aguardando Assinatura`;
2. API de integração com a provedora de assinaturas eletrônicas ativa e respondendo;
3. Usuário autenticado e designado como signatário do contrato.

---

#### Subteste 5.1 — Assinatura eletrônica com sucesso

##### Objetivo

Verificar se o sistema processa a assinatura digital de um documento e altera o status do contrato para `Assinado/Vigente` após a confirmação do signatário.

##### Dados de Entrada

```json
{
  "ID do Contrato": "UUID-CONTRATO-0987",
  "Perfil Signatário": "Alessandro Silva"
}
```

##### Ações do Passo

1. Acessar a tela de detalhes do contrato com pendência de assinatura.
2. Selecionar a opção de assinatura eletrônica do documento.
3. Confirmar as credenciais de assinatura na interface integrada.

##### Resultados Esperados

1. A API externa de autenticação de assinaturas valida o token e retorna sucesso.
2. O status do contrato muda imediatamente para `Assinado/Vigente` na base de dados.
3. O sistema persiste a versão final criptografada do documento no repositório definitivo.

---

#### Subteste 5.2 — Falha de assinatura por indisponibilidade da API externa

##### Objetivo

Verificar se o sistema exibe mensagem de erro adequada quando a API externa de assinaturas não responde (timeout), sem alterar o status do contrato.

##### Dados de Entrada

```json
{
  "ID do Contrato": "UUID-CONTRATO-0987",
  "Perfil Signatário": "Alessandro Silva"
}
```

##### Ações do Passo

1. Acessar a tela de detalhes do contrato com pendência de assinatura com a API externa simulando timeout.
2. Selecionar a opção de assinatura eletrônica do documento.
3. Confirmar as credenciais de assinatura na interface integrada.

##### Resultados Esperados

1. A API externa não responde dentro do tempo limite estabelecido.
2. Sistema interrompe a operação sem alterar o status do contrato.
3. O contrato permanece com status `Aguardando Assinatura` na base de dados.
4. Sistema exibe a mensagem de erro: `Não foi possível concluir a assinatura. O serviço de assinatura não está disponível no momento. Tente novamente mais tarde.`

---

#### Subteste 5.3 — Tentativa de assinatura por usuário não designado como signatário

##### Objetivo

Verificar se o sistema impede a assinatura quando o usuário autenticado não está designado como signatário do contrato.

##### Dados de Entrada

```json
{
  "ID do Contrato": "UUID-CONTRATO-0987",
  "Perfil Signatário": "Carlos Mendes (não designado para este contrato)"
}
```

##### Ações do Passo

1. Acessar a tela de detalhes do contrato `UUID-CONTRATO-0987` autenticado como `Carlos Mendes`.
2. Tentar selecionar a opção de assinatura eletrônica do documento.

##### Resultados Esperados

1. Sistema verifica que o usuário autenticado não consta na lista de signatários designados para o contrato.
2. Sistema bloqueia a ação antes de acionar a API externa.
3. Sistema exibe a mensagem de erro: `Você não está autorizado a assinar este contrato. Apenas os signatários designados podem realizar esta ação.`
