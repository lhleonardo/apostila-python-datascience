# Tuplas

> Módulo 1 — Fundamentos de Python · Tópico 17 de 25

## O que é e por que importa

Tupla é uma coleção ordenada de valores, muito parecida com uma lista (`16-listas.md`), com uma diferença fundamental: depois de criada, ela não pode ser alterada — não dá para adicionar, remover ou trocar itens. Por isso dizemos que tupla é "imutável", enquanto lista é "mutável".

Pensa em tupla como um "pacote fechado e lacrado": uma vez que você define, por exemplo, as coordenadas de um endereço `(latitude, longitude)` ou os dados fixos de um produto `("Caneta Azul", "Papelaria")`, não faz sentido que esses valores mudem no meio do programa. Usar tupla nesses casos é uma forma de dizer "isso aqui é fixo" tanto para quem lê o código quanto para o próprio Python, que pode até otimizar o uso de memória sabendo disso.

Em análise de dados, tuplas aparecem com frequência para representar um "registro" com poucos campos fixos (como um par nome-valor) ou quando uma função (veremos em `22-definindo-funcoes.md`) precisa devolver mais de um resultado de uma vez.

## Como funciona (com exemplo comentado)

```python
# Tupla criada com parênteses (embora, tecnicamente, o que define é a vírgula)
produto = ("Caneta Azul", 5.90, "Papelaria")

# Acesso por índice, igual em listas
nome = produto[0]
preco = produto[1]
categoria = produto[2]
print(nome, preco, categoria)

# len() também funciona em tuplas
print("Quantidade de campos:", len(produto))

# for também percorre tuplas normalmente
for informacao in produto:
    print(informacao)

# Tentar alterar um item de uma tupla gera erro
try:
    produto[1] = 6.50
except TypeError as erro:
    print("Não é possível alterar uma tupla:", erro)

# "Desempacotamento": jeito prático de separar os valores de uma tupla em variáveis
nome, preco, categoria = produto
print(f"{nome} custa R$ {preco} e é da categoria {categoria}")

# Uso comum: uma lista de tuplas representando várias vendas (produto, valor)
vendas = [("Caneta Azul", 5.90), ("Caderno", 12.50), ("Borracha", 2.25)]

for venda in vendas:
    nome_produto, valor = venda
    print(f"Vendido: {nome_produto} por R$ {valor}")
```

## Erros comuns de quem está começando

- Tentar alterar um item de tupla como se fosse lista (`produto[1] = 6.50`), o que gera `TypeError`. Se você precisa alterar os valores depois, a estrutura certa é lista, não tupla.
- Esquecer a vírgula ao criar uma tupla de um item só: `(5.90)` não é uma tupla, é só o número entre parênteses. O correto é `(5.90,)`, com vírgula no final.
- Confundir quando usar tupla e quando usar lista. Regra prática: se os dados podem crescer, encolher ou mudar durante o programa, use lista; se são um conjunto fixo de valores relacionados, tupla é mais apropriada.

## Exercício prático

A Loja da Ana quer guardar informações fixas de um produto: nome, preço e categoria.

1. Crie uma tupla `produto` com os valores `("Mochila Escolar", 89.90, "Acessórios")`.
2. Use desempacotamento para separar os três valores em variáveis (`nome`, `preco`, `categoria`).
3. Mostre uma mensagem formatada com os três valores.

**Desafio bônus (opcional):** crie uma lista chamada `catalogo` com três tuplas de produtos diferentes (nome, preço, categoria) e use um `for` para mostrar todos, um por linha.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
# Tupla representando um produto (dados fixos)
produto = ("Mochila Escolar", 89.90, "Acessórios")

# Desempacotando os valores
nome, preco, categoria = produto
print(f"{nome} - R$ {preco} - Categoria: {categoria}")

# Desafio bônus: catálogo com várias tuplas
catalogo = [
    ("Mochila Escolar", 89.90, "Acessórios"),
    ("Caneta Azul", 5.90, "Papelaria"),
    ("Caderno Universitário", 12.90, "Papelaria"),
]

for item in catalogo:
    nome_item, preco_item, categoria_item = item
    print(f"{nome_item} - R$ {preco_item} - Categoria: {categoria_item}")
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar a diferença entre lista e tupla com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Sei fazer desempacotamento de tupla em variáveis
