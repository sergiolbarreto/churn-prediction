# 🚀 Projeto Final: Previsão de Churn em Telecom

## 👥 Grupo
- Sérgio Barreto (slbp)  
- Gabriel Felipo (gfrm)  
- Roseane Oliveira (rocg)  
- João Victor Soares (jvsf)  
- Filipe Eduardo Ferreira da Silva (fefs)  

## 📝 Descrição do Projeto
Este projeto tem como objetivo desenvolver e avaliar modelos de classificação para prever o **churn** (abandono) de clientes em uma empresa de telecomunicações.  

Foi utilizada uma base de dados real do Kaggle e explorados diversos classificadores, incluindo redes neurais como **MLP** e modelos baseados em Transformers como **STab** e **TabPFN**, além de modelos tradicionais como **Random Forest** e **Gradient Boosting** para comparação.

### 🎯 Objetivos
1. **Pré-processar** a base de dados: tratar valores ausentes, realizar codificação e normalização.
2. **Dividir** os dados em treino, validação e teste de forma estratificada e sem vazamento de dados.
3. **Implementar e treinar** múltiplos modelos de classificação.
4. **Otimizar hiperparâmetros** com a biblioteca **Optuna**, usando a métrica **KS (Kolmogorov-Smirnov)** como foco.
5. **Avaliar desempenho** com métricas como KS, AUC-ROC, Matriz de Confusão, Acurácia, Precisão, Recall, F1-Score e MSE.
6. **Documentar e comparar** os resultados para identificar o modelo mais performático.

## 📂 Base de Dados
- Fonte: [Customers churned in telecom services - Kaggle](https://www.kaggle.com/datasets/kapturovalexander/customers-churned-in-telecom-services/data)  

## 🛠️ Tecnologias e Ferramentas
- **Linguagem:** Python  
- **Bibliotecas:** Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, Optuna, TensorFlow, PyTorch, TabPFN, STab  
- **Modelos:** MLP, STab, TabPFN, Random Forest, Gradient Boosting  
- **Métricas:** KS, AUC-ROC, Confusion Matrix, Accuracy, Precision, Recall, F1-score, MSE  

## 📊 Estrutura Geral do Projeto
1. **Configuração do ambiente** e instalação de dependências.
2. **Análise exploratória de dados (EDA)** com visualizações e estatísticas descritivas.
3. **Pré-processamento**: tratamento de valores ausentes, codificação e normalização.
4. **Divisão de dados** em treino, validação e teste.
5. **Treinamento e avaliação** de diferentes modelos.
6. **Otimização de hiperparâmetros** com Optuna.
7. **Comparação de resultados** e escolha do modelo final.

---
✍️ *Projeto desenvolvido como trabalho final de curso.*
