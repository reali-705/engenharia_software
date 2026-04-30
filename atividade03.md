<div align="center">

# Atividade 2 - Criação de Modelo de Ciclo de Vida

## Universidade Federal do Pará (UFPA)

### Instituto de Ciências Exatas e Naturais (ICEN)

#### Bacharelado em Ciência da Computação

| Alunos | Matrículas |
| --- | :-: |
| **Alessandro Reali Lopes Silva** | 202304940049 |
| **Felipe Lisboa Brasil** | 202404940029 |

---

</div>

## Detalhes da Atividade 03

### Questão 1: Defina claramente o escopo de um sistema desejado, a ser desenvolvido, descrevendo

1. Problema (Problema, Afetado, Impacto, Solução),
2. Justificativa,
3. Objetivo,
4. O que não faz parte do escopo.

### Questão 2: Classifique os requisitos a seguir para um sistema de venda de ingressos de cinema

1. O sistema deve solicitar tanto ao  gerente quanto ao cliente em qual filial deseja se conectar, no caso do gerente podendo ter acesso à versão restrita.
2. O sistema deve ter uma interface leve (abrir em no máximo 4 segundos e com pouca animação/imagens).
3. Deve disponibilizar informações de horários, salas e sinopses dos filmes em cartaz e os que estrearão na semana seguinte.
4. Deve conter um sistema de cadastros de usuários. Somente usuários cadastrados podem comprar ingressos.

## Resolução da Questão 1

Ideia incial de um sistema de controle administrativo para uma empresa de médio porte, focado na gestão de pessoal e contratos.

### Definição do Problema

- **Problema:** Descentralização de dados e processos administrativos, onde informações de contratos, processos e pessoal residem em planilhas ou sistemas isolados.
- **Afetado:** Gestores de RH, administradores de contratos e a diretoria operacional.
- **Impacto:** Morosidade na geração de relatórios estratégicos, risco de perda de prazos contratuais e falta de visibilidade sobre a produtividade e status de pessoal.
- **Solução:** Uma plataforma centralizada de gestão que integre o ciclo de vida do funcionário, o monitoramento de contratos vigentes e a automação de processos administrativos internos.

### Justificativa

A fragmentação da informação gera um custo de oportunidade elevado, pois o tempo gasto na consolidação manual de dados impede a análise estratégica. A centralização em uma plataforma única reduz a redundância de dados e mitiga erros humanos em processos críticos como gestão de contratos e pessoal.

### Objetivo

Prover uma ferramenta robusta para o controle administrativo que permita o acompanhamento em tempo real de *status* de funcionários, visualização de fluxos de processos e geração automática de relatórios de desempenho e conformidade contratual.

### O que não faz parte do escopo (Não-Escopo)

Para evitar o **perfeccionismo disfuncional** e garantir a entrega do **núcleo administrativo**, os seguintes itens estão fora do escopo:

- Processamento direto de folha de pagamento (integração financeira externa).
- Módulo de contabilidade fiscal ou tributária.
- Comunicação interna via chat/mensageria.

## Resolução da Questão 2

A classificação segue a distinção entre Requisitos Funcionais (RF) — o que o sistema faz — e Requisitos Não-Funcionais (RNF) — como o sistema deve operar ou restrições impostas.

### O sistema deve solicitar tanto ao  gerente quanto ao cliente em qual filial deseja se conectar, no caso do gerente podendo ter acesso à versão restrita

- "O sistema deve solicitar tanto ao  gerente quanto ao cliente em qual filial deseja se conectar..."
  - **Requisito Funcional (RF)**: Define uma funcionalidade específica do sistema relacionada à autenticação e acesso.
- "...no caso do gerente podendo ter acesso à versão restrita."
  - **Requisito Não Funcional (RNF)**: Especifica uma funcionalidade adicional relacionada ao controle de acesso baseado em perfil.

### O sistema deve ter uma interface leve (abrir em no máximo 4 segundos e com pouca animação/imagens)

- **Classificação Geral:**
  - **Requisito Não Funcional (RNF)**: Define uma restrição de desempenho e usabilidade, focando na eficiência da interface.

### Deve disponibilizar informações de horários, salas e sinopses dos filmes em cartaz e os que estrearão na semana seguinte

- **Classificação Geral:**
  - **Requisito Funcional (RF)**: Especifica uma funcionalidade clara do sistema relacionada à exibição de informações sobre os filmes.

### Deve conter um sistema de cadastros de usuários. Somente usuários cadastrados podem comprar ingressos

- "Deve conter um sistema de cadastros de usuários..."
  - **Requisito Funcional (RF)**: Define uma funcionalidade essencial para o gerenciamento de usuários.
- "...Somente usuários cadastrados podem comprar ingressos."
  - **Requisito Funcional (RF)**: Especifica uma regra de negócio relacionada à funcionalidade de compra de ingressos.
