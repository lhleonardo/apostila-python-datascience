# Floats

> Módulo 1 — Fundamentos de Python · Tópico 5 de 25

## O que é e por que importa

Float é o tipo de número que tem casa decimal: 5.90, 12.5, 0.33, -1.75. O nome vem de "ponto flutuante" (floating point), uma forma de representar números com parte fracionária. Na prática, pense em floats como "números que você mede", em vez de "números que você conta" (isso é o `int`, visto em `04-inteiros.md`).

Em análise de dados, floats aparecem em quase todo lugar que envolve dinheiro, médias, porcentagens e medidas: preço de um produto, nota média de avaliação, temperatura, ticket médio de vendas. Se um dado pode ter "meio", provavelmente é float.

Um detalhe importante (e que confunde muita gente): por causa de como computadores guardam números decimais, contas com float às vezes dão resultados "estranhos", tipo `0.1 + 0.2` resultando em `0.30000000000000004` em vez de `0.3` certinho. Isso não é um bug do seu código — é uma limitação conhecida de como float funciona em praticamente toda linguagem de programação, e existem formas de contornar (como arredondar o resultado).

## Como funciona (com exemplo comentado)

```python
# Preço de produtos da Loja da Ana (dinheiro sempre tem casa decimal, então é float)
preco_caneta = 5.00
preco_caderno = 12.50

# type() confirma que são floats
print(type(preco_caneta))  # <class 'float'>

# Contas entre floats resultam em float
total = preco_caneta + preco_caderno
print("Total:", total)

# Misturar int com float também vira float (Python "promove" o resultado)
quantidade = 3  # int
valor_total_canetas = preco_caneta * quantidade
print("Valor total canetas:", valor_total_canetas, "-", type(valor_total_canetas))

# Cuidado com imprecisão de float em contas repetidas
resultado_estranho = 0.1 + 0.2
print(resultado_estranho)  # 0.30000000000000004

# A função round() arredonda para um número de casas decimais, contornando o problema
print(round(resultado_estranho, 2))  # 0.3
```

## Erros comuns de quem está começando

- Comparar dois floats com `==` esperando exatidão perfeita (ex.: `0.1 + 0.2 == 0.3` dá `False` por causa da imprecisão citada acima). O jeito seguro é arredondar antes de comparar, com `round()`.
- Achar que float sempre mostra as casas decimais que você escreveu. `5.00` pode aparecer como `5.0` na tela — o valor é o mesmo, só a exibição muda.
- Usar float para IDs ou códigos (tipo "código do produto 007"). Se não faz sentido ter meio valor, provavelmente não devia ser float.

## Exercício prático

A Loja da Ana vendeu os seguintes produtos em um dia, com seus preços:

- Caneta Azul: R$ 3.50
- Caderno: R$ 12.90
- Borracha: R$ 2.25

1. Guarde os três preços em variáveis float.
2. Calcule o total da compra (soma dos três).
3. Arredonde o total para 2 casas decimais usando `round()` e mostre com `print()`.

**Desafio bônus (opcional):** calcule quanto seria o total com um desconto de 10% (multiplique o total por `0.9`) e arredonde o resultado.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
# Preços dos produtos (floats, pois envolvem centavos)
preco_caneta = 3.50
preco_caderno = 12.90
preco_borracha = 2.25

# Somando o total da compra
total = preco_caneta + preco_caderno + preco_borracha

# Arredondando para 2 casas decimais (padrão de dinheiro)
total_arredondado = round(total, 2)
print("Total da compra:", total_arredondado)

# Desafio bônus: aplicando 10% de desconto
total_com_desconto = round(total * 0.9, 2)
print("Total com desconto de 10%:", total_com_desconto)
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar a diferença entre `int` e `float` com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Entendo por que contas com float às vezes dão resultados "estranhos" e como o `round()` ajuda
