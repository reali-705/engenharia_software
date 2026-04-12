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
  subgraph Processo de Desenvolvimento
    direction LR
    Inicio(( )) ==>
    Atv1([Atividade 1]) ==>
    Atv2([Atividade 2]) ==>
    Cond1{Condição 1} ==>|Sim| Atv3
    Cond1 ==>|Não| Atv1
    Atv3([Atividade 3]) ==>
    Atv4([Atividade 4]) ==>
    Atv5([Atividade 5]) ==>
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

  Atv1 -.- D1
  Atv2 -.- D2
  Atv3 -.- D3
  Atv4 -.- D4
  Atv5 -.- D5

  class Atv1,Atv2,Atv3,Atv4,Atv5 atividade
  class Cond1 condicao
  class RH1,RH2,RH3,RH4,RH5 rh
  class RNH1,RNH2,RNH3,RNH4,RNH5 rnh
  class ArtE1,ArtE2,ArtE3,ArtE4,ArtE5 artEntrada
  class ArtS1,ArtS2,ArtS3,ArtS4,ArtS5 artSaida
  class Proc1,Proc2,Proc3,Proc4,Proc5 procedimento
```
