# Agrupamento com groupby

> Módulo 4 — Pandas Essencial · Tópico 8 de 12

## O que é e por que importa

`groupby` é, sem exagero, uma das ferramentas mais poderosas do Pandas.
Responde perguntas do tipo "para cada X, qual é o Y?" — "para cada categoria,
qual o faturamento total?", "para cada cliente, quantas compras ele fez?",
"para cada mês, qual a média de vendas?". Esse padrão (agrupar por uma
categoria e depois resumir) é tão comum em análise de dados que vale a pena
internalizar bem a lógica por trás dele.

A ideia por trás do `groupby` é sempre a mesma, conhecida como
**split-apply-combine**:

1. **Split**: divide o DataFrame em grupos, um para cada valor único da
   coluna escolhida.
2. **Apply**: aplica uma função de agregação (soma, média, contagem...) em
   cada grupo, separadamente.
3. **Combine**: junta os resultados de volta em uma tabela só.

## Como funciona (com exemplo comentado)

```python
import pandas as pd

df = pd.DataFrame({
    "produto": ["Caneta Azul", "Caderno", "Mochila", "Lapis HB", "Estojo", "Borracha"],
    "categoria": ["Papelaria", "Papelaria", "Acessorios", "Papelaria", "Acessorios", "Papelaria"],
    "quantidade": [3, 1, 2, 5, 4, 10],
    "preco_unitario": [2.50, 15.90, 89.90, 1.20, 25.00, 0.90],
})
df["total"] = df["quantidade"] * df["preco_unitario"]

# groupby sozinho não retorna nada "visível" ainda -- é preciso dizer o que agregar
agrupado = df.groupby("categoria")
print(agrupado)  # <pandas.core.groupby.generic.DataFrameGroupBy object ...>

# Agora sim: soma do total, por categoria
soma_por_categoria = df.groupby("categoria")["total"].sum()
print(soma_por_categoria)
# categoria
# Acessorios    204.8
# Papelaria      27.5
# Name: total, dtype: float64

# Outras agregações comuns -- mesmas funções vistas em NumPy (Módulo 3, Tópico 5)
print(df.groupby("categoria")["total"].mean())   # média por categoria
print(df.groupby("categoria")["total"].count())  # quantas linhas por categoria
print(df.groupby("categoria")["total"].max())     # maior valor por categoria
print(df.groupby("categoria").size())             # equivalente a count(), mas conta linhas mesmo com NaN

# Agrupando por mais de uma coluna -- passa uma lista
por_categoria_e_qtd = df.groupby(["categoria", "quantidade"])["total"].sum()
print(por_categoria_e_qtd)

# Agregando MÚLTIPLAS colunas de uma vez, sem escolher só uma
resumo = df.groupby("categoria")[["quantidade", "total"]].sum()
print(resumo)
#             quantidade   total
# categoria
# Acessorios           6   204.8
# Papelaria           19    27.5

# .reset_index() -- transforma o resultado (que tem a categoria como índice)
# de volta em colunas normais, útil para salvar em CSV ou continuar processando
resumo_tabela = resumo.reset_index()
print(resumo_tabela)
#     categoria  quantidade  total
# 0  Acessorios           6  204.8
# 1   Papelaria          19   27.5

# Depois de agrupar, dá pra ordenar normalmente (Tópico 7)
resumo_ordenado = resumo_tabela.sort_values("total", ascending=False)
print(resumo_ordenado)
```

## Erros comuns de quem está começando

- Esquecer de escolher qual coluna agregar e/ou qual função aplicar —
  `df.groupby("categoria")` sozinho não calcula nada, só prepara os grupos; é
  preciso encadear `["coluna"].sum()` (ou outra agregação) para obter um
  resultado.
- Esquecer o `.reset_index()` quando o resultado precisa voltar a ser um
  DataFrame "normal" (por exemplo, para ordenar por uma coluna que virou
  índice, ou para salvar em CSV com a coluna de agrupamento visível).
- Tentar agregar uma coluna de texto com `.sum()`/`.mean()` sem querer —
  isso costuma gerar erro ou resultado sem sentido (concatenar strings em
  vez de somar números); sempre confira quais colunas fazem sentido agregar
  antes de aplicar `.sum()`/`.mean()` a um `groupby` inteiro sem selecionar
  colunas.

## Exercício prático

```python
df = pd.DataFrame({
    "vendedor": ["Marcos", "Julia", "Marcos", "Pedro", "Julia", "Marcos"],
    "produto": ["Caneta", "Caderno", "Mochila", "Estojo", "Lapis", "Caderno"],
    "valor": [7.5, 15.9, 89.9, 25.0, 6.0, 15.9],
})
```

1. Agrupe por `vendedor` e calcule a soma do `valor` vendido por cada um.
2. Descubra quantas vendas (linhas) cada vendedor fez, usando `.size()` ou
   `.count()`.
3. Ordene o resultado do item 1 do vendedor que mais vendeu para o que menos
   vendeu.
4. Descubra qual vendedor teve a maior venda individual (dica: `.max()` por
   vendedor).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

df = pd.DataFrame({
    "vendedor": ["Marcos", "Julia", "Marcos", "Pedro", "Julia", "Marcos"],
    "produto": ["Caneta", "Caderno", "Mochila", "Estojo", "Lapis", "Caderno"],
    "valor": [7.5, 15.9, 89.9, 25.0, 6.0, 15.9],
})

total_por_vendedor = df.groupby("vendedor")["valor"].sum()
print(total_por_vendedor)

qtd_vendas = df.groupby("vendedor").size()
print(qtd_vendas)

total_ordenado = total_por_vendedor.reset_index().sort_values("valor", ascending=False)
print(total_ordenado)

maior_venda_por_vendedor = df.groupby("vendedor")["valor"].max()
print(maior_venda_por_vendedor)
```

</details>

## Checklist antes de avançar

- [ ] Entendo a lógica split-apply-combine por trás do groupby
- [ ] Sei agrupar por uma ou mais colunas e aplicar sum/mean/count/max
- [ ] Sei quando e por que usar `.reset_index()` depois de um groupby
- [ ] Resolvi o exercício sem olhar a solução
