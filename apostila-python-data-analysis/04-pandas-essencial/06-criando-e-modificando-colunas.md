# Criando e modificando colunas

> Módulo 4 — Pandas Essencial · Tópico 6 de 12

## O que é e por que importa

Depois de carregar e filtrar dados, é comum precisar **transformá-los**:
calcular uma coluna nova a partir de outras (o total de uma venda = preço
vezes quantidade), renomear colunas com nomes ruins, mudar o tipo de uma
coluna, ou aplicar uma função personalizada linha a linha. Essa é a etapa
onde os dados brutos começam a virar informação útil.

## Como funciona (com exemplo comentado)

```python
import pandas as pd

df = pd.DataFrame({
    "produto": ["Caneta Azul", "Caderno", "Mochila", "Lapis HB"],
    "quantidade": [3, 1, 2, 5],
    "preco_unitario": [2.50, 15.90, 89.90, 1.20],
})

# Criar uma coluna nova: operação vetorizada, igual a arrays NumPy (Módulo 3)
df["total"] = df["quantidade"] * df["preco_unitario"]
print(df)
#        produto  quantidade  preco_unitario  total
# 0  Caneta Azul           3            2.50    7.5
# 1      Caderno           1           15.90   15.9
# 2      Mochila           2           89.90  179.8
# 3     Lapis HB           5            1.20    6.0

# Criar coluna a partir de uma condição -- combina com boolean masking (Tópico 5)
df["categoria_preco"] = "barato"
df.loc[df["preco_unitario"] > 10, "categoria_preco"] = "caro"
print(df["categoria_preco"])

# Forma equivalente e mais direta com np.where (visto no Módulo 3, Tópico 7)
import numpy as np
df["categoria_preco_v2"] = np.where(df["preco_unitario"] > 10, "caro", "barato")

# Modificar uma coluna existente -- mesma sintaxe de criar, só que o nome já existe
df["preco_unitario"] = df["preco_unitario"] * 1.10  # reajuste de 10% em tudo

# Renomear colunas
df = df.rename(columns={"total": "valor_total", "produto": "nome_produto"})
print(df.columns.tolist())

# Remover colunas
df = df.drop(columns=["categoria_preco_v2"])
# (também é possível usar: df.drop("categoria_preco_v2", axis=1))

# .apply() -- aplica uma função a cada valor de uma coluna (ou linha, com axis=1)
# use quando a transformação não dá pra fazer com operações vetorizadas simples
def classificar_estoque(quantidade):
    if quantidade >= 5:
        return "alto"
    elif quantidade >= 2:
        return "medio"
    return "baixo"

df["nivel_estoque"] = df["quantidade"].apply(classificar_estoque)
print(df[["nome_produto", "quantidade", "nivel_estoque"]])

# .apply(..., axis=1) -- aplica uma função a cada LINHA inteira (recebe a linha como argumento)
def resumo_linha(linha):
    return f"{linha['nome_produto']}: {linha['quantidade']} un."

df["resumo"] = df.apply(resumo_linha, axis=1)
print(df["resumo"])

# Mudando o tipo de uma coluna com .astype()
df["quantidade"] = df["quantidade"].astype(float)
print(df["quantidade"].dtype)  # float64
```

Uma regra prática importante: sempre que a transformação puder ser escrita
como uma **operação vetorizada** (`coluna_a * coluna_b`, `np.where(...)`),
prefira isso a `.apply()`. `.apply()` roda uma função Python por linha, o que
é bem mais lento em DataFrames grandes — reserve `.apply()` para lógicas que
realmente não dá para vetorizar.

## Erros comuns de quem está começando

- Usar `.apply()` para contas simples (soma, multiplicação, comparação) que
  já funcionam vetorizadas — funciona, mas é desnecessariamente lento e
  menos idiomático.
- Esquecer que a maioria dos métodos do Pandas (como `.rename()`, `.drop()`)
  **retorna um novo DataFrame** por padrão, em vez de alterar o original.
  Se você chamar `df.rename(columns=...)` sem reatribuir (`df = df.rename(...)`),
  a mudança se perde. (Alguns métodos aceitam `inplace=True` para alterar
  direto, mas o time do Pandas recomenda evitar esse parâmetro — reatribuir é
  mais previsível.)
- Esquecer `axis=1` ao usar `.apply()` para operar em linhas inteiras — sem
  isso, o Pandas assume que você quer aplicar a função a cada **coluna**
  (`axis=0`, o padrão), o que raramente é a intenção quando a função espera
  uma linha completa.

## Exercício prático

```python
df = pd.DataFrame({
    "produto": ["Caneta Azul", "Caderno", "Mochila", "Lapis HB"],
    "quantidade": [3, 1, 2, 5],
    "preco_unitario": [2.50, 15.90, 89.90, 1.20],
})
```

1. Crie a coluna `total` (`quantidade * preco_unitario`).
2. Crie a coluna `frete_gratis`, que vale `True` quando `total` for maior que
   R$ 50, e `False` caso contrário (use `np.where` ou `.loc`).
3. Renomeie a coluna `produto` para `nome`.
4. Usando `.apply()`, crie a coluna `etiqueta` com o texto
   `"{nome} (x{quantidade})"` para cada linha (por exemplo, `"Caderno (x1)"`).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "produto": ["Caneta Azul", "Caderno", "Mochila", "Lapis HB"],
    "quantidade": [3, 1, 2, 5],
    "preco_unitario": [2.50, 15.90, 89.90, 1.20],
})

df["total"] = df["quantidade"] * df["preco_unitario"]

df["frete_gratis"] = np.where(df["total"] > 50, True, False)

df = df.rename(columns={"produto": "nome"})

df["etiqueta"] = df.apply(lambda linha: f"{linha['nome']} (x{linha['quantidade']})", axis=1)

print(df)
```

</details>

## Checklist antes de avançar

- [ ] Sei criar colunas novas com operações vetorizadas entre colunas existentes
- [ ] Sei usar `.loc` ou `np.where` para criar colunas baseadas em condições
- [ ] Sei quando usar `.apply()` e por que evitá-lo quando dá pra vetorizar
- [ ] Sei que a maioria dos métodos do Pandas retorna um DataFrame novo (preciso reatribuir)
- [ ] Resolvi o exercício sem olhar a solução
