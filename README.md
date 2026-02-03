# credit
# 📊 Análise de Risco de Crédito - Clusterização de Empresas (CVM)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow)


## 🎯 Objetivo do Projeto
REalizar a segmentação de risco de crédito de empresas listadas na B3 (Dados CVM) utilizando algoritmos de Machine Learning. 

---

## 🗂️ Dicionário de Dados
**Fonte Oficial:** [Dados Abertos CVM](https://dados.cvm.gov.br/) 
Os dados brutos foram extraídos das demonstrações financeiras (DFP) da CVM. Abaixo, a descrição das variáveis utilizadas:

### 1. Identificação e Dados Brutos
| **DENOM_CIA** | Razão Social (Nome) da empresa listada. |
| **CD_CVM** | Código único de identificação da empresa na CVM. |
| **Receita** | Receita Operacional Líquida (Vendas). |
| **Ebit** | *Earnings Before Interest and Taxes* (Lucro Operacional). Mede a geração de caixa da operação. |
| **Lucro** | Lucro Líquido final (após impostos e financeiro). |
| **Caixa** | Disponibilidades + Aplicações Financeiras. |
| **Divida_Total** | Soma da Dívida de Curto Prazo + Longo Prazo. |

### 2. Engenharia de Atributos (Indicadores Calculados)
Para a clusterização, foram criados indicadores fundamentais de análise de crédito:

| Indicador | Fórmula (Python) | Interpretação de Negócio |
| :--- | :--- | :--- |
| **Dívida Líquida** | `Dívida Total - Caixa` | O valor real da dívida descontando o que a empresa tem em caixa. |
| **Alavancagem Financeira** | `Dívida Líquida / Ebit` | **Principal driver.** Quantos anos de geração de caixa (EBIT) a empresa levaria para pagar sua dívida. <br>• *Quanto maior, maior o risco.* |
| **Margem Líquida** | `Lucro / Receita` | Eficiência operacional. Quanto sobra de lucro para cada R$ 1 vendido. <br>• *Quanto maior, menor o risco.* |
Obs.: foram baixados vários arquivos da CVM e compilados em um único arquivo para a finalidade deste projeto. 


---

## ⚖️ Comparação de Modelos: K-Means vs. DBSCAN
Para validar a robustez da segmentação, foram testadas duas abordagens:

### 1. K-Means (O Escolhido)
* **Abordagem:** Partição baseada em distância euclidiana.
* **Resultado:** Segmentou a carteira em 4 níveis claros de risco (Baixo, Médio, Alto, Queima de Caixa).
* **Decisão Estratégica:** Optou-se pelo K-Means pois ele oferece uma classificação acionável para 100% da base, permitindo a criação de uma régua de rating (A, B, C, D).

### 2. DBSCAN (A Validação)
* **Abordagem:** Densidade.
* **Resultado:** Identificou uma massa homogênea e isolou **30 empresas** como *outliers* extremos.
* **Insight:** O DBSCAN serviu para validar estatisticamente que as empresas classificadas como "Alto Risco" pelo K-Means são de fato anomalias do mercado.

---

## 📊 Visualização dos Resultados
O modelo gerou a imagem da Matriz de Risco, exportada para o Power BI para tomada de decisão executiva:

---
## 🚀 Conclusão e Aplicação de Negócio
A clusterização permitiu segmentar a carteira de 397 empresas em 4 perfis de risco distintos:

1.  **Alto Risco (Cluster 1):** Empresas altamente alavancadas. Ação sugerida: *Travamento de limites e monitoramento intensivo.*
2.  **Oportunidade (Cluster 0):** Baixa dívida e alta margem. Ação sugerida: *Oferta de produtos premium e aumento de exposição.*
3.  **Em Observação (Cluster 2):** Empresas com margens negativas (Queima de Caixa). Ação sugerida: *Acompanhamento de curto prazo.*
4.  **Médio Risco / Operacional (Cluster 3):** O "miolo" da carteira, com indicadores dentro da média de mercado. Ação sugerida: *Manutenção das condições atuais.*
---

## 🔮 Próximos Passos (Roadmap)
Atualmente estou expandindo a análise deste portfólio para incluir a dimensão temporal:

* [Em andamento] **Módulo de Séries Temporais:** Implementação de modelos **GARCH** para prever a volatilidade da carteira e antecipar a migração de risco entre os clusters ao longo do tempo (Early Warning Signals).

---
**Tecnologias:** Python, Pandas, Scikit-Learn, Power BI.
