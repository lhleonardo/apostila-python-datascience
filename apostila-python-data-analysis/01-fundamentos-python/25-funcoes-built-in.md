# Funções built-in (len, sum, map, filter, etc.)

> Módulo 1 — Fundamentos de Python · Tópico 25 de 25

## O que é e por que importa

Funções built-in ("embutidas") são funções que já vêm prontas no Python, sem você precisar defini-las nem importar nada. Você já usou várias ao longo desta apostila — `print()`, `len()`, `type()`, `int()`, `float()`, `sum()`, `max()`, `min()`, `sorted()` — mas ainda não tinha esse nome formal para o grupo. Este é o último tópico do Módulo 1, e serve para consolidar essas ferramentas e apresentar duas que faltavam: `map()` e `filter()`.

Pensa nas built-ins como os "eletrodomésticos de fábrica" da cozinha: já vêm instalados, prontos para usar, e resolvem tarefas tão comuns que não faria sentido cada pessoa reinventar a sua própria versão. `map()` aplica uma função a cada item de uma coleção (parecido com o que list comprehensions fazem, visto em `20-list-comprehensions.md`); `filter()` seleciona só os itens que passam em uma condição (parecido com list comprehension com `if`).

Dominar essas funções builtin, combinadas com o que você aprendeu sobre lambda (`24-funcoes-lambda.md`) e funções próprias (`22-definindo-funcoes.md`), fecha o ciclo de fundamentos: a partir do Módulo 2, você vai aplicar tudo isso em bibliotecas como pandas, que são construídas em cima dessas mesmas ideias.

## Como funciona (com exemplo comentado)

```python
vendas = [45.90, 120.00, 15.50, 200.00, 33.00, 89.90]

# Revisão rápida das built-ins mais usadas até aqui
print(len(vendas))    # 6 -- quantidade de itens
print(sum(vendas))    # soma de todos os valores
print(max(vendas))    # maior valor
print(min(vendas))    # menor valor
print(sorted(vendas)) # nova lista ordenada, sem alterar a original

# map(): aplica uma função a cada item de uma coleção, devolvendo um "map object"
# que normalmente convertemos para list() para poder ver/usar
vendas_com_taxa = list(map(lambda venda: venda * 1.05, vendas))
print("Vendas com taxa de 5%:", vendas_com_taxa)

# O mesmo resultado poderia ser feito com list comprehension (visto em 20-list-comprehensions.md)
vendas_com_taxa_v2 = [venda * 1.05 for venda in vendas]
print(vendas_com_taxa_v2 == vendas_com_taxa)  # True, mesmo resultado, formas diferentes

# filter(): mantém só os itens que passam em uma condição (função que devolve True/False)
vendas_grandes = list(filter(lambda venda: venda > 100, vendas))
print("Vendas grandes:", vendas_grandes)

# round() arredonda, já visto em 05-floats.md -- reforçando aqui como built-in
print(round(45.678, 1))  # 45.7

# any() e all() são úteis para checagens em lote
tem_venda_acima_de_150 = any(venda > 150 for venda in vendas)
print("Alguma venda acima de R$ 150?", tem_venda_acima_de_150)

todas_vendas_positivas = all(venda > 0 for venda in vendas)
print("Todas as vendas são positivas?", todas_vendas_positivas)
```

## Erros comuns de quem está começando

- Esquecer de converter o resultado de `map()` e `filter()` para `list()` antes de usar. Sem essa conversão, você tem um objeto especial que ainda não "virou" a lista de valores propriamente dita para imprimir ou percorrer normalmente.
- Achar que `map()`/`filter()` são obrigatoriamente melhores que list comprehension. Na prática, muitos programadores Python preferem list comprehension por ser mais legível — vale conhecer as duas formas e escolher a que ficar mais clara para o seu caso.
- Usar `sum()` em uma lista que contém texto misturado com número, o que gera erro (`sum()` só funciona em coleções totalmente numéricas).

## Exercício prático

A Loja da Ana tem a seguinte lista de vendas do mês: `[45.90, 120.00, 15.50, 200.00, 33.00, 89.90, 310.00]`.

1. Use `sum()` e `len()` para calcular o ticket médio das vendas (faturamento total dividido pela quantidade de vendas).
2. Use `filter()` com uma lambda para obter apenas as vendas acima do ticket médio calculado.
3. Use `map()` com uma lambda para criar uma lista com 5% de comissão sobre cada venda acima do ticket médio.
4. Mostre o ticket médio, as vendas acima da média e os valores de comissão.

**Desafio bônus (opcional):** use `any()` para checar se existe alguma venda acima de R$ 300, e `all()` para checar se todas as vendas são maiores que R$ 10.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
vendas = [45.90, 120.00, 15.50, 200.00, 33.00, 89.90, 310.00]

# Ticket médio
ticket_medio = sum(vendas) / len(vendas)
print("Ticket médio:", round(ticket_medio, 2))

# Vendas acima do ticket médio, usando filter()
vendas_acima_da_media = list(filter(lambda venda: venda > ticket_medio, vendas))
print("Vendas acima da média:", vendas_acima_da_media)

# Comissão de 5% sobre essas vendas, usando map()
comissoes = list(map(lambda venda: round(venda * 0.05, 2), vendas_acima_da_media))
print("Comissões (5%):", comissoes)

# Desafio bônus
tem_venda_acima_de_300 = any(venda > 300 for venda in vendas)
todas_acima_de_10 = all(venda > 10 for venda in vendas)

print("Alguma venda acima de R$ 300?", tem_venda_acima_de_300)
print("Todas as vendas acima de R$ 10?", todas_acima_de_10)
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar o que `map()` e `filter()` fazem com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Terminei o Módulo 1 e me sinto pronto para seguir para o Módulo 2
