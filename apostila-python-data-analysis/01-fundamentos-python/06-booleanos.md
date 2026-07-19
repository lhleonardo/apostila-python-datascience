# Booleanos

> Módulo 1 — Fundamentos de Python · Tópico 6 de 25

## O que é e por que importa

Booleano é um tipo de dado que só tem dois valores possíveis: `True` (verdadeiro) ou `False` (falso). Em Python o tipo se chama `bool`. Pensa nele como um interruptor de luz: ou está ligado, ou está desligado — não existe meio-termo.

Isso pode parecer um tipo "sem graça" perto de números e textos, mas é a base para tomar decisões no código: "essa venda foi acima de R$ 100?", "o cliente é novo?", "o estoque acabou?". Toda pergunta que se responde com sim/não vira, no Python, um `True`/`False`.

Booleanos ganham muita força quando combinados com comparações (`10 > 5` já resulta em um booleano) e com condicionais (`if`), que vamos ver em `09-operadores-de-comparacao.md` e `11-condicionais.md`. Por ora, o importante é entender que é um tipo de dado como qualquer outro — você pode guardar um booleano em uma variável, mostrar com `print()`, e usar em contas.

## Como funciona (com exemplo comentado)

```python
# Um booleano guardando se uma venda foi feita à vista
venda_a_vista = True

# Um booleano guardando se o estoque de um produto acabou
estoque_zerado = False

print(venda_a_vista)   # True
print(type(venda_a_vista))  # <class 'bool'>

# Comparações já retornam um booleano diretamente
faturamento_do_dia = 458.90
meta_do_dia = 400.00

bateu_meta = faturamento_do_dia > meta_do_dia
print("Bateu a meta?", bateu_meta)  # True

# Curiosidade: internamente, True equivale a 1 e False equivale a 0
print(True + True)   # 2
print(bateu_meta * 10)  # 10, porque True vale 1
```

## Erros comuns de quem está começando

- Escrever `"True"` (como texto) em vez de `True` (o valor booleano de verdade). São coisas diferentes: uma é string, outra é `bool`.
- Comparar um booleano com `== True` (ex: `if bateu_meta == True:`), quando basta usar `if bateu_meta:` — é redundante e menos legível.
- Achar que booleano é só usado dentro de `if`. Ele é um valor comum, pode ser guardado em variável, em lista, retornado por uma função etc.

## Exercício prático

A Loja da Ana teve, em um dia, faturamento de R$ 620.00, e a meta do dia era R$ 500.00. Além disso, o número de clientes atendidos foi 15, e a meta de clientes era 20.

1. Crie uma variável booleana `bateu_meta_faturamento` guardando se o faturamento passou da meta.
2. Crie uma variável booleana `bateu_meta_clientes` guardando se o número de clientes passou da meta.
3. Mostre as duas com `print()`, com uma mensagem explicando o que cada uma representa.

**Desafio bônus (opcional):** conte quantas das duas metas foram batidas, somando os dois booleanos (lembre que `True` vale 1 e `False` vale 0).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
# Dados do dia
faturamento_do_dia = 620.00
meta_faturamento = 500.00

clientes_atendidos = 15
meta_clientes = 20

# Comparações resultam diretamente em booleanos
bateu_meta_faturamento = faturamento_do_dia > meta_faturamento
bateu_meta_clientes = clientes_atendidos > meta_clientes

print("Bateu meta de faturamento?", bateu_meta_faturamento)
print("Bateu meta de clientes?", bateu_meta_clientes)

# Desafio bônus: contando quantas metas foram batidas (True=1, False=0)
metas_batidas = bateu_meta_faturamento + bateu_meta_clientes
print("Quantidade de metas batidas:", metas_batidas)
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar o que é um booleano com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Entendo que uma comparação (como `>`) já produz um valor booleano
