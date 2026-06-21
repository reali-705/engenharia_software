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

A partir os requisitos listados e especificados na [Prática 5](https://docs.google.com/document/d/1GsnwbizGQO-j8Atvnh9J6qYrmessHYBtOcvFYvkxhY4/edit?tab=t.0), gere 5 Casos de Teste para as Funcionalidades, contendo:

- Título do Caso de Teste
- Objetivo
- Pré-Condição
- Dados de Entrada
- Ações do Passo (Cenários)
- Resultados Esperados

## 1. Validar cadastro de contrato público

### 1.1. Objetivo

Verificar se o sistema realiza o cadastro de um novo contrato público após o preenchimento correto de todas as informações obrigatórias.

### 1.2. Pré-Condição

Usuário autenticado com o perfil de Gestor de Contratos e banco de dados operacional.

### 1.3. Dados de Entrada

```Json
{
  "Número do Processo": "PGE-PA-2026/04",
  "Data de Assinatura": "21/06/2026",
  "Descrição do Objeto": "Prestação de serviços de manutenção de rede interna.",
  "Fiscal Responsável": "Felipe Brasil"
}
```

### 1.4. Ações do Passo (Cenários)

1. Acessar o módulo de contratos e clicar no botão `ADICIONAR CONTRATO`.
2. Preencher os campos obrigatórios com os dados de entrada fornecidos.
3. Clicar no botão `CONFIRMAR`.

### 1.5. Resultados Esperados

1. Sistema executa a validação dos campos sem apontar inconsistências.
2. O registro é persistido com sucesso no banco de dados.
3. Sistema apresenta a mensagem de confirmação: "Contrato cadastrado com sucesso!".

## 2. Validar upload de arquivo com extensão inválida

### 2.1. Objetivo

Verificar se o sistema impede o upload de documentos que não estejam nos formatos permitidos (`.pdf` ou `.docx`).

### 2.2. Pré-Condição

Usuário autenticado no sistema posicionado na interface de upload de arquivos.

### 2.3. Dados de Entrada

`Arquivo = "planilha_custos_pge.xlsx"` (Extensão inválida)

### 2.4. Ações do Passo

1. Clicar na zona de seleção de arquivos ou no botão de upload.
2. Selecionar o arquivo contendo a extensão inválida `.xlsx` a partir do dispositivo local.

### 2.5. Resultados Esperados

1. Sistema intercepta a transferência do arquivo durante a validação de formato.
2. Sistema exibe a mensagem de erro na interface:  
  `Formato de arquivo inválido. Apenas PDF e DOCX são aceitos.`
3. A área temporária do servidor permanece limpa e sem resíduos do arquivo rejeitado.

## 3. Validar exibição de alerta visual de contrato a vencer

### 3.1. Objetivo

Verificar se o sistema calcula o tempo restante de vigência e renderiza o alerta visual na cor amarela para contratos que vencem em até 30 dias.

### 3.2. Pré-Condição

Existência de um contrato previamente salvo cuja data de término seja exatamente daqui a 15 dias em relação à data atual do servidor.

### 3.3. Dados de Entrada

- `Data Atual = "21/06/2026"`
- `Data de Vencimento do Contrato Alvo = "06/07/2026"` (Intervalo de 15 dias)

### 3.4. Ações do Passo

1. Acessar o menu `Contratos` e selecionar a opção `Gestão de Prazos`.
2. Localizar o contrato alvo na listagem de prazos apresentada.

### 3.5. Resultados Esperados

1. Sistema realiza a consulta e calcula o tempo de vigência restante com precisão.
2. O status do registro atualiza para `A Vencer`.
3. A interface exibe o card do contrato destacado com um alerta visual na cor amarela.

## 4. Validar falha ao delegar contrato para usuário sem permissão

### 4.1. Objetivo

Verificar se o mecanismo de proteção bloqueia a delegação temporária de responsabilidade para usuários que não possuem perfil de gerência homologado.

### 4.2. Pré-Condição

Usuário delegante autenticado com permissão de escrita e existência de um usuário na base sem as credenciais necessárias de gestão.

### 4.3. Dados de Entrada

```Json
{
  "Contrato Selecionado": "PGE-PA-2026/04",
  "Usuário Destinatário": "João Silva (Perfil: Consulta Geral)",
  "Motivo": "Afastamento médico do titular por 5 dias."
}
```

### 4.4. Ações do Passo

1. Selecionar o contrato na listagem e clicar na opção `DELEGAR RESPONSABILIDADE`.
2. Preencher o campo de usuário com o nome do funcionário sem permissão.
3. Inserir as datas, preencher a justificativa obrigatória e clicar em `CONFIRMAR DELEGAÇÃO`.

### 4.5. Resultados Esperados

1. Sistema interrompe a operação durante a validação de regras de negócio.
2. O banco de dados aborta a geração do evento de auditoria para evitar inconsistências.
3. A interface apresenta o alerta de bloqueio:  
  `O usuário selecionado não possui permissão para gerenciar contratos. Selecione um usuário com as permissões necessárias.`

## 5. Validar assinatura eletrônica de contrato

### 5.1. Objetivo

Verificar se o sistema processa a assinatura digital de um documento e altera o status do contrato para `Assinado/Vigente` após a confirmação do signatário.

### 5.2. Pré-Condição

Contrato com o arquivo PDF gerado posicionado com o status estático de `Aguardando Assinatura`.

### 5.3. Dados de Entrada

```Json
{
  "ID do Contrato": "UUID-CONTRATO-0987",
  "Perfil Signatário": "Alessandro Silva"
}
```

### 5.4. Ações do Passo

1. Acessar a tela de detalhes do contrato com pendência de assinatura.
2. Selecionar a opção de assinatura eletrônica do documento.
3. Confirmar as credenciais de assinatura na interface integrada.

### 5.5. Resultados Esperados

1. A API externa de autenticação de assinaturas valida o token e retorna sucesso.
2. O status do contrato muda imediatamente para `Assinado/Vigente` na base de dados.
3. O sistema persiste a versão final criptografada do documento no repositório definitivo.
