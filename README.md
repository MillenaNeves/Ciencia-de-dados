# Previsão da Gravidade de Acidentes de Trânsito no Recife (2024)

Este projeto foi desenvolvido para a disciplina de Ciência de Dados e tem como objetivo construir um pipeline completo de ciência de dados para prever a gravidade de sinistros de trânsito na cidade do Recife utilizando o algoritmo **k-Nearest Neighbors (kNN)**.

## Sobre o Dataset
* **Fonte:** Portal de Dados Abertos da Prefeitura do Recife (Registros oficiais da CTTU de 2024).
* **Volume Inicial:** 5.315 observações e 37 atributos.
* **Variável Alvo (Target):** `natureza`, indicando a gravidade da ocorrência entre as classes:
  * **SEM VÍTIMA** (Classe amplamente majoritária)
  * **COM VÍTIMA**
  * **VÍTIMA FATAL** (Classe extremamente rara)

---

## Ciclo de Entregas do Projeto

### Entrega 1: Análise Exploratória e Diagnóstico (EDA)
Foco no mapeamento e qualidade inicial dos dados brutos.
* **Diagnóstico de Qualidade:** Identificação de 12 colunas 100% nulas (como limites de velocidade), problemas de formatação numérica (padrão brasileiro de vírgulas) e ruídos de digitação (datas no futuro).
* **Insights Principais:** Constatação de um **desbalanceamento extremo** de classes e forte assimetria à direita em atributos de contagem (vítimas, motos). O envolvimento de motocicletas foi identificado como o fator com maior correlação positiva com o número de vítimas.

### Entrega 2: Limpeza, Normalização e Encoding
Preparação geométrica dos atributos e validação inicial do modelo kNN (k=5).
* **Tratamento de Dados:** Remoção de colunas irrelevantes, imputação de nulos categóricos com a string `"DESCONHECIDO"` e aplicação de *clipping* via IQR nas variáveis de contagem.
* **Preservação de Dinâmicas:** Variáveis de geolocalização (latitude/longitude) e temporais não passaram por remoção de outliers para não apagar ocorrências reais da malha urbana (ex: madrugada ou bairros distantes).
* **Resultados & Ilusão da Acurácia:** O modelo atingiu uma acurácia global alta (~91%), mas um **F1-Score Macro mediano (~0.49)**. A análise revelou que o kNN negligencia a classe minoritária devido ao desbalanceamento. As melhores combinações envolveram **Quantile Transformer (Normal)** e **Effect Encoding**.

### Entrega 3: Seleção de Features e Redução de Dimensionalidade
* Aplicação de técnicas de seleção de atributos para remover ruídos e avaliar o impacto direto no desempenho do kNN.
* Testes com redução de dimensionalidade utilizando abordagens como PCA para contornar a "maldição da dimensionalidade" gerada pela alta cardinalidade de atributos como bairros.

### Entrega 4: Balanceamento de Dados
* Foco total na correção do desbalanceamento extremo evidenciado na Entrega 2.
* Implementação e comparação de estratégias de oversampling (ex: SMOTE) e undersampling para forçar o kNN a identificar corretamente as classes mais raras (especialmente acidentes fatais), buscando elevar o F1-Score Macro.

### Entrega Final: Pipeline Completo e Avaliação de Combinações
* Consolidação de todas as etapas anteriores em uma arquitetura de pipeline unificada.
* Testes sistemáticos de múltiplas combinações de pré-processamento avaliados via **validação cruzada** para garantir a estabilidade e robustez científica dos resultados do kNN.

---

## Tecnologias Utilizadas
* Python 3
* Pandas & NumPy (Manipulação de dados)
* Scikit-Learn (Pipelines, Transformações e kNN)
* Category Encoders (Effect / Sum Encoding)
* Matplotlib & Seaborn (Visualização de dados)

---
