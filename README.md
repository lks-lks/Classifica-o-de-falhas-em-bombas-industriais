# Classificação de Falhas em Bombas Industriais

Este projeto de Ciência de Dados tem como objetivo aplicar técnicas de aprendizado de máquina para **detectar e classificar falhas operacionais** em bombas industriais com base em dados de sensores coletados ao longo do tempo.

---

## 🎯 Objetivo

Construir um modelo capaz de classificar o tipo de falha de uma bomba industrial a partir de dados temporais sensoriais. As categorias de falhas são:

- `Normal`
- `Cavitation` (Cavitação)
- `Dry_run` (Trabalho a seco)
- `OverPressure` (Sobrepressão)

---

## 📁 Dados Utilizados

Foram utilizados arquivos CSV contendo telemetria das bombas em diferentes dias de operação:

- `2024-11-11.csv` – não utilizado por ausência de falhas compatíveis.
- `2024-11-12.csv` e `2024-11-13.csv` – usados para modelagem.

As janelas de falha foram definidas no script `dataset_targets.py`, simulando os momentos exatos de ocorrência de falhas para rotular os dados.

O dataset final consolidado foi salvo como:  
`bombas_rotuladas .csv`

---

## 🔎 Análise Exploratória (EDA)

- Conversão de datas e análise de intervalos entre registros (`Date`)
- Verificação de variáveis com maior impacto no comportamento da bomba
- Filtros aplicados com base no tipo de estator (`ESTATOR_NOVO`)
- Gráficos de linha por variável em diferentes estados operacionais

As falhas foram contextualizadas tecnicamente para interpretação:

| Falha          | Causa Técnica                                              |
|----------------|------------------------------------------------------------|
| Cavitação      | Pressão muito baixa no fluido gera bolhas de vapor         |
| Trabalho a seco| Ausência de fluido, causando atrito e superaquecimento     |
| Sobrepressão   | Fluido com pressão além do limite operacional da bomba     |

---

## ⚙️ Engenharia de Atributos

- Remoção de colunas irrelevantes (e.g. identificadores, strings)
- Criação de variáveis como: desvio padrão, média móvel, diffs temporais
- Normalização/Padronização (quando necessário)
- Exclusão de dados rotulados como "Unlabeled"

---

## 🤖 Modelagem

Dois modelos principais foram treinados e comparados:

### 1. Random Forest
- Classificador robusto para problemas com múltiplas classes e variáveis correlacionadas
- Hiperparâmetros ajustados:  
  `n_estimators=100`, `max_depth=None`, `random_state=42`

### 2. XGBoost
- Algoritmo de boosting com melhor capacidade preditiva
- Hiperparâmetros ajustados:  
  `n_estimators=200`, `learning_rate=0.1`, `max_depth=6`, `subsample=0.8`

---

## 📊 Avaliação

- Divisão treino/teste: 80/20
- Classes balanceadas artificialmente, sem oversampling
- Métricas de avaliação:
  - Acurácia
  - **F1-score macro** e por classe
  - Matriz de Confusão
  - Classificação detalhada com `classification_report`

### Resultado:
- **F1-Score geral** acima de 0.90 com Random Forest
- XGBoost teve leve vantagem em recall para classes minoritárias

---

## 📈 Visualizações Geradas

- Gráficos de linha por tipo de falha
- Boxplots para variáveis sensíveis
- Matriz de correlação entre sensores
- Gráficos de importância de atributos (feature importance)

---

## 📂 Estrutura dos Arquivos

- `Categoria_bombas.ipynb`: Notebook principal com todo o fluxo do projeto
- `dataset_targets.py`: Script com as janelas simuladas de falhas
- `bombas_rotuladas (2).csv`: Dataset final rotulado utilizado para treinamento

---

## 🧭 Próximos Passos

- Desenvolver modelo de **detecção de anomalias** incluindo registros "Unlabeled"
- Implementar pipeline em **ambiente de produção** com gatilho de desligamento remoto da bomba
- Ajustar janela temporal e detecção em tempo real para operações contínuas

---

## 👨‍💻 Autor

Projeto desenvolvido como desafio técnico prático com foco em aplicações reais de Machine Learning na indústria.

