# Dicionários

> Módulo 1 — Fundamentos de Python · Tópico 18 de 25

## O que é e por que importa

Dicionário é uma coleção de dados organizada em pares de "chave" e "valor" — em vez de acessar um item pela posição (como em listas, `16-listas.md`), você acessa pelo nome. Pensa em um dicionário de verdade: você não procura a palavra "maçã" pela posição 4523 na página, você procura pela própria palavra. Em Python, `dict` funciona assim: `produto["nome"]` te dá o valor associado à chave `"nome"`.

Isso resolve um problema real de listas simples: se você guarda `["Caneta Azul", 5.90, 10]`, precisa lembrar de cabeça que a posição 0 é o nome, a 1 é o preço e a 2 é a quantidade. Com dicionário, você escreve `{"nome": "Caneta Azul", "preco": 5.90, "quantidade": 10}` e acessa cada campo pelo nome, o que deixa o código muito mais legível e menos sujeito a erro.

Em análise de dados, dicionários são a forma mais natural de representar um "registro" com vários campos nomeados — muito parecido com uma linha de planilha, onde cada coluna tem um nome. É também a estrutura de dados por trás de formatos populares como JSON, super comuns quando dados vêm de sites ou de outros sistemas.

## Como funciona (com exemplo comentado)

```python
# Um dicionário representando um produto da Loja da Ana
produto = {
    "nome": "Caneta Azul",
    "preco": 5.90,
    "quantidade_estoque": 10,
    "categoria": "Papelaria",
}

# Acessando um valor pela chave
print(produto["nome"])       # Caneta Azul
print(produto["preco"])      # 5.90

# Alterando um valor existente
produto["quantidade_estoque"] = 8
print(produto["quantidade_estoque"])  # 8

# Adicionando uma nova chave
produto["em_promocao"] = False
print(produto)

# .get() acessa um valor sem quebrar o programa se a chave não existir
fornecedor = produto.get("fornecedor", "Não informado")
print(fornecedor)  # "Não informado", pois a chave "fornecedor" não existe

# .keys(), .values() e .items() percorrem o dicionário de formas diferentes
for chave in produto.keys():
    print("Chave:", chave)

for valor in produto.values():
    print("Valor:", valor)

for chave, valor in produto.items():
    print(f"{chave}: {valor}")

# Uso muito comum: uma lista de dicionários, representando várias vendas
vendas = [
    {"produto": "Caneta Azul", "valor": 5.90, "quantidade": 3},
    {"produto": "Caderno", "valor": 12.50, "quantidade": 1},
]

for venda in vendas:
    total_venda = venda["valor"] * venda["quantidade"]
    print(f"{venda['produto']}: total de R$ {total_venda}")
```

## Erros comuns de quem está começando

- Acessar uma chave que não existe com `[]` (ex: `produto["fornecedor"]`), o que gera erro `KeyError`. Quando não tem certeza se a chave existe, use `.get()`, que permite definir um valor padrão.
- Confundir chave de dicionário com índice de lista. Dicionários não têm "posição 0" — a ordem de inserção até é preservada em Python moderno, mas o acesso correto é sempre pela chave.
- Esquecer as aspas nas chaves de texto (`produto[nome]` em vez de `produto["nome"]`), o que faz o Python procurar por uma variável chamada `nome`, gerando erro se ela não existir.

## Exercício prático

A Loja da Ana quer representar uma venda como um dicionário.

1. Crie um dicionário `venda` com as chaves `"produto"` (texto), `"preco_unitario"` (float), `"quantidade"` (int) e `"forma_pagamento"` (texto).
2. Calcule o valor total da venda (`preco_unitario * quantidade`) e guarde numa nova chave `"total"` dentro do próprio dicionário.
3. Mostre uma mensagem com todos os dados da venda, usando as chaves do dicionário.

**Desafio bônus (opcional):** crie uma lista `vendas_do_dia` com três dicionários de vendas diferentes, use um `for` para somar o `"total"` de todas e mostre o faturamento do dia.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
venda = {
    "produto": "Caneta Azul",
    "preco_unitario": 5.90,
    "quantidade": 3,
    "forma_pagamento": "dinheiro",
}

# Calculando o total e guardando dentro do próprio dicionário
venda["total"] = venda["preco_unitario"] * venda["quantidade"]

print(f"Produto: {venda['produto']}")
print(f"Quantidade: {venda['quantidade']}")
print(f"Forma de pagamento: {venda['forma_pagamento']}")
print(f"Total: R$ {venda['total']}")

# Desafio bônus
vendas_do_dia = [
    {"produto": "Caneta Azul", "preco_unitario": 5.90, "quantidade": 3},
    {"produto": "Caderno", "preco_unitario": 12.50, "quantidade": 2},
    {"produto": "Borracha", "preco_unitario": 2.25, "quantidade": 5},
]

faturamento_total = 0
for venda_do_dia in vendas_do_dia:
    total_venda = venda_do_dia["preco_unitario"] * venda_do_dia["quantidade"]
    faturamento_total = faturamento_total + total_venda

print("Faturamento do dia:", faturamento_total)
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar o que é um dicionário (chave/valor) com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Sei usar `.get()` para acessar uma chave com segurança
