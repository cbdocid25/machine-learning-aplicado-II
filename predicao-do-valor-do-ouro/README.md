# Predição do Valor do Ouro

## Descrição

Projeto de predição de preços do ouro (Gold Futures - GC=F) utilizando séries temporais com validação cruzada específica para dados temporais. Implementação de AdaBoost Regressor com TimeSeriesSplit considerando gap de 48 horas para prevenção de data leakage.

## Objetivo

Prever o preço futuro do ouro usando técnicas avançadas de séries temporais e machine learning, com validação temporal adequada que simula cenários reais de trading.

## Dataset

**Dados Históricos - Ouro Futuros (GC=F)**
- Fonte: Arquivo CSV "Dados Históricos - Ouro Futuros.csv"
- Período: 01/01/2025 a 31/10/2025
- Formato: CSV com formatação brasileira (. = milhares, , = decimal)
- Características:
  - Preços: Abertura, Máxima, Mínima, Fechamento
  - Volume de negociação
  - Variação percentual

## Metodologia

### 1. Pré-processamento de Dados

- **Carregamento**: Leitura de CSV com formato brasileiro
- **Limpeza**: 
  - Remoção de separadores de milhares
  - Conversão de vírgulas decimais para pontos
  - Conversão de volume (K, M, B → valores numéricos)
- **Estruturação**: MultiIndex compatível com formato de séries temporais

### 2. Engenharia de Features

**60+ features criadas:**

#### Features de Lag (8 períodos)
- Lags: 1, 2, 3, 5, 7, 10, 14, 21 dias
- Capturam dependências temporais

#### Features de Rolling Window (7 janelas)
- Médias móveis: 3, 5, 7, 10, 14, 21, 30 dias
- Desvio padrão, mínimo e máximo para cada janela
- Suavizam ruído e identificam tendências

#### Features de Momentum (4 períodos)
- Períodos: 3, 5, 7, 14 dias
- Capturam força e direção da tendência

#### Features de Volatilidade (3 janelas)
- Janelas: 5, 10, 20 dias
- Medem instabilidade do mercado

#### Indicadores Técnicos
- **RSI (Relative Strength Index)**: períodos 7 e 14
- **Daily Return**: variação percentual diária
- **High-Low %**: amplitude intraday
- **Close-Open %**: direção do movimento

#### Features Temporais
- Dia da semana
- Dia do mês
- Mês
- Trimestre

### 3. Validação Temporal

**TimeSeriesSplit com Gap de 48h**
- **Configuração**: 5-fold cross-validation
- **Gap**: 2 dias úteis (~48 horas)
- **Objetivo**: Prevenir data leakage e simular cenário real
- **Vantagem**: Não permite acesso a dados futuros próximos

```
Fold 1: |████████████ TREINO ████████|⚪⚪GAP⚪⚪|████ TESTE ████|
Fold 2: |████████████████ TREINO ████████████████|⚪⚪GAP⚪⚪|████ TESTE ████|
Fold 3: |████████████████████ TREINO ████████████████████|⚪⚪GAP⚪⚪|████ TESTE ████|
...
```

### 4. Modelo: AdaBoost Regressor

**Configuração:**
- **Estimador base**: DecisionTreeRegressor (max_depth=4)
- **N_estimators**: 100
- **Learning rate**: 0.1
- **Random state**: 42

**Normalização:**
- StandardScaler aplicado às features

### 5. Métricas de Avaliação

- **RMSE (Root Mean Squared Error)**: Erro quadrático médio em USD
- **MAE (Mean Absolute Error)**: Erro absoluto médio em USD
- **R² Score**: Coeficiente de determinação

## Resultados

### Validação Cruzada (5-CV com Gap de 48h)

Os resultados são apresentados por fold, mostrando métricas para treino e teste:

- **RMSE Médio**: Erro típico das previsões em dólares
- **MAE Médio**: Erro médio absoluto das previsões
- **R² Médio**: Qualidade do ajuste do modelo

### Análise por Fold

- Melhor e pior fold identificados
- Variação de R² entre folds
- Análise de consistência temporal

### Visualizações Incluídas

1. **Série Temporal**: Evolução do preço do ouro
2. **Volume de Negociação**: Atividade do mercado
3. **TimeSeriesSplit**: Visualização dos folds
4. **Métricas por Fold**: R², RMSE, MAE
5. **Real vs Previsto**: Comparação visual
6. **Scatter Plot**: Correlação previsões/valores reais
7. **Análise de Resíduos**: Distribuição e padrões de erro

## Insights e Descobertas

### 1. TimeSeriesSplit com Gap de 48h
- Essencial para validação realista
- Previne data leakage temporal
- Simula cenário real de trading

### 2. Importância das Features
- Lags capturam tendências de curto prazo
- Médias móveis suavizam volatilidade
- RSI identifica pontos de reversão
- Features temporais capturam sazonalidade

### 3. Desempenho do AdaBoost
- Capacidade de capturar padrões complexos
- Adaptação a diferentes regimes de volatilidade
- Robustez em dados de séries temporais financeiras

## Limitações

- Não captura eventos de cisne negro
- Alta volatilidade pode aumentar erro
- Necessita retreinamento periódico
- Não considera fatores fundamentalistas

## Recomendações

### Para Trading/Investimento
1. Usar previsões como ferramenta complementar
2. Monitorar resíduos para mudanças de regime
3. Retreinar periodicamente
4. Considerar fatores macroeconômicos externos

### Para Melhorias do Modelo
1. Incluir features macroeconômicas (dólar, inflação, juros)
2. Adicionar mais indicadores técnicos (MACD, Bandas de Bollinger)
3. Testar diferentes gaps (24h, 72h)
4. Experimentar ensemble de múltiplos modelos
5. Incorporar análise de sentimento de notícias

## Tecnologias Utilizadas

- **Python 3.x**
- **pandas**: Manipulação de dados temporais
- **numpy**: Operações numéricas
- **scikit-learn**: 
  - AdaBoostRegressor
  - TimeSeriesSplit
  - StandardScaler
  - Métricas de avaliação
- **matplotlib**: Visualizações

## Estrutura do Notebook

1. Importação de bibliotecas
2. Carregamento de dados (CSV)
3. Análise exploratória dos dados
4. Engenharia de features para séries temporais
5. Preparação dos dados para modelagem
6. Configuração do TimeSeriesSplit com gap de 48h
7. Treinamento com AdaBoost Regressor
8. Validação cruzada com TimeSeriesSplit
9. Análise detalhada por fold
10. Modelo final e análise de previsões
11. Conclusões e insights

## Como Executar

1. Clone o repositório:
```bash
git clone https://github.com/cbdocid25/machine-learning-aplicado-II.git
```

2. Navegue até o diretório:
```bash
cd machine-learning-aplicado-II/predicao-do-valor-do-ouro
```

3. Instale as dependências:
```bash
pip install pandas numpy scikit-learn matplotlib yfinance
```

4. Execute o notebook:
```bash
jupyter notebook predicao-do-ouro.ipynb
```

## Arquivos

- `predicao-do-ouro.ipynb`: Notebook principal com análise completa
- `Dados Históricos - Ouro Futuros.csv`: Dataset de preços do ouro

## Referências

- [Scikit-learn TimeSeriesSplit](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.TimeSeriesSplit.html)
- [AdaBoost Regressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.AdaBoostRegressor.html)
- [Pandas Documentation](https://pandas.pydata.org/)

## Autor

**cbdocid25**

## Instituição

Universidade do Estado do Amazonas (UEA)  
Pós-Graduação em Ciências de Dados  
Disciplina: Machine Learning Aplicado II  
Ano: 2025
