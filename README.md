# 🧠 MVP — Prova 1- Sistema de Detecção de Intrusões (UNSW-NB15)

## 📘 Descrição Geral
Este projeto foi desenvolvido como parte da **Prova 1 da disciplina SSD (Sistemas de Suporte à Decisão)**, no curso de **Engenharia de Produção – UnB**.  
O objetivo é **criar e avaliar modelos de machine learning** capazes de identificar **ataques de rede (intrusões)** com base no dataset **UNSW-NB15**, amplamente utilizado em pesquisas de segurança cibernética.

---

## 🎯 Objetivo do Projeto
Desenvolver um **modelo preditivo supervisionado** que classifique o tráfego de rede em duas categorias:

- `0` → **Normal** (tráfego legítimo)  
- `1` → **Attack** (tráfego malicioso)

O modelo final deve alcançar **alta acurácia e generalização**, auxiliando na construção de sistemas inteligentes de **detecção de intrusões (IDS)**.

---

## 📊 Dataset Utilizado
- **Nome:** UNSW-NB15  
- **Fonte:** [Kaggle – mrwellsdavid/unsw-nb15](https://www.kaggle.com/datasets/mrwellsdavid/unsw-nb15)  
- **Tamanho:** 82.332 registros e 45 variáveis  
- **Target:** `label`  
- **Classes:**
  - `0` → Normal  
  - `1` → Attack  
- **Variáveis categóricas:** `proto`, `service`, `state`  
- **Coluna removida:** `attack_cat` (evita *data leakage*)  
- **Situação:** sem valores ausentes, dados estruturados e limpos.

---

## ⚙️ Pipeline de Desenvolvimento

| Etapa | Descrição |
|-------|------------|
| **1️⃣ Importação e EDA** | Inspeção dos dados, verificação de tipos e identificação de vazamentos. |
| **2️⃣ Pré-processamento** | Escalonamento (`StandardScaler`) e codificação (`OneHotEncoder`) das features. |
| **3️⃣ Divisão Treino/Teste** | 80% treino, 20% teste, com estratificação das classes. |
| **4️⃣ Validação Cruzada** | 3-Fold estratificada para garantir robustez dos resultados. |
| **5️⃣ Modelagem** | Modelos: Logistic Regression, KNN e Random Forest. |
| **6️⃣ Otimização de Hiperparâmetros** | `RandomizedSearchCV` e `GridSearchCV` aplicados ao Random Forest. |
| **7️⃣ Avaliação Final** | Comparação dos modelos em métricas de *accuracy*, *precision*, *recall* e *F1-score*. |

---

## 🤖 Modelos Avaliados

| Modelo | Tipo | Status |
|--------|------|--------|
| **Random Forest (otimizado)** | Ensemble de árvores | ✅ Melhor desempenho |
| **K-Nearest Neighbors (k=5)** | Baseado em instâncias | ✅ Alternativo |
| **Logistic Regression** | Linear supervisionado | ✅ Comparativo |

---

## 📈 Resultados Obtidos

| Modelo | Accuracy | Precision | Recall | F1-Score |
|--------|-----------|-----------|--------|----------|
| **Random Forest (Otimizado)** | **0.9973** | **0.9973** | **0.9973** | **0.9973** |
| **KNN (k=5)** | 0.9782 | 0.9782 | 0.9782 | 0.9782 |
| **Logistic Regression** | 0.9544 | 0.9544 | 0.9544 | 0.9544 |

📊 **Interpretação:**  
O **Random Forest** superou os demais modelos, apresentando desempenho quase perfeito (F1 = 0.997).  
Nenhum modelo apresentou *overfitting*, e todos mantiveram resultados consistentes entre treino e teste.

---

## 🧠 Conclusões

- ✅ O MVP cumpre integralmente os requisitos da Prova 1 SSD.  
- ✅ O pipeline é **reprodutível, limpo e escalável**.  
- ✅ O modelo final (Random Forest) apresentou **excelente desempenho e estabilidade**.  
- 🔒 Evitou-se *data leakage* removendo `attack_cat` antes da modelagem.  
- 📂 Resultados foram exportados em `results_summary.csv`.

---

## 🚀 Próximos Passos

- Aplicar **XGBoost** ou **LightGBM** para comparar com o Random Forest.  
- Implementar **feature importance** para reduzir dimensionalidade.  
- Expandir o modelo para **classificação multiclasses** (usando `attack_cat`).  
- Criar uma **API de inferência** para aplicação prática do modelo em tempo real.

---

## 🧩 Tecnologias Utilizadas

| Categoria | Ferramentas |
|------------|-------------|
| **Linguagem** | Python 3.12 |
| **Ambiente** | Google Colab |
| **Bibliotecas principais** | `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `scipy` |
| **Versionamento** | Git + GitHub |
| **Fonte de dados** | Kaggle API |

---

## 💡 Autoria
**Aluno:** *Ingredy Thamis*  
**Curso:** Engenharia de Produção — UnB  
**Disciplina:** Sistemas de Suporte à Decisão (SSD)  
**Ano/Semestre:** 2025/2  
**Orientador:** Prof. Dr. Andre Luiz Marques Serrano



