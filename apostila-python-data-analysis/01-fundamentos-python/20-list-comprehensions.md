# List comprehensions

> Módulo 1 — Fundamentos de Python · Tópico 20 de 25

## O que é e por que importa

List comprehension é uma forma compacta de criar uma lista nova a partir de outra, aplicando uma transformação e/ou um filtro, tudo em uma linha só. É basicamente um `for` (visto em `12-loops.md`) que constrói uma lista, só que escrito de forma mais enxuta.

Pensa no problema: você tem uma lista de preços sem desconto e quer uma lista nova com todos os preços já com 10% de desconto aplicado. Com `for` tradicional, você criaria uma lista vazia, faria um loop, e usaria `.append()` a cada volta (como fizemos em `16-listas.md`). List comprehension faz a mesma coisa em uma única linha, e é a forma que a maioria dos programadores Python prefere escrever quando a transformação é simples.

Em análise de dados, esse padrão — "para cada item de uma lista, calcule algo e monte uma lista nova" (ou "para cada item, mantenha só os que passam em um filtro") — é extremamente comum: aplicar desconto em todos os preços, filtrar só as vendas acima de um valor, extrair só os nomes de uma lista de dicionários.

## Como funciona (com exemplo comentado)

```python
precos = [10.00, 25.90, 5.50, 100.00]

# Jeito tradicional, com for e append (o que você já sabe fazer)
precos_com_desconto_tradicional = []
for preco in precos:
    precos_com_desconto_tradicional.append(preco * 0.9)
print(precos_com_desconto_tradicional)

# O mesmo resultado, usando list comprehension
precos_com_desconto = [preco * 0.9 for preco in precos]
print(precos_com_desconto)

# List comprehension também pode filtrar itens, usando if no final
vendas = [45.90, 120.00, 15.50, 200.00, 33.00]
vendas_grandes = [venda for venda in vendas if venda > 100]
print("Vendas grandes:", vendas_grandes)

# Combinando transformação e filtro ao mesmo tempo
vendas_grandes_com_taxa = [venda * 1.05 for venda in vendas if venda > 100]
print("Vendas grandes com taxa de 5%:", vendas_grandes_com_taxa)

# Também funciona para extrair um campo de uma lista de dicionários
catalogo = [
    {"nome": "Caneta Azul", "preco": 5.90},
    {"nome": "Caderno", "preco": 12.50},
    {"nome": "Mochila", "preco": 89.90},
]

nomes_produtos = [produto["nome"] for produto in catalogo]
print(nomes_produtos)

produtos_caros = [produto["nome"] for produto in catalogo if produto["preco"] > 10]
print("Produtos acima de R$ 10:", produtos_caros)
```

## Erros comuns de quem está começando

- Tentar fazer uma list comprehension complexa demais (com vários `if`/`else` e lógica pesada) e acabar com uma linha ilegível. Se está difícil de ler, é sinal de que um `for` tradicional é a escolha melhor.
- Esquecer os colchetes `[]` envolvendo a expressão. Sem eles, o Python interpreta a expressão de outra forma (gerador), o que foge do escopo deste tópico.
- Confundir a ordem: em list comprehension, a expressão de transformação vem **antes** do `for` (`[preco * 0.9 for preco in precos]`), o que é o oposto da ordem "natural" de um `for` tradicional.

## Exercício prático

A Loja da Ana tem a seguinte lista de vendas do dia: `[45.90, 120.00, 15.50, 200.00, 33.00, 89.90]`.

1. Usando list comprehension, crie uma nova lista `vendas_com_taxa_cartao` aplicando uma taxa de 3% (multiplicando por `1.03`) em cada venda.
2. Usando list comprehension com filtro, crie uma lista `vendas_acima_de_50` contendo só as vendas maiores que R$ 50.
3. Mostre as duas listas resultantes.

**Desafio bônus (opcional):** usando list comprehension, crie uma lista de textos formatados, tipo `"R$ 45.9"`, a partir da lista original de vendas (dica: use `str()` dentro da comprehension).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
vendas_do_dia = [45.90, 120.00, 15.50, 200.00, 33.00, 89.90]

# Aplicando taxa de 3% em todas as vendas
vendas_com_taxa_cartao = [venda * 1.03 for venda in vendas_do_dia]
print("Vendas com taxa de cartão:", vendas_com_taxa_cartao)

# Filtrando só as vendas acima de R$ 50
vendas_acima_de_50 = [venda for venda in vendas_do_dia if venda > 50]
print("Vendas acima de R$ 50:", vendas_acima_de_50)

# Desafio bônus: formatando como texto
vendas_formatadas = ["R$ " + str(venda) for venda in vendas_do_dia]
print(vendas_formatadas)
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar o que é uma list comprehension com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Sei quando é melhor usar `for` tradicional em vez de list comprehension
