<div align="center">

# Trabalho 10 - Respostas de Manuntenção

## Universidade Federal do Pará (UFPA)

### Instituto de Ciências Exatas e Naturais (ICEN)

#### Bacharelado em Ciência da Computação

| Alunos | Matrículas |
| --- | :-: |
| **Alessandro Reali Lopes Silva** | 202304940049 |
| **Felipe Lisboa Brasil** | 202404940029 |

---

</div>

## Se você fosse chamado para fazer uma Manutenção Corretiva, Manutenção Evolutiva e Manutenção Preventiva em um sistema, relate como cada uma dessas individualmente ocorreria, descrevendo um cenário em que cada uma delas estaria acontecendo

### Manutenção Corretiva

**Como ocorre:** É uma atividade reativa engatilhada pela descoberta de um defeito após a entrega do *software*, cuja execução visa restaurar o comportamento esperado do sistema mapeado nos requisitos originais.

**Cenário Prático:** No módulo de contratos do *SIGESCON*, quando dois gestores tentam confirmar o cadastro de documentos simultaneamente, ocorre uma falha de concorrência que resulta em um erro de persistência no *PostgreSQL*, abortando a transação. O mantenedor é acionado para aplicar uma correção na camada do backend em *FastAPI* para tratar o bloqueio de tabelas.

### Manutenção Evolutiva

**Como ocorre:** Ocorre a partir de solicitações dos *stakeholders* ou usuários master para alterar o escopo do produto, seja modificando regras existentes ou adicionando novos fluxos operacionais para gerar valor de negócio.

**Cenário Prático:** O setor competente da Procuradoria solicita que o sistema passe a permitir o gerenciamento e uso de modelos/*templates* de contratos pré-aprovados diretamente no sistema. Como essa capacidade não fazia parte do escopo original, o desenvolvedor altera a estrutura de classes e adiciona novos *endpoints* na *API* para acomodar a funcionalidade evolutiva.

### Manutenção Preventiva

**Como ocorre:** É uma atividade proativa com foco em melhorar a manutenibilidade, segurança e confiabilidade futuras do sistema antes que falhas se manifestem, mitigando custos de oportunidade de longo prazo.

**Cenário Prático:** Sem que nenhum erro tenha sido relatado pelos administradores, a equipe de TI decide atualizar a imagem base do *Docker* do *Ubuntu Server* e refatorar as consultas do *PostgreSQL* no *backend* para otimizar o tempo de resposta das requisições de relatórios consolidados por área, prevenindo gargalos futuros à medida que o volume de dados cresce.

## Relate de maneira prática, mostrando a partir de exemplos, a diferença entre Engenharia Reversa e Reengenharia

### Engenharia Reversa

A Engenharia Reversa é um processo estritamente analítico que realiza o caminho inverso do ciclo de vida tradicional: parte da implementação física (código-fonte bruto) em direção a níveis mais altos de abstração. O seu propósito fundamental é puramente **compreensiva e bibliográfica**: redocumentar o sistema e entender seus relacionamentos internos, **sem realizar qualquer alteração ou modificação no código atual**.

**Exemplo Prático:** Uma instituição possui um sistema de análise de dívidas antigo, cujo código-fonte está em *scripts* *PHP* monolíticos sem qualquer documentação, diagramas UML ou engenheiros originais presentes. Um analista é encarregado de ler as linhas de código e, a partir delas, reconstruir o diagrama de entidades e o documento de requisitos do sistema para decifrar as regras de negócio ocultas.

### Reengenharia

A Reengenharia é uma intervenção profunda e reconstrutiva. Ela envolve o exame cuidadoso do *software* existente (frequentemente utilizando a engenharia reversa como etapa inicial) seguido pela **efetiva modificação e reescrita do sistema em uma nova forma**. O objetivo central é rejuvenescer o *software*, atualizando sua tecnologia, estendendo sua expectativa de vida e eliminando problemas técnicos de desempenho crônicos.

**Exemplo Prático:** A diretoria decide extinguir o sistema *PHP* antigo devido a frequentes falhas de produção e problemas técnicos de integração de sistemas. A equipe de engenharia pega a documentação extraída pela engenharia reversa e reconstrói completamente o *software* do zero, migrando a arquitetura para microsserviços modernos rodando em containers *Docker* com *backend* em *FastAPI* e persistência em *PostgreSQL*, eliminando os gargalos de manutenção anteriores.
