# Inteiros (int)

> Módulo 1 — Fundamentos de Python · Tópico 4 de 25

## O que é e por que importa

Inteiros são números sem casa decimal: 1, 2, 100, -5, 0. Em Python, esse tipo se chama `int` (de "integer"). Pensa neles como "coisas que você conta" — quantidade de produtos vendidos, número de clientes, dias do mês. Você nunca diz "vendi 3.5 clientes hoje".

Em análise de dados, inteiros aparecem toda hora em contagens: quantas vendas aconteceram, quantos itens tem em um pedido, quantos clientes visitaram a loja. Saber que um valor é `int` também ajuda a evitar erros bobos, como tentar dividir uma quantidade de forma que dê resultado quebrado quando não faz sentido (não existe "meio cliente").

Python identifica sozinho quando um número é `int`, só de você escrever sem ponto decimal. Isso é diferente de outras ferramentas onde você precisa declarar o tipo manualmente.

## Como funciona (com exemplo comentado)

```python
# Quantidade de produtos vendidos hoje na Loja da Ana (é uma contagem, então é int)
qtd_vendida = 12

# Número de clientes que passaram pela loja
qtd_clientes = 8

# A função type() mostra qual é o tipo de uma variável
print(type(qtd_vendida))  # <class 'int'>

# Inteiros aceitam contas normalmente
total_itens_por_cliente = qtd_vendida // qtd_clientes  # divisão inteira, resultado sem casas decimais
print("Média de itens por cliente (arredondada pra baixo):", total_itens_por_cliente)

# Somar dois inteiros continua sendo inteiro
qtd_vendida_ontem = 9
total_dois_dias = qtd_vendida + qtd_vendida_ontem
print("Total vendido em dois dias:", total_dois_dias)
print(type(total_dois_dias))  # continua int
```

## Erros comuns de quem está começando

- Achar que qualquer número é `int`. Se tiver ponto decimal (mesmo `5.0`), o tipo já é `float`, não `int` — veja `05-floats.md`.
- Usar `int` para representar dinheiro. Preços quase sempre têm centavos, então o tipo certo é `float` (ou, em sistemas profissionais, tipos especiais de dinheiro — mas isso foge do escopo aqui).
- Confundir divisão normal (`/`) com divisão inteira (`//`). `//` descarta a parte decimal do resultado, o que nem sempre é o que você quer.

## Exercício prático

A Loja da Ana vendeu, em uma semana, a seguinte quantidade de unidades do produto "Caneta Azul", um valor por dia: 5, 8, 3, 10, 2, 7, 4.

1. Guarde essas quantidades em sete variáveis (uma por dia) ou some-as diretamente.
2. Calcule o total de canetas vendidas na semana.
3. Calcule quantas canetas, em média, foram vendidas por dia, usando divisão inteira (`//`).
4. Mostre os dois resultados com `print()`.

**Desafio bônus (opcional):** calcule quantos "pacotes de 6 canetas" dariam para montar com o total vendido na semana, e quantas canetas sobrariam (dica: `//` e o operador de resto, que vamos formalizar em `08-operadores-aritmeticos.md` — por ora, se quiser, pesquise sobre o operador `%`).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
# Quantidades vendidas por dia (todas inteiras, pois é contagem de unidades)
seg = 5
ter = 8
qua = 3
qui = 10
sex = 2
sab = 7
dom = 4

# Total da semana
total_semana = seg + ter + qua + qui + sex + sab + dom
print("Total vendido na semana:", total_semana)

# Média usando divisão inteira (arredonda pra baixo, ignorando casas decimais)
media_por_dia = total_semana // 7
print("Média de canetas por dia:", media_por_dia)

# Desafio bônus
pacotes_de_6 = total_semana // 6
sobra = total_semana % 6
print("Pacotes de 6 possíveis:", pacotes_de_6, "- Sobram:", sobra, "canetas")
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar o que é um `int` com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Entendo a diferença entre divisão normal e divisão inteira
