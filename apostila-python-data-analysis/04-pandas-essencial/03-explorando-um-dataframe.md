# Explorando um DataFrame

> Módulo 4 — Pandas Essencial · Tópico 3 de 12

## O que é e por que importa

Antes de filtrar, transformar ou calcular qualquer coisa, o primeiro passo
com qualquer dataset novo é **olhar para ele**: quantas linhas e colunas tem,
que tipo de dado cada coluna guarda, se há valores faltando, quais são os
valores típicos. Pandas tem um punhado de métodos feitos exatamente para essa
"primeira olhada" — usá-los sempre no início evita surpresas mais tarde (como
descobrir no meio de uma análise que uma coluna que parecia numérica na
verdade é texto).

## Como funciona (com exemplo comentado)

```python
import pandas as pd
from io import StringIO

csv_texto = """produto,categoria,quantidade,preco_unitario,em_estoque
Caneta Azul,Papelaria,3,2.50,True
Caderno,Papelaria,1,15.90,True
Mochila,Acessorios,2,89.90,False
Lapis HB,Papelaria,5,1.20,True
Estojo,Acessorios,,25.00,True
"""
df = pd.read_csv(StringIO(csv_texto))

# .head(n) -- primeiras n linhas (padrão 5) -- a primeira coisa a rodar sempre
print(df.head(3))

# .tail(n) -- últimas n linhas
print(df.tail(2))

# .shape -- (linhas, colunas), igual ao shape de arrays NumPy (Módulo 3)
print(df.shape)  # (5, 5)

# .info() -- resumo: tipos de cada coluna, quantos valores não-nulos, uso de memória
df.info()
# <class 'pandas.core.frame.DataFrame'>
# RangeIndex: 5 entries, 0 to 4
# Data columns (total 5 columns):
#  #   Column          Non-Null Count  Dtype
# ---  ------          --------------  -----
#  0   produto         5 non-null      object
#  1   categoria       5 non-null      object
#  2   quantidade      4 non-null      float64   <- repare: 4, não 5! tem um valor faltando
#  3   preco_unitario  5 non-null      float64
#  4   em_estoque      5 non-null      bool
# -- .info() já é uma forma rápida de detectar valores ausentes (mais sobre isso no Tópico 11)

# .describe() -- estatísticas resumidas das colunas numéricas
print(df.describe())
#        quantidade  preco_unitario
# count    4.000000        5.000000
# mean     2.750000       26.900000
# std      1.707825       35.499...
# min      1.000000        1.200000
# 25%      1.750000        2.500000
# 50%      2.500000       15.900000
# 75%      3.500000       40.225000
# max      5.000000       89.900000
# -- é o mesmo tipo de agregação vista no Módulo 3 (mean, min, max, std), só que
#    o Pandas já calcula tudo de uma vez e organiza numa tabela

# .describe(include="object") -- estatísticas para colunas de texto
print(df.describe(include="object"))
#        produto  categoria
# count        5          5
# unique       5          2
# top     Caneta Azul  Papelaria
# freq         1          3

# .dtypes -- tipo de cada coluna
print(df.dtypes)

# .columns e .index -- nomes das colunas e do índice
print(df.columns.tolist())  # ['produto', 'categoria', 'quantidade', 'preco_unitario', 'em_estoque']

# .value_counts() -- conta quantas vezes cada valor aparece numa coluna (Series, não DataFrame)
print(df["categoria"].value_counts())
# Papelaria     3
# Acessorios    2
# Name: count, dtype: int64

# .nunique() -- quantos valores ÚNICOS existem numa coluna
print(df["categoria"].nunique())  # 2

# .isnull().sum() -- conta valores ausentes por coluna (mais detalhes no Tópico 11)
print(df.isnull().sum())
# produto           0
# categoria         0
# quantidade        1
# preco_unitario    0
# em_estoque        0
```

## Erros comuns de quem está começando

- Pular direto para filtros e cálculos sem antes rodar `.head()`, `.info()` e
  `.describe()` — isso costuma resultar em descobrir tarde demais que uma
  coluna tem valores ausentes, tipos errados, ou nomes de coluna diferentes
  do esperado.
- Confundir `.describe()` (estatísticas resumidas) com `.info()` (tipos e
  contagem de não-nulos) — são complementares, não a mesma coisa: `.info()`
  responde "o que tem aqui e está tudo preenchido?", `.describe()` responde
  "como esses números se distribuem?".
- Esquecer que `.describe()` por padrão só olha colunas numéricas — colunas
  de texto ficam de fora a menos que você passe `include="object"` (ou
  `include="all"` para ver tudo junto).

## Exercício prático

Usando o `df` do exemplo acima (produtos da loja):

1. Rode `.info()` e identifique qual coluna tem valores ausentes e quantos.
2. Rode `.describe()` e identifique qual produto tem o maior preço unitário
   olhando o valor de `max`.
3. Use `.value_counts()` para descobrir quantos produtos existem em cada
   categoria.
4. Use `.nunique()` para descobrir quantas categorias distintas existem.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd
from io import StringIO

csv_texto = """produto,categoria,quantidade,preco_unitario,em_estoque
Caneta Azul,Papelaria,3,2.50,True
Caderno,Papelaria,1,15.90,True
Mochila,Acessorios,2,89.90,False
Lapis HB,Papelaria,5,1.20,True
Estojo,Acessorios,,25.00,True
"""
df = pd.read_csv(StringIO(csv_texto))

df.info()
# "quantidade" tem 1 valor ausente (4 non-null de 5 linhas)

print(df.describe())
# max de preco_unitario é 89.90 -> olhando o df, é a Mochila

print(df["categoria"].value_counts())
# Papelaria: 3, Acessorios: 2

print(df["categoria"].nunique())  # 2
```

</details>

## Checklist antes de avançar

- [ ] Sempre rodo `.head()`, `.info()` e `.describe()` ao carregar um dataset novo
- [ ] Sei ler a saída de `.info()` para identificar tipos e valores ausentes
- [ ] Sei usar `.value_counts()` e `.nunique()` para explorar colunas categóricas
- [ ] Resolvi o exercício sem olhar a solução
