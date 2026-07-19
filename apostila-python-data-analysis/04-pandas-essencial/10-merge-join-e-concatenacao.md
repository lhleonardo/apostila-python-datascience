# Merge, join e concatenação

> Módulo 4 — Pandas Essencial · Tópico 10 de 12

## O que é e por que importa

Dados do mundo real quase nunca vêm todos numa tabela só. Uma loja pode ter
uma tabela de pedidos e outra de clientes; um sistema pode exportar vendas
de janeiro num arquivo e de fevereiro em outro. Pandas tem duas operações
principais para juntar tabelas:

- **`pd.concat()`**: empilha DataFrames — útil quando as tabelas têm as
  **mesmas colunas** e você só quer juntar as linhas (ex: vendas de janeiro
  + vendas de fevereiro).
- **`pd.merge()`**: combina DataFrames **pelo valor de uma coluna em comum**
  (uma chave), parecido com um `JOIN` de banco de dados — útil quando as
  tabelas têm informações complementares (ex: pedidos + dados dos clientes
  que fizeram os pedidos).

## Como funciona (com exemplo comentado)

```python
import pandas as pd

# concat -- empilhando duas tabelas com as mesmas colunas
vendas_jan = pd.DataFrame({
    "produto": ["Caneta", "Caderno"],
    "quantidade": [10, 5],
})
vendas_fev = pd.DataFrame({
    "produto": ["Mochila", "Estojo"],
    "quantidade": [3, 7],
})

vendas_total = pd.concat([vendas_jan, vendas_fev])
print(vendas_total)
#    produto  quantidade
# 0   Caneta          10
# 1  Caderno           5
# 0  Mochila           3
# 1   Estojo           7
# -- repare que o índice se repete (0, 1, 0, 1)! use reset_index (Tópico 7) se precisar

vendas_total = pd.concat([vendas_jan, vendas_fev], ignore_index=True)
print(vendas_total)  # agora o índice é 0, 1, 2, 3 -- sequencial

# merge -- combinando duas tabelas por uma coluna em comum (a "chave")
pedidos = pd.DataFrame({
    "pedido_id": [1, 2, 3, 4],
    "cliente_id": [101, 102, 101, 103],
    "valor": [150.0, 89.9, 45.0, 200.0],
})

clientes = pd.DataFrame({
    "cliente_id": [101, 102, 103],
    "nome": ["Marcos", "Julia", "Pedro"],
    "cidade": ["São Paulo", "Rio de Janeiro", "Belo Horizonte"],
})

# merge padrão ("inner"): só mantém linhas cuja chave existe nas DUAS tabelas
pedidos_com_cliente = pd.merge(pedidos, clientes, on="cliente_id")
print(pedidos_com_cliente)
#    pedido_id  cliente_id  valor    nome          cidade
# 0          1         101  150.0  Marcos       São Paulo
# 1          3         101   45.0  Marcos       São Paulo
# 2          2         102   89.9   Julia  Rio de Janeiro
# 3          4         103  200.0   Pedro  Belo Horizonte

# how="left" -- mantém TODAS as linhas da tabela da esquerda (pedidos),
# mesmo que não encontre correspondência na direita (preenche com NaN)
pedidos_todos = pd.merge(pedidos, clientes, on="cliente_id", how="left")

# how="right" -- mantém TODAS as linhas da tabela da direita (clientes)
clientes_com_pedidos = pd.merge(pedidos, clientes, on="cliente_id", how="right")

# how="outer" -- mantém TODAS as linhas de ambas, preenchendo com NaN onde não bate
tudo = pd.merge(pedidos, clientes, on="cliente_id", how="outer")

# Quando o nome da coluna-chave é diferente nas duas tabelas, use left_on/right_on
# pd.merge(pedidos, clientes, left_on="cliente_id", right_on="id_do_cliente")
```

A escolha de `how` é a decisão mais importante num merge: pense em qual
tabela é a "principal" (você quer manter todas as linhas dela mesmo sem
correspondência) e escolha `left`/`right` de acordo, ou `outer` se quiser
tudo de ambas, ou o padrão `inner` se só interessam os casos que batem nas
duas.

## Erros comuns de quem está começando

- Usar `pd.concat()` para juntar tabelas com colunas diferentes por engano
  (por exemplo, `pedidos` e `clientes`) — o resultado fica cheio de `NaN`
  porque `concat` só empilha linhas, não combina por chave. Para combinar
  informações de tabelas diferentes, o certo é `merge`.
- Esquecer o `how` no merge e ser surpreendido pelo padrão `inner`, que
  **descarta silenciosamente** linhas sem correspondência — se o resultado
  do merge tem menos linhas do que o esperado, o primeiro suspeito é sempre
  o `how`.
- Fazer merge por uma coluna-chave com tipos diferentes nas duas tabelas
  (uma como texto, outra como número) — o merge não encontra correspondência
  nenhuma e o resultado sai vazio ou cheio de `NaN`, sem erro explícito.
  Confira `.dtypes` das colunas-chave antes de dar merge se o resultado
  parecer estranho.

## Exercício prático

```python
produtos = pd.DataFrame({
    "produto_id": [1, 2, 3],
    "nome": ["Caneta", "Caderno", "Mochila"],
    "preco": [2.5, 15.9, 89.9],
})

vendas = pd.DataFrame({
    "venda_id": [1, 2, 3, 4],
    "produto_id": [1, 2, 1, 4],  # repare: produto_id 4 não existe em "produtos"
    "quantidade": [3, 1, 2, 5],
})
```

1. Faça um merge de `vendas` com `produtos` usando `how="inner"` e veja
   quantas linhas sobram (deve ser 3, já que o `produto_id` 4 não existe em
   `produtos`).
2. Faça o mesmo merge com `how="left"` (mantendo todas as vendas) e observe
   os valores `NaN` que aparecem para o `produto_id` 4.
3. No resultado do merge com `how="left"`, crie uma coluna `total` com
   `quantidade * preco` (linhas com `preco` ausente vão gerar `NaN` no
   total — normal, veremos como tratar isso no Módulo 5).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

produtos = pd.DataFrame({
    "produto_id": [1, 2, 3],
    "nome": ["Caneta", "Caderno", "Mochila"],
    "preco": [2.5, 15.9, 89.9],
})

vendas = pd.DataFrame({
    "venda_id": [1, 2, 3, 4],
    "produto_id": [1, 2, 1, 4],
    "quantidade": [3, 1, 2, 5],
})

merge_inner = pd.merge(vendas, produtos, on="produto_id", how="inner")
print(merge_inner)      # 3 linhas
print(merge_inner.shape)

merge_left = pd.merge(vendas, produtos, on="produto_id", how="left")
print(merge_left)  # 4 linhas, com NaN para produto_id 4

merge_left["total"] = merge_left["quantidade"] * merge_left["preco"]
print(merge_left)
```

</details>

## Checklist antes de avançar

- [ ] Sei quando usar `concat` (empilhar) e quando usar `merge` (combinar por chave)
- [ ] Sei explicar a diferença entre `how="inner"`, `"left"`, `"right"` e `"outer"`
- [ ] Sei diagnosticar um merge com resultado vazio ou menor que o esperado
- [ ] Resolvi o exercício sem olhar a solução
