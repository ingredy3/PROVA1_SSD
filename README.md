# 🛡️ MVP - Sistema de Suporte à Decisão: Detecção de Intrusões em Rede com UNSW-NB15

## 📖 Definição do Problema
A segurança de redes de computadores é um desafio crítico na era digital, com ataques cibernéticos se tornando cada vez mais sofisticados e frequentes.  
Detectar intrusões em tempo real é essencial para proteger sistemas e dados contra acessos não autorizados e atividades maliciosas.

Este projeto tem como objetivo **desenvolver um sistema de classificação binária para identificar ataques em redes de computadores**, utilizando o dataset moderno UNSW-NB15 que simula tráfego de rede realista.

---

## 🎯 Hipótese
- **Hipótese principal:** Modelos clássicos de Machine Learning (Random Forest, SVM, Regressão Logística) conseguem identificar padrões discriminativos para detecção de intrusões com alta acurácia.  
- **Hipóteses secundárias:**  
  - Features relacionadas a volume de dados (bytes, pacotes) são altamente preditivas
  - Protocolos e serviços específicos estão mais associados a atividades maliciosas
  - O dataset apresenta redundâncias que podem ser exploradas para feature selection

---

## 📊 Conjunto de Dados
O dataset utilizado foi **[UNSW-NB15 Network Intrusion Dataset (Kaggle)](https://www.kaggle.com/datasets/mrwellsdavid/unsw-nb15)**.  

- **Total de registros:** 82.332 instâncias de tráfego de rede
- **Features:** 45 atributos (40 numéricas + 4 categóricas + 1 target)
- **Distribuição das classes:**
  - **Ataque (label=1):** 45.332 instâncias (55.06%)
  - **Normal (label=0):** 37.000 instâncias (44.94%)
- **Categorias de ataque:** 9 tipos diferentes (Analysis, Backdoors, DoS, Exploits, Fuzzers, Generic, Reconnaissance, Shellcode, Worms)

---

## 🛠️ Metodologia

### 1. **Configuração do Ambiente**
- Importação de bibliotecas essenciais (pandas, numpy, scikit-learn, matplotlib, seaborn)
- Configuração de reprodutibilidade
- Supressão de avisos para melhor legibilidade

### 2. **Carregamento e Exploração dos Dados**
- Download automático via API Kaggle
- Análise da estrutura do dataset (82.332 linhas × 45 colunas)
- Verificação de valores ausentes (nenhum encontrado)
- Análise de distribuição das classes

### 3. **Análise Exploratória (EDA)**
- Identificação de tipos de dados (30 int64, 11 float64, 4 object)
- Análise de correlação entre features
- Identificação de redundâncias (alta correlação >0.97 entre algumas features)
- Distribuição balanceada (55% attack vs 45% normal)

### 4. **Pré-processamento**
- Separação de features numéricas e categóricas
- Remoção de colunas não relevantes ('id', 'attack_cat')
- Aplicação de StandardScaler para features numéricas
- OneHotEncoder para features categóricas ('proto', 'service', 'state')
- Divisão estratificada: 80% treino, 20% teste

### 5. **Modelagem**
- **Modelos testados:** Random Forest, Logistic Regression, K-Nearest Neighbors
- **Validação cruzada:** Stratified K-Fold (5 folds)
- **Otimização:** GridSearchCV para hiperparâmetros
- **Métricas:** Acurácia, Precision, Recall, F1-Score, AUC-ROC

### 6. **Avaliação e Seleção**
- Comparação entre modelos base e otimizados
- Análise de matrizes de confusão
- Curvas ROC e cálculo de AUC
- Identificação do melhor modelo baseado em múltiplas métricas

---

## 📈 Resultados

### Modelos Testados
- **Random Forest** → Melhor desempenho geral
- **Logistic Regression** → Bom balance entre performance e interpretabilidade  
- **K-Nearest Neighbors** → Performance competitiva

### Métricas do Melhor Modelo (Random Forest):
- **Acurácia:** > 95%
- **Precision:** > 96% 
- **Recall:** > 95%
- **F1-Score:** > 95%
- **AUC-ROC:** > 0.99

### Interpretação:
- O modelo consegue detectar intrusões com **alta confiabilidade**
- **Baixa taxa de falsos positivos** - crucial para sistemas de produção
- **Alta taxa de verdadeiros positivos** - detecta a maioria dos ataques
- As features mais importantes incluem:
  - **Volume de dados** (sbytes, dbytes)
  - **Contagem de pacotes** (spkts, dpkts)  
  - **Protocolos e serviços** (proto, service)
  - **Taxas de transmissão** (rate, sload, dload)

---

## 📊 Visualizações Principais
- **Matrizes de Confusão** → Comparação visual do desempenho por modelo
- **Curvas ROC** → Análise da capacidade discriminativa (AUC > 0.99)
- **Importância de Features** → Identificação dos atributos mais relevantes
- **Distribuição de Classes** → Verificação do balanceamento do dataset
- **Análise de Correlação** → Detecção de redundâncias entre features

---

## ✅ Conclusões

### Confirmação das Hipóteses
- ✅ **Modelos clássicos são eficazes** para detecção de intrusões
- ✅ **Features de volume são altamente preditivas** como esperado
- ✅ **Protocolos específicos** mostram forte associação com ataques
- ✅ **Dataset bem balanceado** permitiu treinamento robusto

### Contribuições Técnicas
1. **Pipeline reprodutível** desde o carregamento até a avaliação
2. **Análise comparativa abrangente** entre múltiplos algoritmos
3. **Otimização sistemática** de hiperparâmetros
4. **Avaliação multicritério** com métricas complementares

### Aplicabilidade Prática
- Sistema pode ser integrado em **IDS (Intrusion Detection Systems)**
- **Baixa latência** de previsão adequada para tempo real
- **Alta confiabilidade** reduz alertas falsos em ambientes produtivos

---

## 🎯 Próximos Passos

1. **Feature Engineering** → Criar features derivadas específicas para segurança
2. **Ensemble Methods** → Combinar múltiplos modelos para melhor performance  
3. **Deep Learning** → Explorar redes neurais para detecção de padrões complexos
4. **Deploy em Tempo Real** → Integrar com sistemas de monitoramento de rede
5. **Detecção de Novos Ataques** → Implementar aprendizado contínuo

---

## 📚 Referências

- [UNSW-NB15 Dataset Documentation](https://www.unsw.adfa.edu.au/unsw-canberra-cyber/cybersecurity/ADFA-NB15-Datasets/)
- Moustafa, N., & Slay, J. (2015). UNSW-NB15: a comprehensive data set for network intrusion detection systems.
- Scikit-learn Documentation
- Kaggle UNSW-NB15 Dataset

---

**🚀 Desenvolvido como parte do MVP de Sistemas de Suporte à Decisão**

*Universidade de Brasília - Departamento de Engenharia de Produção*




