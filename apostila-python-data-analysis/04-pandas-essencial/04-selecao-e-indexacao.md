# Seleção e indexação (loc, iloc)

> Módulo 4 — Pandas Essencial · Tópico 4 de 12

## O que é e por que importa

Selecionar pedaços de um DataFrame — uma coluna, algumas linhas, uma célula
específica — é algo que você vai fazer o tempo todo. Pandas tem várias formas
de fazer isso, e a mais confiável (a que sempre funciona do jeito esperado) é
usar `.loc[]` e `.iloc[]`:

- **`.loc[]`** seleciona por **rótulo** (label): o nome do índice, o nome da
  coluna.
- **`.iloc[]`** seleciona por **posição** (integer location): o número da
  linha/coluna, começando em 0 — igual à indexação de listas e arrays NumPy
  (Módulo 3).

Entender a diferença evita um dos erros mais comuns em Pandas: usar colchetes
simples (`df[...]`) de forma ambígua e obter um resultado inesperado.

## Como funciona (com exemplo comentado)

```python
import pandas as pd

df = pd.DataFrame({
    "produto": ["Caneta Azul", "Caderno", "Mochila", "Lapis HB"],
    "quantidade": [3, 1, 2, 5],
    "preco_unitario": [2.50, 15.90, 89.90, 1.20],
}, index=["p1", "p2", "p3", "p4"])  # índice com rótulos de texto, não números

# Selecionar UMA coluna -- retorna uma Series
print(df["produto"])

# Selecionar VÁRIAS colunas -- colchete duplo, retorna um DataFrame
print(df[["produto", "preco_unitario"]])

# .loc -- seleciona por RÓTULO (nome do índice e/ou nome da coluna)
print(df.loc["p2"])              # linha inteira com índice "p2" (retorna uma Series)
print(df.loc["p2", "produto"])   # "Caderno" -- célula específica
print(df.loc["p1":"p3"])         # linhas de "p1" até "p3" -- ATENÇÃO: com .loc, o fim é INCLUSIVO
print(df.loc[:, "produto"])      # todas as linhas, só a coluna "produto"
print(df.loc[["p1", "p3"], ["produto", "quantidade"]])  # linhas e colunas específicas

# .iloc -- seleciona por POSIÇÃO (números, como em listas/arrays)
print(df.iloc[0])          # primeira linha (posição 0), seja qual for o rótulo do índice
print(df.iloc[0, 1])       # linha 0, coluna 1 (quantidade da primeira linha) -> 3
print(df.iloc[0:2])        # linhas 0 e 1 -- com .iloc, o fim é EXCLUSIVO (igual listas/NumPy)
print(df.iloc[:, 0])       # todas as linhas, coluna de posição 0 (produto)
print(df.iloc[[0, 2], [0, 1]])  # linhas 0 e 2, colunas 0 e 1

# Um erro comum: usar colchete simples com número em índice não-numérico
# df[0]  # ERRO -- o índice aqui é texto ("p1", "p2"...), não existe coluna/rótulo "0"

# Quando o índice É numérico (o padrão, 0, 1, 2...), .loc e .iloc podem parecer
# iguais, mas ainda se comportam diferente com fatias:
df_padrao = df.reset_index(drop=True)  # volta para índice numérico 0,1,2,3
print(df_padrao.loc[0:2])   # linhas 0, 1 E 2 (fim inclusivo)
print(df_padrao.iloc[0:2])  # linhas 0 e 1 apenas (fim exclusivo)
```

## Erros comuns de quem está começando

- Usar `df[0]` esperando pegar a primeira linha — colchete simples com um
  índice de texto tenta achar uma **coluna** chamada `0`, e dá erro. Para
  pegar linhas por posição, use `.iloc[0]`.
- Esquecer que `.loc` inclui o valor final em fatias (`df.loc["p1":"p3"]`
  inclui `"p3"`), enquanto `.iloc` exclui (`df.iloc[0:2]` não inclui a
  posição 2) — a mesma diferença de comportamento entre slicing "por rótulo"
  e "por posição" que existe em outras partes do Pandas.
- Misturar rótulo e posição no mesmo `.loc`/`.iloc`, como `df.loc[0]` num
  DataFrame cujo índice não é numérico (não existe rótulo `0`) — sempre
  confirme qual é o índice atual do DataFrame (`df.index`) antes de usar
  `.loc`.

## Exercício prático

```python
df = pd.DataFrame({
    "cidade": ["São Paulo", "Rio de Janeiro", "Belo Horizonte", "Salvador"],
    "populacao_milhoes": [12.3, 6.7, 2.5, 2.9],
    "regiao": ["Sudeste", "Sudeste", "Sudeste", "Nordeste"],
}, index=["c1", "c2", "c3", "c4"])
```

1. Use `.loc` para selecionar a linha da cidade `"c3"`.
2. Use `.iloc` para selecionar a última linha do DataFrame, sem usar o
   número `3` diretamente (dica: `-1` funciona em `.iloc` como em listas).
3. Use `.loc` para selecionar só as colunas `cidade` e `regiao` das linhas
   `"c1"` e `"c4"`.
4. Use `.iloc` para pegar a célula da linha de posição 1, coluna de posição 1
   (deve ser `6.7`).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

df = pd.DataFrame({
    "cidade": ["São Paulo", "Rio de Janeiro", "Belo Horizonte", "Salvador"],
    "populacao_milhoes": [12.3, 6.7, 2.5, 2.9],
    "regiao": ["Sudeste", "Sudeste", "Sudeste", "Nordeste"],
}, index=["c1", "c2", "c3", "c4"])

print(df.loc["c3"])

print(df.iloc[-1])

print(df.loc[["c1", "c4"], ["cidade", "regiao"]])

print(df.iloc[1, 1])  # 6.7
```

</details>

## Checklist antes de avançar

- [ ] Sei quando usar `.loc` (por rótulo) e quando usar `.iloc` (por posição)
- [ ] Sei a diferença de comportamento de fatias entre os dois (fim inclusivo x exclusivo)
- [ ] Sei selecionar uma coluna, várias colunas, uma linha e uma célula específica
- [ ] Resolvi o exercício sem olhar a solução
