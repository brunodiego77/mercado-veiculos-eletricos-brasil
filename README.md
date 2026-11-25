# ⚡ Inteligência de Mercado: Veículos Elétricos e Infraestrutura de Recarga no Brasil (2024–2026)

Pipeline de Engenharia e Análise de Dados **End-to-End** construído no **Databricks (Serverless Compute)** utilizando **PySpark**, **Spark SQL**, **Delta Lake** e **Unity Catalog**, estruturado na **Arquitetura Medallion** (Raw → Bronze → Silver → Gold) e orquestrado via **Databricks Workflows**.

---

## 🎯 Objetivo de Negócio

Avaliar a viabilidade comercial e mapear oportunidades de expansão para operações de veículos eletrificados e infraestrutura de recarga (eletropostos) nos **27 estados brasileiros**, respondendo a três perguntas estratégicas:
1. Quais estados combinam **alta demanda de compra**, **incentivo tributário (IPVA)** e **escassez de eletropostos**?
2. Qual é o volume financeiro estimado (**VGC**) e a liderança por montadora e tecnologia (**Plug-in BEV/PHEV** vs. **Híbrido Convencional HEV/MHEV**)?
3. Onde estão os maiores gargalos de recarga na relação entre frota circulante plug-in e pontos públicos disponíveis?

---

## 📈 Amostra dos Resultados (`gold_viabilidade_mercado_uf`)

| UF | Estado | Regra IPVA 2026 | Emplacamentos (30m) | Frota Plug-in | Eletropostos | Carros Plug-in / Posto | Diagnóstico Estratégico |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| **SP** | São Paulo | Integral (4%) | 259.130 | 124.884 | 243 | 513,9 | Forte Expansão com Gargalo de Recarga |
| **MG** | Minas Gerais | Integral (4%) | 87.116 | 32.314 | 101 | 319,9 | Forte Expansão com Gargalo de Recarga |
| **DF** | Distrito Federal | **Isento (0%)** | 74.790 | 38.607 | 166 | 232,6 | Alta Demanda + Incentivo Fiscal |
| **BA** | Bahia | **Isento (0%)** | 35.550 | 20.041 | 63 | 318,1 | Alta Demanda + Incentivo Fiscal |
| **PE** | Pernambuco | **Isento (0%)** | 30.685 | 21.101 | 34 | **620,6** | Alta Demanda + Incentivo Fiscal (Gargalo) |
| **MT** | Mato Grosso | Integral | 14.347 | 6.919 | 4 | **1.729,8** | Gargalo Extremo de Infraestrutura |

---

## 🛠️ Stack Tecnológica

* **Plataforma:** Databricks Free Edition (Serverless Compute)
* **Processamento & Linguagens:** PySpark, Spark SQL, Python (Pandas / OpenPyXL)
* **Armazenamento & Governança:** Delta Lake, Unity Catalog (Volumes e Linhagem de Dados)
* **Orquestração:** Databricks Workflows (DAG sequencial de 4 tarefas executadas em ~2 min)

---

## 📂 Estrutura do Repositório

```text
├── 01_ingestao_raw_veiculos.ipynb      # Ingestão de CSVs e XLSX (Volumes -> Delta Raw)
├── 02_camada_bronze_veiculos.ipynb     # Tipagem, tratamento de nulos textuais e deduplicação
├── 03_camada_silver_veiculos.ipynb     # Padronização de UFs e classificação Plug-in vs. Híbrido
├── 04_camada_gold_veiculos.ipynb       # Cruzamento multi-fonte, VGC estimado e matriz por UF
└── README.md                           # Documentação técnica e insights de negócio
