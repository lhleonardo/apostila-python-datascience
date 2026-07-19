# Operadores de comparação

> Módulo 1 — Fundamentos de Python · Tópico 9 de 25

## O que é e por que importa

Operadores de comparação são os símbolos que comparam dois valores e respondem com um booleano (`True` ou `False`, vistos em `06-booleanos.md`): `==` (igual), `!=` (diferente), `>` (maior), `<` (menor), `>=` (maior ou igual), `<=` (menor ou igual). É a forma de o código responder perguntas do tipo "esse valor é maior que aquele?".

Em análise de dados, comparações são a base para filtrar e classificar informação: "quais vendas foram acima de R$ 100?", "esse cliente é o mesmo que já comprou antes?", "o estoque está abaixo do mínimo?". Sem comparação, não dá para separar dados "bons" de dados "ruins", nem tomar decisão nenhuma no código.

Um erro clássico de quem está começando (em quase todas as linguagens, não só Python) é confundir `=` com `==`. O `=` (um sinal só) guarda um valor em uma variável, ensinado em `03-variaveis-e-print.md`. O `==` (dois sinais) compara dois valores e diz se são iguais. São operações completamente diferentes, apesar de parecidas visualmente.

## Como funciona (com exemplo comentado)

```python
preco_produto_a = 25.90
preco_produto_b = 18.50
meta_de_venda = 1000.00
faturamento_do_dia = 950.00

# == compara igualdade (não confundir com = de atribuição)
mesmo_preco = preco_produto_a == preco_produto_b
print("Produtos com mesmo preço?", mesmo_preco)  # False

# != verifica diferença
precos_diferentes = preco_produto_a != preco_produto_b
print("Preços diferentes?", precos_diferentes)  # True

# > e < comparam grandeza
produto_a_mais_caro = preco_produto_a > preco_produto_b
print("Produto A é mais caro?", produto_a_mais_caro)  # True

# >= e <= incluem o caso de igualdade
bateu_a_meta = faturamento_do_dia >= meta_de_venda
print("Bateu a meta (ou empatou)?", bateu_a_meta)  # False

# Comparações também funcionam com texto (ordem alfabética) e são muito usadas em condicionais (ainda vamos ver em 11-condicionais.md)
cliente_1 = "Ana"
cliente_2 = "Bruno"
print(cliente_1 < cliente_2)  # True, "Ana" vem antes de "Bruno" no alfabeto
```

## Erros comuns de quem está começando

- Usar `=` (atribuição) quando o objetivo era `==` (comparação). `if faturamento = 100:` dá erro de sintaxe — o certo é `if faturamento == 100:`.
- Comparar float com `==` esperando exatidão perfeita, como visto em `05-floats.md` (`0.1 + 0.2 == 0.3` dá `False`). Para floats, é mais seguro comparar com uma margem de tolerância ou arredondar antes.
- Esquecer que comparação de texto (`"Ana" < "Bruno"`) é sensível a maiúsculas/minúsculas — `"ana" < "Bruno"` pode não se comportar como esperado, porque letras maiúsculas e minúsculas têm códigos diferentes internamente.

## Exercício prático

A Loja da Ana define que uma venda é "grande" quando o valor total é maior ou igual a R$ 150.00. Considere as vendas: 89.90, 150.00, 210.50, 45.00.

1. Para cada valor, use um operador de comparação para verificar se a venda é "grande" (maior ou igual a 150.00) e guarde o resultado em uma variável booleana.
2. Mostre, para cada venda, o valor e se ela é grande ou não, usando `print()`.

**Desafio bônus (opcional):** compare o total de vendas do dia (some as quatro) com a meta diária de R$ 400.00, e mostre se a meta foi batida.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
venda_1 = 89.90
venda_2 = 150.00
venda_3 = 210.50
venda_4 = 45.00

limite_venda_grande = 150.00

# Comparando cada venda com o limite
venda_1_grande = venda_1 >= limite_venda_grande
venda_2_grande = venda_2 >= limite_venda_grande
venda_3_grande = venda_3 >= limite_venda_grande
venda_4_grande = venda_4 >= limite_venda_grande

print("Venda 1:", venda_1, "- Grande?", venda_1_grande)
print("Venda 2:", venda_2, "- Grande?", venda_2_grande)
print("Venda 3:", venda_3, "- Grande?", venda_3_grande)
print("Venda 4:", venda_4, "- Grande?", venda_4_grande)

# Desafio bônus
total_do_dia = venda_1 + venda_2 + venda_3 + venda_4
meta_diaria = 400.00
bateu_meta = total_do_dia >= meta_diaria
print("Total do dia:", total_do_dia, "- Bateu a meta?", bateu_meta)
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar a diferença entre `=` e `==` com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Sei usar `>=` e `<=` corretamente
