# Machine Learning Aplicado II

Repositório contendo atividades práticas da disciplina de Machine Learning Aplicado II, ministrada pela Universidade do Estado do Amazonas (UEA) em 2025.

## Estrutura do Repositório

```
machine-learning-aplicado-II/
├── Atividade_1_exemplo_nb/
│   ├── atividade_1_exemplo_nb/
│   │   └── atividade_1_exemplo_nb.ipynb
│   └── README.md
├── classificacao-de-texto/
│   ├── classificacao-de-texto.ipynb
│   └── README.md
├── atividade-de-regressão/
│   ├── atividade_de_regressao.ipynb
│   └── README.md
├── predicao-do-valor-do-ouro/
│   ├── predicao-do-ouro.ipynb
│   ├── Dados Históricos - Ouro Futuros.csv
│   └── README.md
└── README.md
```

## Projetos

### 1. [Atividade 1: Classificação com Naive Bayes](./Atividade_1_exemplo_nb/)
Implementação e comparação de três variantes do classificador Naive Bayes aplicados ao dataset Congressional Voting Records.

### 2. [Classificação de Texto](./classificacao-de-texto/)
Projeto de classificação de textos utilizando técnicas de NLP e machine learning.

### 3. [Atividade de Regressão](./atividade-de-regressão/)
Análise preditiva de tráfego de bicicletas com features de impacto da pandemia.

### 4. [Predição do Valor do Ouro](./predicao-do-valor-do-ouro/)
Predição de preços do ouro usando séries temporais com TimeSeriesSplit e AdaBoost Regressor.

---

## Atividade 1: Classificação com Naive Bayes

### Descrição

Implementação e comparação de três variantes do classificador Naive Bayes aplicados ao dataset Congressional Voting Records. O objetivo é analisar o comportamento de diferentes algoritmos Naive Bayes em dados categóricos binários.

### Dataset

**Congressional Voting Records (1984)**
- Fonte: UCI Machine Learning Repository
- URL: https://archive.ics.uci.edu/static/public/105/data.csv
- Características:
  - 435 instâncias (após limpeza)
  - 17 atributos (16 features + 1 target)
  - Target: Partido político (Democrat ou Republican)
  - Features: Votos em 16 questões políticas (y/n)
  - Valores ausentes representados por '?'

### Metodologia

#### Pré-processamento
1. Conversão de valores categóricos para numéricos:
   - Votos: 'y' → 1, 'n' → 0
   - Partido: 'democrat' → 0, 'republican' → 1
2. Remoção de instâncias com target ausente
3. Divisão treino/teste: 70%/30% (random_state=42)
4. Imputação de valores ausentes usando estratégia 'most_frequent'

#### Modelos Avaliados

**BernoulliNB**
- Apropriado para features binárias ou booleanas
- Ideal para o dataset em questão

**GaussianNB**
- Assume distribuição gaussiana (normal) das features
- Inadequado para dados binários discretos

**MultinomialNB**
- Projetado para contagens discretas
- Subótimo para dados binários simples

### Resultados

#### Métricas de Performance

| Modelo | Acurácia | Adequação ao Dataset |
|--------|----------|---------------------|
| BernoulliNB | 94.62% | Apropriado |
| GaussianNB | 93.85% | Inadequado |
| MultinomialNB | 92.31% | Não-ideal |

#### Análise

O BernoulliNB apresentou o melhor desempenho, confirmando sua adequação para dados binários. As diferenças de performance ilustram a importância da escolha do algoritmo adequado ao tipo de dados.

**Relatório Detalhado - BernoulliNB:**
```
              precision    recall  f1-score   support

    Democrat       0.94      0.98      0.96        82
  Republican       0.96      0.89      0.92        48

    accuracy                           0.95       130
   macro avg       0.95      0.93      0.94       130
weighted avg       0.95      0.95      0.95       130
```

### Tecnologias Utilizadas

- Python 3.x
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn

### Estrutura do Notebook

1. Importação de bibliotecas
2. Carregamento e preparação dos dados
3. Análise exploratória
4. Divisão treino/teste
5. Tratamento de valores ausentes
6. Treinamento do modelo BernoulliNB
7. Comparativo com GaussianNB e MultinomialNB
8. Visualização dos resultados

### Como Executar

1. Clone o repositório:
```bash
git clone https://github.com/cbdocid25/machine-learning-aplicado-II.git
```

2. Navegue até o diretório da atividade:
```bash
cd machine-learning-aplicado-II/atividade_1_exemplo_nb
```

3. Instale as dependências:
```bash
pip install pandas numpy scikit-learn matplotlib seaborn
```

4. Execute o notebook:
```bash
jupyter notebook atividade_1_exemplo_nb.ipynb
```

### Observações

- O notebook inclui tratamento adequado de dados ausentes sem vazamento de informação (data leakage)
- A imputação é realizada exclusivamente com base nos dados de treino
- Matriz de confusão e relatório de classificação completos estão disponíveis no notebook

## Autor

**cbdocid25**

## Instituição

Universidade do Estado do Amazonas (UEA)  
Pós-Graduação em Ciências de Dados  
Disciplina: Machine Learning Aplicado II  
Ano: 2025
