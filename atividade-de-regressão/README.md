# Atividade de Regressão

## Descrição

Projeto de análise preditiva de tráfego de bicicletas utilizando modelos de regressão, com features especiais para capturar o impacto da pandemia de COVID-19.

## Objetivo

Prever o volume de tráfego de bicicletas considerando variáveis temporais, meteorológicas e o contexto pandêmico, explorando diferentes algoritmos de regressão.

## Dataset

Dados de tráfego de bicicletas com as seguintes características:
- Variáveis temporais (data, hora, dia da semana)
- Variáveis meteorológicas (temperatura, precipitação, etc.)
- Feature de pandemia (impacto do COVID-19 no comportamento de mobilidade)
- Volume de tráfego (variável target)

## Metodologia

### 1. Pré-processamento
- Tratamento de valores ausentes
- Codificação de variáveis categóricas
- Feature engineering temporal
- Normalização/padronização de features

### 2. Feature Engineering
- Extração de features temporais (dia da semana, mês, hora)
- Criação de feature de pandemia (período COVID-19)
- Engenharia de features meteorológicas
- Interações entre variáveis

### 3. Modelagem
Avaliação de diferentes algoritmos de regressão:
- Regressão Linear
- Random Forest Regressor
- Gradient Boosting
- Outros algoritmos ensemble

### 4. Avaliação
Métricas utilizadas:
- **RMSE (Root Mean Squared Error)**
- **MAE (Mean Absolute Error)**
- **R² Score**
- **MAPE (Mean Absolute Percentage Error)**

## Insights

### Impacto da Pandemia
- Análise do comportamento de mobilidade durante a pandemia
- Mudanças nos padrões de uso de bicicletas
- Comparação pré e pós-pandemia

### Fatores Meteorológicos
- Influência da temperatura no tráfego
- Impacto de precipitação
- Sazonalidade

### Padrões Temporais
- Horários de pico
- Diferenças entre dias úteis e finais de semana
- Tendências mensais e anuais

## Tecnologias Utilizadas

- **Python 3.x**
- **pandas**: Manipulação de dados
- **numpy**: Operações numéricas
- **scikit-learn**: Algoritmos de ML
- **matplotlib/seaborn**: Visualizações

## Estrutura do Notebook

1. Importação de bibliotecas
2. Carregamento e exploração dos dados
3. Análise exploratória (EDA)
4. Pré-processamento e feature engineering
5. Divisão treino/teste
6. Treinamento de modelos
7. Avaliação e comparação de modelos
8. Análise de features importantes
9. Visualização de previsões
10. Conclusões

## Como Executar

1. Clone o repositório:
```bash
git clone https://github.com/cbdocid25/machine-learning-aplicado-II.git
```

2. Navegue até o diretório:
```bash
cd machine-learning-aplicado-II/atividade-de-regressão
```

3. Instale as dependências:
```bash
pip install pandas numpy scikit-learn matplotlib seaborn
```

4. Execute o notebook:
```bash
jupyter notebook atividade_de_regressao.ipynb
```

## Arquivos

- `atividade_de_regressao.ipynb`: Notebook principal com análise completa

## Observações

- O notebook inclui análise detalhada do impacto da pandemia no tráfego de bicicletas
- Tratamento adequado de dados temporais sem vazamento de informação
- Comparação entre múltiplos algoritmos de regressão

## Autor

**cbdocid25**

## Instituição

Universidade do Estado do Amazonas (UEA)  
Pós-Graduação em Ciências de Dados  
Disciplina: Machine Learning Aplicado II  
Ano: 2025
