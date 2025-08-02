# Projeto: Decifrando Emoções Musicais 🎵

Uma análise preditiva com Machine Learning para classificar emoções a partir de características de áudio de músicas do Spotify. Este projeto foi desenvolvido como resposta a um desafio para explorar e comparar modelos de classificação.

## 🎯 Objetivo

O objetivo principal deste projeto é investigar a capacidade de modelos de Machine Learning, como **Regressão Logística** e **Random Forest**, em prever a emoção principal transmitida por uma música (`main_emotion`) utilizando suas características de áudio fornecidas pelo Spotify.

## 💿 O Dataset Utilizado

Os dados foram extraídos do dataset **"500K+ Spotify Songs with Lyrics,Emotions & More"**, disponível no [Kaggle](https://www.google.com/search?q=https://www.kaggle.com/datasets/suraj520/500k-spotify-songs-with-lyrics-emotions-more).

Dada a grande dimensão dos dados originais (+500 mil músicas), foi criada uma **amostra aleatória** para garantir a agilidade no pré-processing e na fase de treinamento dos modelos, permitindo um ciclo de experimentação mais rápido e eficiente.

## 🛠️ Estrutura e Fluxo de Trabalho do Projeto

O projeto foi organizado em dois notebooks sequenciais para garantir a separação de responsabilidades e a reprodutibilidade do processo:

1.  **`01_EDA_e_Pre-processamento.ipynb`**:

      * Carga dos dados brutos.
      * Análise Exploratória de Dados (EDA) para entender a distribuição e as relações entre as features.
      * Limpeza, tratamento de valores ausentes e engenharia de features.
      * O resultado é um DataFrame limpo e preparado para a modelagem.

2.  **`dados_limpos_para_modelagem.parquet`**:

      * Arquivo intermediário no formato Parquet, que armazena os dados processados de forma eficiente.

3.  **`02_Modelagem_e_Avaliacao.ipynb`**:

      * Carrega os dados processados do arquivo Parquet.
      * Divide os dados em conjuntos de treino e teste.
      * Aplica o escalonamento de features (`StandardScaler`).
      * Treina e avalia os modelos de classificação.
      * Compara a performance dos modelos para determinar o mais eficaz para o problema.

## 💻 Tecnologias Utilizadas

  * **Python 3**
  * **Pandas e NumPy** para manipulação de dados.
  * **Scikit-learn** para pré-processamento, modelagem e avaliação.
  * **Matplotlib e Seaborn** para visualização de dados.
  * **Jupyter Notebook** como ambiente de desenvolvimento.

## 📊 Resultados e Desafios

Após a fase de modelagem e avaliação, o modelo que apresentou o melhor desempenho geral foi o **Random Forest**.

  * **Scores F1 (validação cruzada de 5 folds):** `[0.654, 0.657, 0.656, 0.655, 0.654]`
  * **Média do F1-Score:** **0.6556**
  * **Desvio Padrão do F1-Score:** **0.0010**

### Matriz de Confusão - Random Forest

### Análise Crítica dos Desafios

Um dos principais desafios observados foi a dificuldade do modelo em assimilar as diferenças entre classes muito semelhantes. Como pode ser visto na matriz de confusão, o modelo confundiu bastante as classes **1 (Joy)** e **3 (Negative Valence)**.

Isso sugere que, embora o Random Forest seja robusto para problemas multiclasse, as características de áudio para essas duas emoções são muito parecidas, e o modelo não conseguiu capturar suas peculiaridades sutis apenas com a engenharia de features inicial.

## 🚀 Conclusões e Próximos Passos

Este projeto foi uma jornada de aprendizado valiosa, especialmente no que diz respeito à importância da engenharia de features e à análise crítica dos resultados de um modelo. Com base nos achados, os próximos passos seriam focados mais no aprendizado do que puramente na performance:

1.  **Retornar ao Pré-processamento:** O próximo passo lógico seria aprofundar a engenharia de features, buscando "levantar" as diferenças entre as classes problemáticas. Isso poderia envolver a criação de features polinomiais ou de interação (ex: combinar BPM com gênero musical) para fortalecer as características que separam "Joy" de "Negative Valence", ou até mesmo usar técnicas como **Análise de Componentes Principais (PCA)** para criar features mais representativas.

2.  **Ajuste de Hiperparâmetros:** Explorar como os hiperparâmetros do Random Forest influenciam a criação dos nós da árvore, buscando privilegiar as peculiaridades de cada classe.

3.  **Explorar Modelos de Boosting:** Como último recurso, caso os ajustes anteriores não tragam melhorias satisfatórias, uma abordagem seria utilizar modelos mais complexos e "apelativos" como **LightGBM**, **Gradient Boosting** ou **XGBoost**. No entanto, a prioridade seria esgotar o aprendizado com o Random Forest, visto que os modelos de boosting, apesar de potentes, podem mascarar a necessidade de um bom trabalho de feature engineering e demandam maior poder computacional.

## ⚙️ Como Executar o Projeto

1.  Clone o repositório:
    ```bash
    git clone https://github.com/RosettiBR/Case_Music_Emotion.git
    ```
2.  Crie um ambiente virtual e instale as dependências. Recomenda-se criar um arquivo `requirements.txt`.
3.  Baixe os dados do Kaggle e coloque-os em uma pasta `data/` na raiz do projeto.
4.  Execute os notebooks na ordem numérica: `01_EDA_e_Pre-processamento.ipynb` e, em seguida, `02_Modelagem_e_Avaliacao.ipynb`.
