# Introdução ao Seaborn

> Módulo 7 — Visualização · Tópico 6 de 7

## O que é e por que importa

Seaborn é uma biblioteca construída **em cima do Matplotlib**, focada em
gráficos estatísticos: ela sabe trabalhar diretamente com DataFrames do
Pandas (sem precisar extrair colunas manualmente), calcula automaticamente
agregações comuns (como médias com intervalo de confiança) e já vem com um
visual mais elegante por padrão. Para boa parte dos gráficos de EDA
(retomando o Módulo 6), Seaborn exige bem menos código que Matplotlib puro.

Instalação (se ainda não tiver):

```bash
pip install seaborn
```

Convenção de importação:

```python
import seaborn as sns
```

## Como funciona (com exemplo comentado)

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

np.random.seed(0)
df = pd.DataFrame({
    "categoria": np.random.choice(["Papelaria", "Eletronicos", "Roupas"], size=200),
    "preco": np.concatenate([
        np.random.normal(15, 5, 70),
        np.random.normal(500, 100, 60),
        np.random.normal(80, 20, 70),
    ]),
    "avaliacao": np.random.uniform(3, 5, 200),
})

# Seaborn aplica um estilo visual mais agradável globalmente
sns.set_theme(style="whitegrid")

# histplot -- histograma, equivalente ao ax.hist do Matplotlib mas mais simples
sns.histplot(data=df, x="preco", bins=30)
plt.title("Distribuição de preços")
plt.show()

# histplot com separação por categoria -- Seaborn cuida das cores automaticamente
sns.histplot(data=df, x="preco", hue="categoria", bins=30)
plt.title("Distribuição de preços por categoria")
plt.show()

# boxplot -- muito mais direto que no Matplotlib puro (Tópico 3)
sns.boxplot(data=df, x="categoria", y="preco")
plt.title("Preço por categoria")
plt.show()

# scatterplot -- equivalente ao ax.scatter, mas aceita "hue" (cor por categoria)
# e "size" (tamanho por variável numérica) direto como parâmetros
sns.scatterplot(data=df, x="preco", y="avaliacao", hue="categoria", alpha=0.6)
plt.title("Preço x Avaliação")
plt.show()

# barplot -- desenha barras com a MÉDIA de uma coluna por categoria automaticamente
# (não precisa fazer groupby manualmente, embora ainda seja útil saber fazer)
sns.barplot(data=df, x="categoria", y="preco", errorbar="sd")
# errorbar="sd" mostra o desvio padrão como barra de erro em cada barra --
# uma forma visual de já trazer a dispersão (Módulo 6, Tópico 2) junto com a média
plt.title("Preço médio por categoria (com desvio padrão)")
plt.show()

# heatmap -- ótimo para visualizar matrizes de correlação (Módulo 6, Tópico 4)
df_numerico = pd.DataFrame({
    "preco": df["preco"],
    "avaliacao": df["avaliacao"],
    "vendas": np.random.uniform(10, 500, 200),
})
matriz_correlacao = df_numerico.corr()

sns.heatmap(matriz_correlacao, annot=True, cmap="coolwarm", vmin=-1, vmax=1)
# annot=True escreve o valor numérico em cada célula
plt.title("Matriz de correlação")
plt.show()

# pairplot -- gera uma grade de scatter plots entre TODAS as colunas numéricas
# de uma vez, ótimo para uma primeira olhada exploratória (Módulo 6, Tópico 8)
sns.pairplot(df_numerico)
plt.show()
```

## Erros comuns de quem está começando

- Continuar extraindo colunas manualmente (`df["coluna"].values`) como se
  estivesse usando Matplotlib puro, em vez de aproveitar que a maioria das
  funções do Seaborn aceita `data=df, x="coluna", y="outra_coluna"`
  diretamente — isso é justamente o que torna o Seaborn mais rápido de usar
  com dados tabulares.
- Usar `sns.barplot()` esperando que ele desenhe a **soma** dos valores
  (como um `groupby().sum()` faria), quando na verdade o padrão do Seaborn
  é calcular a **média** — se a soma for o que interessa, é mais seguro
  calcular com `groupby` (Módulo 4, Tópico 8) e desenhar o resultado.
- Rodar `sns.pairplot()` em datasets com muitas colunas numéricas (10+) sem
  perceber que o número de gráficos gerados cresce ao quadrado — o gráfico
  fica lento de gerar e difícil de ler; nesses casos, vale selecionar um
  subconjunto de colunas antes.

## Exercício prático

```python
import numpy as np
np.random.seed(2)
df = pd.DataFrame({
    "regiao": np.random.choice(["Norte", "Sul", "Sudeste"], size=150),
    "temperatura": np.random.normal(25, 5, 150),
    "vendas_sorvete": np.random.uniform(50, 500, 150),
})
```

1. Crie um histograma de `temperatura` separado por `regiao` (use `hue`).
2. Crie um boxplot de `temperatura` por `regiao`.
3. Crie um scatterplot de `temperatura` (x) por `vendas_sorvete` (y),
   colorido por `regiao`.
4. Crie um heatmap da matriz de correlação entre `temperatura` e
   `vendas_sorvete`.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

np.random.seed(2)
df = pd.DataFrame({
    "regiao": np.random.choice(["Norte", "Sul", "Sudeste"], size=150),
    "temperatura": np.random.normal(25, 5, 150),
    "vendas_sorvete": np.random.uniform(50, 500, 150),
})

sns.histplot(data=df, x="temperatura", hue="regiao", bins=20)
plt.show()

sns.boxplot(data=df, x="regiao", y="temperatura")
plt.show()

sns.scatterplot(data=df, x="temperatura", y="vendas_sorvete", hue="regiao", alpha=0.6)
plt.show()

matriz = df[["temperatura", "vendas_sorvete"]].corr()
sns.heatmap(matriz, annot=True, cmap="coolwarm", vmin=-1, vmax=1)
plt.show()
```

</details>

## Checklist antes de avançar

- [ ] Sei usar `data=df, x=..., y=...` diretamente com funções do Seaborn
- [ ] Sei usar `hue` para separar categorias por cor automaticamente
- [ ] Sei criar histplot, boxplot, scatterplot, barplot e heatmap
- [ ] Sei quando `pairplot` é útil e quando evitar (muitas colunas)
- [ ] Resolvi o exercício sem olhar a solução
