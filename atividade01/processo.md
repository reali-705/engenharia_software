# Especificação do Processo de Desenvolvimento - Startup Acadêmica

Este documento detalha o processo de engenharia de software para o desenvolvimento do sistema de gerenciamento acadêmico mobile, focando em **redução de danos** e **otimização de custos de oportunidade**.

## 1. Diagrama de Processo (Visão Geral)

```mermaid
graph LR
  %% --- Classes Personalizadas ---
  classDef atividade fill:#ef5350,stroke:#212121,stroke-width:2px,font-size:14px,font-weight:bold,color:#111111;
  classDef condicao fill:#ffeb3b,stroke:#f57f17,stroke-width:2px,font-size:12px,color:#111111;
  classDef rh fill:#e0f7fa,stroke:#006064,stroke-width:2px,font-size:11px,color:#111111;
  classDef rnh fill:#f5f5f5,stroke:#616161,stroke-width:2px,font-size:11px,color:#111111;
  classDef artSaida fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px,font-size:11px,color:#111111;
  classDef artEntrada fill:#ffccbc,stroke:#d84315,stroke-width:2px,font-size:11px,color:#111111;
  classDef procedimento fill:#bbdefb,stroke:#0d47a1,stroke-width:2px,font-size:11px,stroke-dasharray:5 5,color:#111111;

  %% --- Fluxo Principal ---
  subgraph Processo de Desenvolvimento 1
    direction LR
    Inicio(( )) ==>
    Atv1([Levantar<br/>requisitos]) ==>
    Atv2([Desenvolver<br/>protótipo<br/>não funcional]) ==>
    Atv3([Reunir com<br/>o cliente]) ==>
    Cond1{Protótipo<br/>aceito?} ==>|Sim| Atv4
    Cond1 ==>|Não| Atv1
  end

  subgraph Processo de Desenvolvimento 2
    direction TB
    Atv4([Definir<br/>ferramentas]) ==>
    Atv5([Definir<br/>modelagem]) ==>
    Atv6([Implementar<br/>funções básicas]) ==>
    Atv7([Testar<br/>funções básicas]) ==>
    Atv8([Implementar<br/>funções gerais]) ==>
    Atv9([Testar<br/>funções gerais]) ==>
    Cond2{Falhas nos<br/>testes?} ==>|Sim| Atv5
    Cond2 ==>|Não| Atv10
  end

  subgraph Processo de Desenvolvimento 3
    direction RL
    Atv10([Apresentar<br/>ao cliente]) ==>
    Cond3{Aprovado?} ==>|Sim| Atv12
    Cond3 ==>|Não| Atv11
    Atv11([Analisar<br/>Falhas]) ==>
    Cond4{Falha<br/>críticas?} ==>|Sim| Atv1
    Cond4 ==>|Não| Atv5
    Atv12([Inicar<br/>deploy]) ==>
    Atv13([Manter<br/>manuntenção]) ==>
    Fim((( )))
  end

  subgraph D1[Descrição 1]
    direction LR
    RH1([Recurso Humano 1]) 
    RNH1([Recurso Não Humano 1]) 
    ArtE1{{Artefato de Entrada 1}} 
    ArtS1{{Artefato de Saída 1}} 
    Proc1[Procedimento 1] 
  end

  subgraph D2[Descrição 2]
    direction LR
    RH2([Recurso Humano 2]) 
    RNH2([Recurso Não Humano 2]) 
    ArtE2{{Artefato de Entrada 2}} 
    ArtS2{{Artefato de Saída 2}} 
    Proc2[Procedimento 2] 
  end

  subgraph D3[Descrição 3]
    direction LR
    RH3([Recurso Humano 3]) 
    RNH3([Recurso Não Humano 3]) 
    ArtE3{{Artefato de Entrada 3}} 
    ArtS3{{Artefato de Saída 3}} 
    Proc3[Procedimento 3] 
  end

  subgraph D4[Descrição 4]
    direction LR
    RH4([Recurso Humano 4]) 
    RNH4([Recurso Não Humano 4]) 
    ArtE4{{Artefato de Entrada 4}} 
    ArtS4{{Artefato de Saída 4}} 
    Proc4[Procedimento 4] 
  end

  subgraph D5[Descrição 5]
    direction LR
    RH5([Recurso Humano 5]) 
    RNH5([Recurso Não Humano 5]) 
    ArtE5{{Artefato de Entrada 5}} 
    ArtS5{{Artefato de Saída 5}} 
    Proc5[Procedimento 5] 
  end
  subgraph D6[Descrição 6]
    direction LR
    RH6([Recurso Humano 6]) 
    RNH6([Recurso Não Humano 6]) 
    ArtE6{{Artefato de Entrada 6}} 
    ArtS6{{Artefato de Saída 6}} 
    Proc6[Procedimento 6] 
  end

  subgraph D7[Descrição 7]
    direction LR
    RH7([Recurso Humano 7]) 
    RNH7([Recurso Não Humano 7]) 
    ArtE7{{Artefato de Entrada 7}} 
    ArtS7{{Artefato de Saída 7}} 
    Proc7[Procedimento 7] 
  end

  subgraph D8[Descrição 8]
    direction LR
    RH8([Recurso Humano 8]) 
    RNH8([Recurso Não Humano 8]) 
    ArtE8{{Artefato de Entrada 8}} 
    ArtS8{{Artefato de Saída 8}} 
    Proc8[Procedimento 8] 
  end

  subgraph D9[Descrição 9]
    direction LR
    RH9([Recurso Humano 9]) 
    RNH9([Recurso Não Humano 9]) 
    ArtE9{{Artefato de Entrada 9}} 
    ArtS9{{Artefato de Saída 9}} 
    Proc9[Procedimento 9] 
  end

  subgraph D10[Descrição 10]
    direction LR
    RH10([Recurso Humano 10]) 
    RNH10([Recurso Não Humano 10]) 
    ArtE10{{Artefato de Entrada 10}} 
    ArtS10{{Artefato de Saída 10}} 
    Proc10[Procedimento 10] 
  end

  subgraph D11[Descrição 11]
    direction LR
    RH11([Recurso Humano 11])
    RNH11([Recurso Não Humano 11])
    ArtE11{{Artefato de Entrada 11}}
    ArtS11{{Artefato de Saída 11}}
    Proc11[Procedimento 11]
  end

  subgraph D12[Descrição 12]
    direction LR
    RH12([Recurso Humano 12])
    RNH12([Recurso Não Humano 12])
    ArtE12{{Artefato de Entrada 12}}
    ArtS12{{Artefato de Saída 12}}
    Proc12[Procedimento 12]
  end

  subgraph D13[Descrição 13]
    direction LR
    RH13([Recurso Humano 13])
    RNH13([Recurso Não Humano 13])
    ArtE13{{Artefato de Entrada 13}}
    ArtS13{{Artefato de Saída 13}}
    Proc13[Procedimento 13]
  end

  subgraph D14[Descrição 14]
    direction LR
    RH14([Recurso Humano 14])
    RNH14([Recurso Não Humano 14])
    ArtE14{{Artefato de Entrada 14}}
    ArtS14{{Artefato de Saída 14}}
    Proc14[Procedimento 14]
  end

  subgraph D15[Descrição 15]
    direction LR
    RH15([Recurso Humano 15])
    RNH15([Recurso Não Humano 15])
    ArtE15{{Artefato de Entrada 15}}
    ArtS15{{Artefato de Saída 15}}
    Proc15[Procedimento 15]
  end

  Atv1 -.- D1
  Atv2 -.- D2
  Atv3 -.- D3
  Atv4 -.- D4
  Atv5 -.- D5
  Atv6 -.- D6
  Atv7 -.- D7
  Atv8 -.- D8
  Atv9 -.- D9
  Atv10 -.- D10
  Atv11 -.- D11
  Atv12 -.- D12
  Atv13 -.- D13
  Atv14 -.- D14
  Atv15 -.- D15

  class Atv1,Atv2,Atv3,Atv4,Atv5,Atv6,Atv7,Atv8,Atv9,Atv10,Atv11,Atv12,Atv13,Atv14,Atv15 atividade
  class Cond1,Cond2,Cond3,Cond4,Cond5 condicao
  class RH1,RH2,RH3,RH4,RH5,RH6,RH7,RH8,RH9,RH10,RH11,RH12,RH13,RH14,RH15 rh
  class RNH1,RNH2,RNH3,RNH4,RNH5,RNH6,RNH7,RNH8,RNH9,RNH10,RNH11,RNH12,RNH13,RNH14,RNH15 rnh
  class ArtE1,ArtE2,ArtE3,ArtE4,ArtE5,ArtE6,ArtE7,ArtE8,ArtE9,ArtE10,ArtE11,ArtE12,ArtE13,ArtE14,ArtE15 artEntrada
  class ArtS1,ArtS2,ArtS3,ArtS4,ArtS5,ArtS6,ArtS7,ArtS8,ArtS9,ArtS10,ArtS11,ArtS12,ArtS13,ArtS14,ArtS15 artSaida
  class Proc1,Proc2,Proc3,Proc4,Proc5,Proc6,Proc7,Proc8,Proc9,Proc10,Proc11,Proc12,Proc13,Proc14,Proc15 procedimento
```
