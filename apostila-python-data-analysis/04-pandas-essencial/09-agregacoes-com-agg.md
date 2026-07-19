# Agregações com agg

> Módulo 4 — Pandas Essencial · Tópico 9 de 12

## O que é e por que importa

No tópico anterior você aplicou uma agregação por vez (`.sum()`, `.mean()`)
depois de um `groupby`. Mas frequentemente você quer **várias agregações ao
mesmo tempo** — por exemplo, para cada categoria, ver soma, média E contagem
juntas — ou aplicar **agregações diferentes para colunas diferentes**. É para
isso que existe `.agg()` (abreviação de *aggregate*): a forma flexível de
combinar múltiplas agregações num único comando.

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

# .agg() com uma lista de funções -- aplica TODAS na mesma coluna
resumo = df.groupby("categoria")["total"].agg(["sum", "mean", "count", "max"])
print(resumo)
#             sum       mean  count    max
# categoria
# Acessorios  204.8  102.400000      2  179.8
# Papelaria    27.5    9.166667      4   15.9

# .agg() com um dicionário -- escolhe agregações DIFERENTES para colunas diferentes
resumo_customizado = df.groupby("categoria").agg({
    "total": "sum",          # soma do total
    "quantidade": "mean",    # média da quantidade
    "produto": "count",      # quantidade de produtos (linhas) no grupo
})
print(resumo_customizado)

# .agg() com nomes de coluna personalizados no resultado (named aggregation)
# a sintaxe é: nome_da_coluna_nova=("coluna_original", "funcao")
resumo_nomeado = df.groupby("categoria").agg(
    total_vendido=("total", "sum"),
    ticket_medio=("total", "mean"),
    qtd_produtos=("produto", "count"),
)
print(resumo_nomeado)
#             total_vendido  ticket_medio  qtd_produtos
# categoria
# Acessorios          204.8    102.400000             2
# Papelaria            27.5      9.166667             4
# -- essa forma é a mais recomendada quando você precisa de nomes claros,
#    porque evita colunas com nomes genéricos como "sum" ou "mean"

# .agg() também aceita funções personalizadas, não só nomes prontos como "sum"
def amplitude(serie):
    return serie.max() - serie.min()

resumo_com_funcao_customizada = df.groupby("categoria")["total"].agg(["mean", amplitude])
print(resumo_com_funcao_customizada)

# Sem groupby, .agg() também funciona no DataFrame inteiro -- útil para um resumo geral
resumo_geral = df[["quantidade", "total"]].agg(["sum", "mean"])
print(resumo_geral)
```

## Erros comuns de quem está começando

- Usar `.agg(["sum", "mean"])` numa coluna e depois se confundir com o
  resultado ter as funções como **colunas** (quando `.agg` é aplicado numa
  única coluna) — vale sempre imprimir e conferir a forma do resultado antes
  de seguir usando.
- Esquecer que os nomes das funções em `.agg()` são strings (`"sum"`, não
  `sum`) quando referenciando funções prontas do Pandas — usar o nome sem
  aspas (`sum`) na verdade chama a função `sum` embutida do Python, que
  também funciona em alguns casos mas não é a forma idiomática esperada.
- Preferir sempre `.sum()`/`.mean()` soltos mesmo quando precisa de várias
  agregações ao mesmo tempo, encadeando vários `groupby` separados em vez de
  um único `.agg()` — além de mais verboso, é mais lento (recalcula os
  grupos várias vezes).

## Exercício prático

```python
df = pd.DataFrame({
    "vendedor": ["Marcos", "Julia", "Marcos", "Pedro", "Julia", "Marcos"],
    "produto": ["Caneta", "Caderno", "Mochila", "Estojo", "Lapis", "Caderno"],
    "valor": [7.5, 15.9, 89.9, 25.0, 6.0, 15.9],
})
```

1. Use `.agg()` com uma lista para calcular soma, média e contagem do
   `valor`, agrupado por `vendedor`.
2. Use named aggregation (`nome=("coluna", "funcao")`) para criar um
   resumo com as colunas `total_vendido`, `ticket_medio` e `qtd_vendas`.
3. Ordene o resultado do item 2 por `total_vendido`, do maior para o menor.

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

resumo_lista = df.groupby("vendedor")["valor"].agg(["sum", "mean", "count"])
print(resumo_lista)

resumo_nomeado = df.groupby("vendedor").agg(
    total_vendido=("valor", "sum"),
    ticket_medio=("valor", "mean"),
    qtd_vendas=("valor", "count"),
)
print(resumo_nomeado)

resumo_ordenado = resumo_nomeado.sort_values("total_vendido", ascending=False)
print(resumo_ordenado)
```

</details>

## Checklist antes de avançar

- [ ] Sei usar `.agg()` com uma lista de funções para múltiplas agregações na mesma coluna
- [ ] Sei usar `.agg()` com dicionário para agregações diferentes por coluna
- [ ] Sei usar named aggregation para nomear colunas de resultado claramente
- [ ] Resolvi o exercício sem olhar a solução
