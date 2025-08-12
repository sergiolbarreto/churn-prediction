# 🚀 Projeto de Previsão de Churn em Telecom

## 📝 Descrição do Projeto

Este projeto tem como objetivo principal desenvolver e avaliar modelos de classificação para prever o **churn** (abandono) de clientes em uma empresa de telecomunicações. Utilizou-se uma base de dados real do Kaggle para treinar e comparar diferentes abordagens, desde modelos de Machine Learning tradicionais até arquiteturas de Deep Learning modernas.

O foco da avaliação é a métrica **KS (Kolmogorov-Smirnov)**, que mede a capacidade de um modelo de separar clientes que dão churn daqueles que não dão. Essa é uma métrica crucial para o negócio, pois indica quão bem o modelo pode segmentar a base de clientes para ações de retenção.

### 🎯 Objetivos Principais

1. **Pré-processar a base de dados**: Tratar valores ausentes, realizar codificação de variáveis categóricas com `TargetEncoder` e normalizar as features numéricas.  
2. **Dividir os dados**: Criar conjuntos de treino (50%), validação (25%) e teste (25%) de forma estratificada para manter a proporção da variável alvo.  
3. **Implementar e treinar modelos**: Explorar diversos modelos, incluindo `Random Forest`, `Gradient Boosting`, e redes neurais como `MLP`, `TabPFN` e `STab`.  
4. **Otimizar hiperparâmetros**: Utilizar a biblioteca `Optuna` para encontrar os melhores hiperparâmetros para cada modelo, com foco na maximização do score KS.  
5. **Avaliar o desempenho**: Analisar os resultados de forma detalhada, utilizando métricas como KS, AUC-ROC, Acurácia, Precisão, Recall e F1-Score no conjunto de teste.  
6. **Documentar e comparar**: Elaborar uma tabela comparativa para identificar o modelo mais performático para o objetivo de negócio.

---

## 🛠️ Modelos e Pré-processamento

### Pré-processamento e Balanceamento

O pipeline de pré-processamento foi desenhado para evitar vazamento de dados (*data leakage*) e para preparar a base de dados de forma robusta:

- **Divisão Estratificada**: O dataset foi dividido em treino (50%), validação (25%) e teste (25%) com `train_test_split` usando `stratify=y` para garantir que a proporção de clientes com e sem churn fosse mantida em todos os conjuntos.  
- **Codificação e Normalização**: Para lidar com dados categóricos, foi aplicado `TargetEncoder`, que utiliza a média da variável alvo para codificar as categorias. Para as variáveis numéricas, o `StandardScaler` foi utilizado para padronizar os dados. Ambas as transformações foram ajustadas (fit) **apenas no conjunto de treino**.  
- **Balanceamento de Classes**: Como a base de dados era desbalanceada, foi usado o `SMOTE` (`Synthetic Minority Over-sampling Technique`) para gerar amostras sintéticas da classe minoritária (clientes com churn), criando um conjunto de treino balanceado para os modelos.

### Modelos de Classificação

O projeto explorou uma gama de modelos, dos mais tradicionais aos mais modernos baseados em Deep Learning:

- **Random Forest**: Um modelo de ensemble robusto que serviu como baseline de alta performance. Seus hiperparâmetros foram ajustados com `Optuna`.  
- **Gradient Boosting**: Outro modelo de ensemble poderoso, com otimização de hiperparâmetros via `Optuna`, considerado um dos modelos mais fortes para dados tabulares.  
- **MLP (Multi-Layer Perceptron)**: Uma rede neural básica, mas eficaz, implementada com TensorFlow/Keras e otimizada com `Optuna`.  
- **TabPFN (Tabular PFN)**: Um modelo Transformer pré-treinado, que não requer otimização de hiperparâmetros e é projetado para funcionar "out-of-the-box" em dados tabulares. O modelo tem uma limitação de 1024 amostras, portanto, um subconjunto dos dados foi utilizado.  
- **STab (Tabular Transformer)**: Outro modelo baseado em Transformer, mas que necessita de treinamento do zero. Implementado com PyTorch, foi avaliado após uma otimização com `Optuna`.

---

## 🏆 Comparação de Desempenho no Conjunto de Teste

A tabela abaixo resume o desempenho final de cada modelo, ordenado pela métrica-chave **KS**.

| Modelo           | KS     | AUC    | MSE    | Accuracy | Precision | Recall  | F1-Score |
|:-----------------|:-------|:-------|:-------|:---------|:----------|:--------|:---------|
| Gradient Boosting | 0.5429 | 0.8420 | 0.1358 | 0.7978   | 0.6546    | 0.5032  | 0.5690   |
| Random Forest    | 0.5401 | 0.8418 | 0.1360 | 0.8007   | 0.6667    | 0.4968  | 0.5693   |
| STab             | 0.5397 | 0.8436 | 0.1369 | 0.7939   | 0.6390    | 0.5118  | 0.5684   |
| TabPFN           | 0.5395 | 0.8423 | 0.1358 | 0.8052   | 0.6574    | 0.5546  | 0.6016   |
| MLP              | 0.5222 | 0.8301 | 0.1425 | 0.7848   | 0.6189    | 0.4904  | 0.5472   |

### Análise dos Resultados

- **Liderança do Gradient Boosting**: Com o maior score **KS (0.5429)**, o `Gradient Boosting` se mostrou o modelo mais eficaz em separar as classes de clientes com alta e baixa probabilidade de churn. Isso o torna a escolha ideal para o objetivo central do projeto, que é identificar grupos de alto risco com precisão para direcionar ações de retenção.  
- **Destaque do TabPFN**: O `TabPFN` apresentou o melhor **Recall (0.5546)**, o que significa que ele foi o melhor em identificar corretamente os clientes que de fato dariam churn. Além disso, alcançou a maior **Acurácia (0.8052)** e **F1-Score (0.6016)**, demonstrando um ótimo equilíbrio entre as métricas.  
- **Força do Random Forest**: O `Random Forest` alcançou a maior **Precisão (0.6667)**, sendo a melhor opção quando o custo de uma intervenção indevida é alto.  
- **Redes Neurais Tradicionais**: O `MLP` ficou em último lugar, indicando que modelos mais complexos de Deep Learning (como os baseados em Transformers) ou modelos de ensemble (como Gradient Boosting e Random Forest) são mais adequados para a natureza dos dados tabulares deste problema.

---

## 📌 Conclusão e Próximos Passos

O **Gradient Boosting** é o modelo recomendado como a solução principal, pois sua superioridade na métrica **KS** o torna o mais adequado para o problema de segmentação de churn. No entanto, o **TabPFN** e o **Random Forest** também se destacam em cenários de negócio específicos, oferecendo um leque de opções dependendo da prioridade (cobertura vs. precisão).

Para aprimorar a solução, as seguintes etapas são sugeridas:

- **Refinamento de Hiperparâmetros**: Explorar mais a fundo o espaço de busca do `Optuna` para o `Gradient Boosting`, talvez com um foco em aumentar o `recall` sem comprometer o KS.  
- **Técnicas de Ensemble**: Testar combinações (stacking ou blending) entre os modelos líderes, como `Gradient Boosting` e `TabPFN`, para buscar um desempenho ainda mais robusto.  
- **Engenharia de Features**: Criar novas variáveis a partir dos dados existentes (ex: tempo de permanência vs. gastos totais) para aumentar o poder preditivo dos modelos.
