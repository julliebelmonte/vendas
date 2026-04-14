# 📦 Case XVendas — Análise de Rentabilidade

> **Pergunta de negócio:** *"No último ano, o XVendas apresentou perda gradual na rentabilidade. O volume de vendas permaneceu estável. O que pode ser a causa?"*

---

## 🗂️ Estrutura do Projeto

```
├── Case_Vendas.xlsx   # Dataset original
└── vendas.ipynb       # Notebook com análise completa
```

---

## 📊 Sobre o Dataset

| Atributo | Valor |
|---|---|
| Linhas | 3.521 |
| Período | 9 meses |
| Categorias de produto | 415 |
| Variáveis de custo | Entrega, Produto, Marketing |

Não há valores nulos. Os dados estão organizados no nível de **categoria × mês**, com os três custos associados a cada combinação.

---

## 🧠 Lógica da Análise

A análise foi estruturada em 4 etapas:

### 1. Análise Exploratória (EDA)
Validação da estrutura do dataset: tipos de dados, valores nulos, distribuição estatística e amplitude das variáveis. O alto desvio padrão em relação à média em todos os custos indica grande variabilidade entre categorias — esperado dado a diversidade de produtos (de calculadoras a eletrodomésticos).

### 2. Análise de Tendência Mensal
Agregação dos custos por mês para identificar evolução temporal. Resultado:

- **Custo de Entrega:** crescimento de ~247% do mês 1 ao mês 9
- **Custo de Produto:** estável ao longo do período
- **Custo de Marketing:** leve queda

**Conclusão:** com volume de vendas estável, o aumento expressivo no custo de entrega é o principal driver da queda de rentabilidade.

### 3. Correlação e Aprofundamento por Categoria
Análise de correlação entre os três custos revelou relação moderada entre custo de entrega e custo de produto (r = 0.4). Categorias de maior volumetria física (eletrodomésticos, móveis, TVs) concentram os maiores custos de entrega, sugerindo que o preço do frete está atrelado ao tamanho/peso dos produtos.

### 4. Modelagem 
Construção de modelo para prever o custo de entrega por categoria e mês — útil para simulação de cenários e planejamento logístico.

---

## ⚙️ Tecnologias Utilizadas

| Biblioteca | Uso |
|---|---|
| `pandas` | Manipulação e agregação dos dados |
| `matplotlib` / `seaborn` | Visualização de tendências e correlações |
| `scikit-learn` | Modelagem preditiva, cross-validation e métricas |
| `numpy` | Cálculos numéricos auxiliares |

---

## 🤖 Modelagem — Comparação de Modelos

Foram testados três modelos usando **cross-validation com 5 folds** (métrica: MAE):

| Modelo | MAE Médio |
|---|---|
| Linear Regression (baseline) | R$ 522.264 |
| Random Forest | R$ 292.606 |
| **Gradient Boosting** ✅ | **R$ 286.745** |

O **Gradient Boosting** foi o modelo vencedor por menor erro médio absoluto.

### Avaliação Final (split 80/20)

| Métrica | Valor |
|---|---|
| MAE | R$ 177.515 |
| RMSE | R$ 694.796 |
| R² | 0.40 |

O R² de 0.40 indica que o modelo explica 40% da variância do custo de entrega com apenas 4 features. O gap entre MAE e RMSE revela que os maiores erros concentram-se nas categorias de alto custo (cauda longa da distribuição).

### Importância das Features

| Feature | Importância |
|---|---|
| Custo dos Produtos | 54% |
| Custo de Marketing | 29% |
| Categoria | 16% |
| Mês | 1% |

O custo de produto é o maior preditor do custo de entrega — quanto mais caro o produto, mais caro o frete.

---

## 🔍 Limitações do Modelo

O modelo poderia ser enriquecido com:
- **Peso e volume** dos produtos por categoria
- **CEP de destino** (distância de entrega)
- **Transportadora utilizada**
- **Período maior** que 9 meses para capturar sazonalidade


