# Filtragem de dados

> Módulo 4 — Pandas Essencial · Tópico 5 de 12

## O que é e por que importa

Filtrar é selecionar só as linhas que atendem a alguma condição: "só os
produtos com estoque baixo", "só as vendas de junho", "só os clientes de São
Paulo". É provavelmente a operação mais usada em análise de dados no
dia a dia, e funciona com o **mesmo princípio de boolean masking** que você
já viu em arrays NumPy no Módulo 3 (Tópico 7) — a diferença é que agora a
máscara filtra linhas inteiras de uma tabela, não só números soltos.

## Como funciona (com exemplo comentado)

```python
import pandas as pd

df = pd.DataFrame({
    "produto": ["Caneta Azul", "Caderno", "Mochila", "Lapis HB", "Estojo"],
    "categoria": ["Papelaria", "Papelaria", "Acessorios", "Papelaria", "Acessorios"],
    "quantidade": [3, 1, 2, 5, 4],
    "preco_unitario": [2.50, 15.90, 89.90, 1.20, 25.00],
})

# Passo 1: criar a máscara -- comparar uma coluna com um valor retorna uma Series booleana
mascara = df["preco_unitario"] > 10
print(mascara)
# 0    False
# 1     True
# 2     True
# 3    False
# 4     True
# Name: preco_unitario, dtype: bool

# Passo 2: usar a máscara para filtrar o DataFrame
caros = df[mascara]
print(caros)

# Na prática, quase sempre se escreve direto, sem variável intermediária:
caros = df[df["preco_unitario"] > 10]
baratos = df[df["preco_unitario"] <= 10]

# Combinando condições: & (E) e | (OU) -- assim como em NumPy, cada condição
# precisa de parênteses, e NUNCA use "and"/"or" do Python puro aqui
papelaria_barata = df[(df["categoria"] == "Papelaria") & (df["preco_unitario"] < 5)]
print(papelaria_barata)

caros_ou_papelaria = df[(df["preco_unitario"] > 50) | (df["categoria"] == "Papelaria")]
print(caros_ou_papelaria)

# .isin() -- filtra por uma lista de valores possíveis (equivalente a vários "OU")
selecionados = df[df["produto"].isin(["Caneta Azul", "Mochila"])]
print(selecionados)

# ~ (til) -- inverte a condição (equivalente a "NÃO")
nao_papelaria = df[~(df["categoria"] == "Papelaria")]
print(nao_papelaria)  # o mesmo que df[df["categoria"] != "Papelaria"]

# .query() -- forma alternativa, com a condição como string (alguns acham mais legível)
resultado = df.query("preco_unitario > 10 and categoria == 'Papelaria'")
print(resultado)
# repare que dentro de .query() SE usa "and"/"or" normalmente -- é uma string
# interpretada pelo Pandas, não código Python puro sendo avaliado direto

# Filtrando e já selecionando colunas específicas do resultado
nomes_dos_caros = df.loc[df["preco_unitario"] > 10, "produto"]
print(nomes_dos_caros)  # só a coluna "produto" das linhas filtradas
```

## Erros comuns de quem está começando

- Usar `and`/`or` em vez de `&`/`|` ao combinar condições fora do `.query()`
  — mesmo erro visto com arrays NumPy, e pela mesma razão: essas condições
  retornam uma Series inteira de booleanos, não um único `True`/`False`.
- Esquecer os parênteses ao redor de cada condição:
  `df[df["preco"] > 10 & df["categoria"] == "X"]` (sem parênteses) quebra
  por causa da precedência de operadores — sempre
  `(condicao1) & (condicao2)`.
- Comparar strings com case sensitivity diferente do esperado — `"papelaria"
  != "Papelaria"` para o Pandas. Se a filtragem por texto não estiver
  encontrando nada, vale conferir com `.unique()` os valores exatos que
  existem na coluna antes de assumir que a condição está errada.

## Exercício prático

```python
df = pd.DataFrame({
    "produto": ["Caneta Azul", "Caderno", "Mochila", "Lapis HB", "Estojo", "Borracha"],
    "categoria": ["Papelaria", "Papelaria", "Acessorios", "Papelaria", "Acessorios", "Papelaria"],
    "quantidade": [3, 1, 2, 5, 4, 10],
    "preco_unitario": [2.50, 15.90, 89.90, 1.20, 25.00, 0.90],
})
```

1. Filtre os produtos com `quantidade` maior que 3.
2. Filtre os produtos da categoria `"Papelaria"` com `preco_unitario` menor
   que 2.
3. Filtre os produtos que são `"Mochila"` ou `"Estojo"` usando `.isin()`.
4. Usando `.loc`, obtenha só a coluna `produto` dos itens com `quantidade`
   maior ou igual a 4.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

df = pd.DataFrame({
    "produto": ["Caneta Azul", "Caderno", "Mochila", "Lapis HB", "Estojo", "Borracha"],
    "categoria": ["Papelaria", "Papelaria", "Acessorios", "Papelaria", "Acessorios", "Papelaria"],
    "quantidade": [3, 1, 2, 5, 4, 10],
    "preco_unitario": [2.50, 15.90, 89.90, 1.20, 25.00, 0.90],
})

muita_quantidade = df[df["quantidade"] > 3]
print(muita_quantidade)

papelaria_baratissima = df[(df["categoria"] == "Papelaria") & (df["preco_unitario"] < 2)]
print(papelaria_baratissima)

selecionados = df[df["produto"].isin(["Mochila", "Estojo"])]
print(selecionados)

produtos_com_estoque_alto = df.loc[df["quantidade"] >= 4, "produto"]
print(produtos_com_estoque_alto)
```

</details>

## Checklist antes de avançar

- [ ] Sei filtrar um DataFrame com uma condição simples e com condições combinadas (`&`/`|`)
- [ ] Sei usar `.isin()` para filtrar por uma lista de valores
- [ ] Sei usar `~` para inverter uma condição
- [ ] Resolvi o exercício sem olhar a solução
