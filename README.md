# ⚡ Inteligência de Mercado: Veículos Elétricos e Infraestrutura de Recarga no Brasil (2024–2026)

Pipeline de Engenharia e Análise de Dados **End-to-End** construído no **Databricks (Serverless Compute)** utilizando **PySpark**, **Spark SQL**, **Delta Lake** e **Unity Catalog**, estruturado na **Arquitetura Medallion** (Raw → Bronze → Silver → Gold) e orquestrado via **Databricks Workflows**.

---

## 🎯 Objetivo de Negócio

Avaliar a viabilidade comercial e mapear oportunidades de expansão para operações de veículos eletrificados e infraestrutura de recarga (eletropostos) nos **27 estados brasileiros**, respondendo a três perguntas estratégicas:
1. Quais estados combinam **alta demanda de compra**, **incentivo tributário (IPVA)** e **escassez de eletropostos**?
2. Qual é o volume financeiro estimado (**VGC**) e a liderança por montadora e tecnologia (**Plug-in BEV/PHEV** vs. **Híbrido Convencional HEV/MHEV**)?
3. Onde estão os maiores gargalos de recarga na relação entre frota circulante plug-in e pontos públicos disponíveis?

---

## 🏗️ Arquitetura da Solução (Medallion + Workflows)

```mermaid
flowchart LR
    subgraph Fontes["📥 Fontes de Dados"]
        F1["SENATRAN (Excel)\nFrota Circulante Out/2026"]
        F2["ABVE / Recarregados (CSV)\nEmplacamentos 30 meses"]
        F3["Legislação IPVA 2026 (CSV)\nRegras e Alíquotas por UF"]
        F4["Fichas Técnicas (CSV)\nPreços e Especificações"]
        F5["Pipeline Anterior (Delta)\ngold_estacoes_estados"]
    end

    subgraph Databricks["🧱 Databricks Lakehouse (Unity Catalog)"]
        RAW["Camada RAW\n4 Tabelas Delta Brutas"]
        BRONZE["Camada BRONZE\nTipagem, Deduplicação e Nulos"]
        SILVER["Camada SILVER\nPadronização UF e Regras Plug-in"]
        GOLD["Camada GOLD\ngold_viabilidade_mercado_uf\ngold_ranking_modelos_ev"]
    end

    F1 & F2 & F3 & F4 --> RAW
    RAW --> BRONZE --> SILVER --> GOLD
    F5 --> GOLD
 ```

### Etapas Orquestradas no Workflow (`pipeline_mercado_carros_eletricos`)

<img width="1726" height="591" alt="Execução do Workflow Databricks" src="https://github.com/user-attachments/assets/c3a8e261-a68a-46a0-8bfd-5d4f1f5bc882" />


