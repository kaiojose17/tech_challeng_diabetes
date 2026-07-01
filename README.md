# Diagnóstico de Diabetes com Machine Learning - Tech Challenge Fase 1

## Descrição do Projeto

Sistema inteligente de suporte ao diagnóstico de diabetes utilizando técnicas de Machine Learning. O projeto implementa um pipeline completo de análise de dados médicos, desde a exploração até a interpretabilidade com SHAP.

**Base de dados**: Diabetes Data Set (Kaggle) - ~731 registros com 8 features médicas
**Algoritmos**: K-Nearest Neighbors (KNN) + Support Vector Machine (SVM)
**Técnicas**: EDA, Normalização, PCA, Análise de Correlação, Permutation Importance

---

## Estrutura de Arquivos

```
TechChallenge1/
├── notebooks/
│   └── 01_diagnostic_model.ipynb         # Notebook principal com 8 fases
├── data/
│   └── diabetes.csv                      # Dataset (baixado automaticamente)
├── results/
│   ├── model_metrics.json                # Métricas dos modelos
│   ├── feature_importance.png            # Gráfico de importância
│   ├── shap_plots.png                    # Visualizações SHAP
│   ├── roc_curves.png                    # Curvas ROC comparativas
│   └── correlation_matrix.png            # Matriz de correlação
├── Dockerfile                            # Containerização
├── requirements.txt                      # Dependências Python
├── README.md                             # Este arquivo
├── TECHNICAL_REPORT.md                   # Relatório técnico completo
└── VIDEO_SCRIPT.txt                      # Roteiro para vídeo (15 min)
```

---

## Instalação

### Opção 1: Ambiente Local

```bash
# Clonar ou navegar para o repositório
cd TechChallenge1

# Criar ambiente virtual
python -m venv venv
source venv/bin/activate  # No Windows: venv\Scripts\activate

# Instalar dependências
pip install -r requirements.txt

# Executar Jupyter
jupyter notebook
```

### Opção 2: Docker

```bash
# Build da imagem
docker build -t tech-challenge-diabetes .

# Executar container
docker run -p 8888:8888 -v $(pwd)/data:/app/data -v $(pwd)/results:/app/results tech-challenge-diabetes
```

---

## Como Usar

### 1. Executar o Notebook Completo

```bash
# No Jupyter, abrir: notebooks/01_diagnostic_model.ipynb
# Executar todas as células sequencialmente

# OU via terminal:
jupyter nbconvert --to notebook --execute --ExecutePreprocessor.timeout=None \
    notebooks/01_diagnostic_model.ipynb
```

### 2. Estrutura do Notebook (8 Fases)

| Fase | Descrição |
|------|-----------|
| **1** | Setup e Carregamento de Dados |
| **2** | Exploração e Validação de Dados (EDA) |
| **3** | Pré-processamento e PCA |
| **4** | Modelagem - K-Nearest Neighbors |
| **5** | Modelagem - Support Vector Machine |
| **6** | Avaliação Comparativa (Test Set) |
| **7** | Interpretação com Permutation Importance |
| **8** | Discussão Crítica e Conclusões |

---

## Requisitos Técnicos

- **Python**: 3.8+
- **Dependências principais**:
  - pandas: manipulação de dados
  - scikit-learn: modelos de ML e métricas
  - matplotlib/seaborn: visualizações
  - shap: explicabilidade
  - kagglehub: download de datasets

---

## Algoritmos Utilizados

### 1. K-Nearest Neighbors (KNN)
- **Tipo**: Aprendizado baseado em instâncias
- **Princípio**: Classifica baseado nos k vizinhos mais próximos
- **Vantagens**: Simples, interpretável, sem treinamento explícito
- **Hiperparâmetro**: k=5 (número de vizinhos)

### 2. Support Vector Machine (SVM)
- **Tipo**: Aprendizado por otimização de margens
- **Princípio**: Encontra hiperplano ótimo que separa classes
- **Vantagens**: Robusto, eficiente em alta dimensionalidade, resistente a outliers
- **Kernel**: RBF (Radial Basis Function) para relações não-lineares

---

## Métricas e Avaliação

### Métricas Utilizadas

- **Accuracy**: Taxa geral de acertos
- **Recall/Sensitivity**: TP / (TP + FN) - **CRÍTICO** para diagnóstico (não perder doentes)
- **Precision**: TP / (TP + FP)
- **F1-Score**: Média harmônica de Precision e Recall
- **Specificity**: TN / (TN + FP)
- **ROC-AUC**: Área sob curva ROC

### Interpretação Clínica

- **Recall ≥ 0.85**: Prioridade máxima (não perder diagnósticos)
- **Precision ≥ 0.75**: Reduzir falsos positivos
- **Modelo como suporte**: O médico sempre tem a palavra final

---

## Resultados Esperados

### EDA
- Distribuição de classes
- Heatmap de correlação
- Box plots de features principais

### Modelos
- ROC curves de ambos modelos
- Confusion matrices
- Comparação de métricas

### Interpretação
- Feature Importance (top 10 features)
- SHAP summary plot
- SHAP dependence plots

---

## Técnicas Aplicadas

✅ **Exploração de Dados**
- Estatísticas descritivas
- Visualização de distribuições
- Análise de correlação (Pearson)

✅ **Pré-processamento**
- Tratamento de valores ausentes
- Normalização (StandardScaler)
- Separação train/validation/test (70/15/15)

✅ **Modelagem**
- 2 algoritmos de classificação
- Treinamento com GridSearchCV (opcional)
- Avaliação em conjunto de teste separado

✅ **Interpretabilidade**
- Permutation Importance (importância por permutação)
- Análise de Concordância entre modelos
- Visualizações comparativas

✅ **Discussão Crítica**
- Viabilidade clínica
- Limitações do modelo
- Recomendações futuras

---

## Validação de Reprodutibilidade

- Random state fixo em todos os modelos (42)
- Seed fixo para numpy
- Separação train/test com stratify
- Pipeline determinístico

---

## Autores

**Desenvolvido para**: FIAP - Tech Challenge Fase 1  
**Instituição**: Pós-Tech em IA  
**Data**: 2026

---

## Licença

Este projeto é fornecido para fins educacionais.

---

## Suporte

Para executar o projeto:
1. Certifique-se de ter Python 3.8+ instalado
2. Instale as dependências: `pip install -r requirements.txt`
3. Execute o Jupyter: `jupyter notebook`
4. Abra `notebooks/01_diagnostic_model.ipynb`

---

## Referências

- Dataset: https://www.kaggle.com/datasets/mathchi/diabetes-data-set/data
- SHAP: https://github.com/slundberg/shap
- Scikit-learn: https://scikit-learn.org/
