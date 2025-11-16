# Atividade 1: Classificação com Naive Bayes

## Descrição

Implementação e comparação de três variantes do classificador Naive Bayes aplicados ao dataset Congressional Voting Records. O objetivo é analisar o comportamento de diferentes algoritmos Naive Bayes em dados categóricos binários e demonstrar a importância da escolha do algoritmo adequado ao tipo de dados.

## Objetivo

Comparar o desempenho de três variantes do Naive Bayes (BernoulliNB, GaussianNB e MultinomialNB) na classificação de partidos políticos baseando-se em padrões de votação do Congresso dos EUA em 1984.

## Dataset

**Congressional Voting Records (1984)**
- **Fonte**: UCI Machine Learning Repository
- **URL**: https://archive.ics.uci.edu/static/public/105/data.csv
- **Características**:
  - 435 instâncias (após limpeza)
  - 17 atributos (16 features + 1 target)
  - **Target**: Partido político (Democrat ou Republican)
  - **Features**: Votos em 16 questões políticas (yes/no)
  - Valores ausentes representados por '?'

### Questões Políticas Analisadas

1. Handicapped infants
2. Water project cost sharing
3. Adoption of the budget resolution
4. Physician fee freeze
5. El Salvador aid
6. Religious groups in schools
7. Anti-satellite test ban
8. Aid to Nicaraguan contras
9. MX missile
10. Immigration
11. Synfuels corporation cutback
12. Education spending
13. Superfund right to sue
14. Crime
15. Duty-free exports
16. Export administration act South Africa

## Metodologia

### 1. Pré-processamento

#### Conversão de Dados
- **Votos**: 'y' → 1, 'n' → 0
- **Partido**: 'democrat' → 0, 'republican' → 1

#### Limpeza de Dados
- Remoção de instâncias com target ausente
- Tratamento adequado de valores ausentes nas features

#### Divisão dos Dados
- **Treino**: 70% (304 instâncias)
- **Teste**: 30% (131 instâncias)
- **Random state**: 42 (para reprodutibilidade)

#### Imputação de Valores Ausentes
- Estratégia: `most_frequent`
- Aplicação: Apenas no conjunto de treino
- **Importante**: Imputação realizada APÓS a divisão treino/teste para evitar data leakage

### 2. Modelos Avaliados

#### 🏆 BernoulliNB
- **Descrição**: Projetado especificamente para features binárias ou booleanas
- **Adequação**: IDEAL para o dataset (votos sim/não)
- **Vantagem**: Modela explicitamente a presença/ausência de features binárias

#### GaussianNB
- **Descrição**: Assume distribuição gaussiana (normal) das features
- **Adequação**: INADEQUADO para dados binários discretos
- **Limitação**: Distribuição normal não é apropriada para dados binários

#### MultinomialNB
- **Descrição**: Projetado para contagens discretas (ex: frequência de palavras)
- **Adequação**: NÃO-IDEAL para dados binários simples
- **Limitação**: Melhor para dados de contagem com múltiplos valores possíveis

## Resultados

### Métricas de Performance

| Modelo | Acurácia | Precisão (macro) | Recall (macro) | F1-Score (macro) | Adequação |
|--------|----------|------------------|----------------|------------------|-----------|
| **BernoulliNB** | **94.62%** | **0.95** | **0.93** | **0.94** | ✅ Apropriado |
| GaussianNB | 93.85% | 0.94 | 0.92 | 0.93 | ❌ Inadequado |
| MultinomialNB | 92.31% | 0.93 | 0.91 | 0.92 | ⚠️ Não-ideal |

### Análise Detalhada - BernoulliNB (Melhor Modelo)

```
              precision    recall  f1-score   support

    Democrat       0.94      0.98      0.96        82
  Republican       0.96      0.89      0.92        48

    accuracy                           0.95       130
   macro avg       0.95      0.93      0.94       130
weighted avg       0.95      0.95      0.95       130
```

#### Matriz de Confusão - BernoulliNB

|                | Predito: Democrat | Predito: Republican |
|----------------|-------------------|---------------------|
| **Real: Democrat** | 80 (VP) | 2 (FN) |
| **Real: Republican** | 5 (FP) | 43 (VN) |

- **VP (Verdadeiros Positivos)**: 80 democratas corretamente classificados
- **VN (Verdadeiros Negativos)**: 43 republicanos corretamente classificados
- **FP (Falsos Positivos)**: 5 republicanos classificados como democratas
- **FN (Falsos Negativos)**: 2 democratas classificados como republicanos

### Visualizações Incluídas

1. **Gráfico Comparativo de Acurácia**: Comparação visual entre os três modelos
2. **Matriz de Confusão**: Análise detalhada dos erros de classificação
3. **Relatório de Classificação**: Métricas completas por classe

## Insights e Descobertas

### 1. Importância da Escolha do Algoritmo
- **BernoulliNB superou os demais** em 2.31% de acurácia comparado ao MultinomialNB
- A diferença de performance ilustra a importância de escolher o algoritmo adequado ao tipo de dados
- Algoritmos inadequados (GaussianNB, MultinomialNB) ainda apresentam resultados razoáveis, mas subótimos

### 2. Características dos Dados
- Dados binários de votação são naturalmente adequados para BernoulliNB
- Padrões de votação são consistentes dentro de cada partido
- Alta correlação entre votos específicos e filiação partidária

### 3. Performance por Classe
- **Democrats**: 98% de recall (excelente detecção)
- **Republicans**: 96% de precision (baixo erro de falsos positivos)
- Modelo ligeiramente melhor em identificar democratas

### 4. Tratamento de Valores Ausentes
- Estratégia `most_frequent` efetiva para dados binários
- Imputação após divisão treino/teste evita data leakage
- Valores ausentes não prejudicaram significativamente a performance

## Limitações e Considerações

### Limitações do Dataset
- Dataset histórico (1984) pode não refletir padrões atuais
- Número limitado de instâncias (435)
- Apenas duas classes (sistema bipartidário)

### Limitações do Modelo
- Naive Bayes assume independência entre features (nem sempre verdadeiro)
- Padrões de votação podem ter dependências não capturadas
- Modelo simples pode não capturar relações complexas

### Considerações Práticas
- Alta acurácia não garante generalização para novos contextos políticos
- Modelo treinado em dados históricos específicos
- Requer retreinamento com dados atuais para aplicação prática

## Tecnologias Utilizadas

- **Python 3.x**
- **pandas**: Manipulação e análise de dados
- **numpy**: Operações numéricas
- **scikit-learn**: 
  - `BernoulliNB`, `GaussianNB`, `MultinomialNB`
  - `train_test_split`
  - `SimpleImputer`
  - Métricas de avaliação
- **matplotlib**: Visualizações
- **seaborn**: Gráficos estatísticos avançados

## Estrutura do Notebook

1. **Importação de Bibliotecas**
2. **Carregamento de Dados**
   - Download do UCI Repository
   - Inspeção inicial
3. **Preparação dos Dados**
   - Conversão de categorias para numéricos
   - Limpeza de valores ausentes no target
4. **Análise Exploratória**
   - Estatísticas descritivas
   - Distribuição de classes
5. **Divisão Treino/Teste**
   - 70/30 split com random_state=42
6. **Tratamento de Valores Ausentes**
   - SimpleImputer com estratégia 'most_frequent'
7. **Treinamento do Modelo BernoulliNB**
   - Fit e predict
   - Avaliação de performance
8. **Comparativo com Outros Modelos**
   - GaussianNB
   - MultinomialNB
9. **Visualização de Resultados**
   - Matriz de confusão
   - Gráfico comparativo
   - Relatório de classificação

## Como Executar

1. Clone o repositório:
```bash
git clone https://github.com/cbdocid25/machine-learning-aplicado-II.git
```

2. Navegue até o diretório:
```bash
cd machine-learning-aplicado-II/Atividade_1_exemplo_nb
```

3. Instale as dependências:
```bash
pip install pandas numpy scikit-learn matplotlib seaborn
```

4. Execute o notebook:
```bash
jupyter notebook atividade_1_exemplo_nb.ipynb
```

## Arquivos

- `atividade_1_exemplo_nb.ipynb`: Notebook principal com análise completa
- `comparativo_modelos_nb.png`: Gráfico comparativo de acurácia dos modelos
- `README.md`: Esta documentação

## Conclusões

### Principais Aprendizados

1. **BernoulliNB é superior para dados binários**: Confirma teoricamente e empiricamente
2. **Escolha do algoritmo importa**: 2.31% de diferença em acurácia
3. **Tratamento adequado de dados é crucial**: Evitar data leakage na imputação
4. **Naive Bayes é eficiente**: Simplicidade com boa performance

### Recomendações

**Para Classificação de Dados Binários:**
- Sempre preferir BernoulliNB
- Considerar outros algoritmos apenas se necessário
- Validar adequação do modelo ao tipo de dado

**Para Trabalhos Futuros:**
- Testar outros algoritmos (Random Forest, SVM, Logistic Regression)
- Análise de features importantes
- Cross-validation para robustez
- Aplicação em datasets políticos mais recentes

## Referências

- [UCI Machine Learning Repository - Voting Records](https://archive.ics.uci.edu/dataset/105/congressional+voting+records)
- [Scikit-learn Naive Bayes](https://scikit-learn.org/stable/modules/naive_bayes.html)
- [BernoulliNB Documentation](https://scikit-learn.org/stable/modules/generated/sklearn.naive_bayes.BernoulliNB.html)

## Autor

**cbdocid25**

## Instituição

Universidade do Estado do Amazonas (UEA)  
Pós-Graduação em Ciências de Dados  
Disciplina: Machine Learning Aplicado II  
Ano: 2025
