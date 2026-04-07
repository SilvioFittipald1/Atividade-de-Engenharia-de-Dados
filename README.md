# Atividade de Engenharia de Dados - Arquitetura Medalhão

## 📋 O que é este projeto?

Este projeto implementa uma **pipeline de dados** para processar informações de e-commerce utilizando a **Arquitetura Medalhão**. O objetivo é transformar dados brutos em informações analíticas prontas para uso, passando por três camadas de refinamento progressivo.

Os dados utilizados são do **dataset Olist** (marketplace brasileiro) e incluem informações sobre pedidos, clientes, produtos, vendedores, pagamentos e avaliações. Também são integrados dados de **cotação do dólar** via API do Banco Central.

## 🛠️ Tecnologias Utilizadas

- **Databricks** - Plataforma de processamento de dados
- **PySpark** - Framework para processamento distribuído
- **Delta Lake** - Formato de armazenamento transacional
- **SQL** - Queries e manipulação de dados
- **Python** - Linguagem principal
- **Unity Catalog** - Governança e catalogação de dados
- **Databricks Workflows** - Orquestração e agendamento da pipeline

## 🏗️ Camadas da Arquitetura


### **Bronze**
- Primeira camada de persistência
- Dados ingeridos sem transformações
- Mantém o formato original dos arquivos
- Adiciona timestamp de ingestão para rastreabilidade
- **10 tabelas criadas** com dados brutos do Olist e cotações do dólar

**Notebook**: `Atividade_land_to_bronze.ipynb`

### **Silver**
- Dados limpos e padronizados
- Colunas renomeadas para português
- Tipos de dados validados
- Registros duplicados removidos
- Valores nulos tratados
- Colunas calculadas adicionadas (ex: tempo de entrega)
- **10 tabelas criadas** entre dimensões (clientes, produtos, vendedores) e fatos (pedidos, pagamentos, avaliações)

**Notebook**: `Atividade_bronze_to_silver.ipynb`

### **Gold**
- Dados agregados para análise de negócio
- Métricas e indicadores prontos para consumo
- Duas visões principais:
  - **Visão Comercial**: receita, ticket médio, produtos mais/menos vendidos
  - **Visão de Qualidade**: avaliações, satisfação, ranking de produtos e vendedores
- **2 tabelas criadas** com agregações por período e categoria

**Notebook**: `Atividade_silver_to_gold.ipynb`

## 🔄 Pipeline de Execução

A pipeline é orquestrada pelo Databricks Workflow (`pipeline_medalhao.yaml`) e executa diariamente às 13h:

```
land_to_bronze → bronze_to_silver → silver_to_gold
```

Cada etapa depende da anterior, garantindo integridade e consistência dos dados.

## 👥 Autor

**Silvio Fittipaldi**  
📧 fittipaldisilvio@gmail.com
