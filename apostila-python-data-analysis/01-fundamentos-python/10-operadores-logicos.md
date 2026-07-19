# Operadores lógicos

> Módulo 1 — Fundamentos de Python · Tópico 10 de 25

## O que é e por que importa

Operadores lógicos combinam duas ou mais condições booleanas (vistas em `06-booleanos.md` e `09-operadores-de-comparacao.md`) em uma única resposta verdadeiro/falso. São três: `and` (e — todas as condições precisam ser verdadeiras), `or` (ou — basta uma condição ser verdadeira) e `not` (nega o valor: transforma `True` em `False` e vice-versa).

Pensa em `and` como uma exigência de lista: "só aprovo o empréstimo se a pessoa tiver renda comprovada E não tiver nome sujo" — as duas coisas precisam ser verdade. Já o `or` é uma alternativa: "aceito pagamento em dinheiro OU cartão" — qualquer um dos dois já resolve.

Em análise de dados, operadores lógicos são essenciais para filtros compostos: "vendas acima de R$ 100 E feitas em dinheiro", "clientes que compraram no último mês OU que gastaram mais de R$ 500 no total". Praticamente todo filtro "de verdade" em dados combina mais de uma condição, e é aí que `and`, `or` e `not` entram.

## Como funciona (com exemplo comentado)

```python
valor_venda = 180.00
forma_pagamento = "dinheiro"
cliente_fidelidade = True

# and: as duas condições precisam ser verdadeiras
venda_grande_em_dinheiro = valor_venda > 150 and forma_pagamento == "dinheiro"
print("Venda grande paga em dinheiro?", venda_grande_em_dinheiro)  # True

# or: basta uma condição ser verdadeira
merece_desconto = valor_venda > 200 or cliente_fidelidade
print("Merece desconto?", merece_desconto)  # True, porque cliente_fidelidade é True

# not: inverte o valor booleano
nao_e_fidelidade = not cliente_fidelidade
print("Cliente não é fidelidade?", nao_e_fidelidade)  # False

# Combinando os três operadores (parênteses ajudam a deixar a ordem clara)
promocao_valida = (valor_venda >= 100 and forma_pagamento == "dinheiro") or cliente_fidelidade
print("Promoção válida?", promocao_valida)

# and e or "curto-circuitam": param assim que já sabem a resposta.
# Em "False and ...", o Python nem avalia o resto, porque já sabe que é False.
estoque = 0
tem_estoque_e_preco_valido = estoque > 0 and (100 / estoque > 5)  # não quebra, pois para no primeiro False
print("Tem estoque e preço válido?", tem_estoque_e_preco_valido)
```

## Erros comuns de quem está começando

- Usar `&` e `|` no lugar de `and` e `or`. Esses símbolos existem em Python, mas têm outro significado (operações bit a bit) e não devem ser usados aqui neste contexto — o correto para lógica booleana comum é escrever a palavra `and`/`or`.
- Esquecer parênteses em expressões com `and` e `or` misturados, o que pode gerar um resultado diferente do esperado. Quando tiver dúvida, agrupe com `()` para deixar a intenção clara.
- Escrever `not (x == y)` quando dava para simplificar com `x != y`, deixando o código mais difícil de ler sem necessidade.

## Exercício prático

A Loja da Ana quer identificar vendas que merecem um cupom de desconto na próxima compra. A regra é: o cupom é dado se a venda foi maior que R$ 200 **e** o pagamento foi em cartão, **ou** se o cliente já é fidelidade (independente do valor).

Considere os dados de uma venda:

```python
valor_venda = 250.00
forma_pagamento = "cartao"
cliente_fidelidade = False
```

1. Escreva uma expressão lógica que combine as três informações seguindo a regra acima.
2. Guarde o resultado em uma variável `merece_cupom` e mostre com `print()`.
3. Repita o exercício com `valor_venda = 90.00`, `forma_pagamento = "dinheiro"`, `cliente_fidelidade = True`.

**Desafio bônus (opcional):** adicione a regra "e não é a primeira compra da pessoa" (`primeira_compra = False` para valer o desconto) combinando com `not`.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
# Caso 1
valor_venda = 250.00
forma_pagamento = "cartao"
cliente_fidelidade = False

merece_cupom = (valor_venda > 200 and forma_pagamento == "cartao") or cliente_fidelidade
print("Caso 1 - Merece cupom?", merece_cupom)  # True (bateu a primeira condição)

# Caso 2
valor_venda = 90.00
forma_pagamento = "dinheiro"
cliente_fidelidade = True

merece_cupom = (valor_venda > 200 and forma_pagamento == "cartao") or cliente_fidelidade
print("Caso 2 - Merece cupom?", merece_cupom)  # True (é fidelidade)

# Desafio bônus
primeira_compra = False
merece_cupom_final = merece_cupom and not primeira_compra
print("Merece cupom (considerando não ser primeira compra)?", merece_cupom_final)
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar a diferença entre `and` e `or` com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Sei usar `not` para inverter uma condição
