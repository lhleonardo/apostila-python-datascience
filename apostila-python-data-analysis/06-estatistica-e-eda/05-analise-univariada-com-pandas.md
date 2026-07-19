# Análise univariada com Pandas

> Módulo 6 — Estatística e EDA · Tópico 5 de 8

## O que é e por que importa

Análise **univariada** examina **uma variável de cada vez**, isoladamente —
é o primeiro passo de qualquer EDA, antes de cruzar variáveis entre si
(Tópico 6). Para cada coluna do dataset, o objetivo é responder: qual é o
tipo dela (numérica ou categórica)? Qual sua distribuição? Tem valores
estranhos? Este tópico junta as ferramentas dos tópicos anteriores (medidas
de tendência central, dispersão, distribuição) num fluxo de trabalho
aplicado, coluna por coluna.

## Como funciona (com exemplo comentado)

```python
import pandas as pd

df = pd.DataFrame({
    "produto": ["Caneta", "Caderno", "Mochila", "Lapis", "Estojo", "Borracha", "Caneta"],
    "categoria": ["Papelaria", "Papelaria", "Acessorios", "Papelaria", "Acessorios", "Papelaria", "Papelaria"],
    "preco": [2.5, 15.9, 89.9, 1.2, 25.0, 0.9, 2.5],
    "quantidade_vendida": [120, 45, 12, 200, 30, 300, 95],
})

# ANÁLISE UNIVARIADA DE UMA COLUNA NUMÉRICA: "preco"
print(df["preco"].describe())
# count, mean, std, min, 25%, 50%, 75%, max -- tudo de uma vez

print("Assimetria (skew):", df["preco"].skew())
print("Valores únicos:", df["preco"].nunique())

# faixas (bins) para "ver" a distribuição sem gráfico ainda
print(pd.cut(df["preco"], bins=4).value_counts().sort_index())

# ANÁLISE UNIVARIADA DE UMA COLUNA CATEGÓRICA: "categoria"
print(df["categoria"].value_counts())         # contagem absoluta
print(df["categoria"].value_counts(normalize=True))  # proporção (0 a 1)
print(df["categoria"].value_counts(normalize=True) * 100)  # em porcentagem

print("Categorias distintas:", df["categoria"].nunique())
print("Categoria mais comum:", df["categoria"].mode()[0])

# Função reutilizável para resumir QUALQUER coluna numérica de uma vez
def resumo_numerico(serie):
    return pd.Series({
        "media": serie.mean(),
        "mediana": serie.median(),
        "desvio_padrao": serie.std(),
        "minimo": serie.min(),
        "maximo": serie.max(),
        "assimetria": serie.skew(),
        "valores_ausentes": serie.isnull().sum(),
    })

print(resumo_numerico(df["preco"]))
print(resumo_numerico(df["quantidade_vendida"]))

# Aplicando a função a todas as colunas numéricas de uma vez com .apply()
# (revisão de Módulo 4, Tópico 6 -- .apply() em colunas de um DataFrame, axis=0 é o padrão)
colunas_numericas = df.select_dtypes(include="number")
print(colunas_numericas.apply(resumo_numerico))

# .select_dtypes() -- útil para separar automaticamente colunas numéricas de categóricas
colunas_categoricas = df.select_dtypes(include="object")
print(colunas_categoricas.columns.tolist())
```

## Erros comuns de quem está começando

- Pular a análise univariada e ir direto para cruzamentos entre variáveis
  (Tópico 6) — sem entender cada coluna isoladamente primeiro, é fácil
  interpretar mal um cruzamento que na verdade reflete um problema simples
  numa única coluna (um outlier, uma categoria mal escrita).
- Tratar uma coluna numérica com poucos valores distintos (como uma nota de
  1 a 5, ou um código de categoria numérico) como se fosse contínua,
  calculando média/desvio padrão quando na verdade ela deveria ser analisada
  como categórica (com `value_counts()`).
- Analisar `value_counts()` de uma coluna categórica sem `normalize=True`
  quando o objetivo é comparar proporções entre datasets de tamanhos
  diferentes — contagens absolutas de datasets de tamanho diferente não são
  diretamente comparáveis.

## Exercício prático

```python
df = pd.DataFrame({
    "cliente": ["A", "B", "C", "D", "E", "F", "G"],
    "idade": [25, 34, 41, 29, 55, 38, 45],
    "plano": ["Basico", "Premium", "Basico", "Basico", "Premium", "Premium", "Basico"],
    "gasto_mensal": [50, 150, 45, 60, 200, 180, 55],
})
```

1. Faça a análise univariada completa da coluna `idade` (média, mediana,
   desvio padrão, min, max, skew).
2. Faça a análise univariada da coluna `plano` (contagem absoluta e
   percentual de cada categoria).
3. Use `.select_dtypes()` para separar as colunas numéricas das
   categóricas.
4. Aplique a função `resumo_numerico` (do exemplo) a todas as colunas
   numéricas de uma vez.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

df = pd.DataFrame({
    "cliente": ["A", "B", "C", "D", "E", "F", "G"],
    "idade": [25, 34, 41, 29, 55, 38, 45],
    "plano": ["Basico", "Premium", "Basico", "Basico", "Premium", "Premium", "Basico"],
    "gasto_mensal": [50, 150, 45, 60, 200, 180, 55],
})

print(df["idade"].describe())
print(df["idade"].skew())

print(df["plano"].value_counts())
print(df["plano"].value_counts(normalize=True) * 100)

numericas = df.select_dtypes(include="number")
categoricas = df.select_dtypes(include="object")
print(numericas.columns.tolist())
print(categoricas.columns.tolist())

def resumo_numerico(serie):
    return pd.Series({
        "media": serie.mean(),
        "mediana": serie.median(),
        "desvio_padrao": serie.std(),
        "minimo": serie.min(),
        "maximo": serie.max(),
        "assimetria": serie.skew(),
    })

print(numericas.apply(resumo_numerico))
```

</details>

## Checklist antes de avançar

- [ ] Sei fazer a análise univariada de uma coluna numérica (tendência central + dispersão + forma)
- [ ] Sei fazer a análise univariada de uma coluna categórica com `value_counts()`
- [ ] Sei usar `.select_dtypes()` para separar colunas numéricas e categóricas
- [ ] Resolvi o exercício sem olhar a solução
