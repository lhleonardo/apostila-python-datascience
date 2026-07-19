# Loops (for/while)

> Módulo 1 — Fundamentos de Python · Tópico 12 de 25

## O que é e por que importa

Loop é uma estrutura que repete um bloco de código várias vezes, sem você precisar copiar e colar a mesma instrução. Pensa em quando você arrasta uma fórmula do Excel para baixo, aplicando o mesmo cálculo em cada linha da planilha — um loop faz isso, só que de forma explícita no código.

Python tem dois tipos principais: `for`, que repete um número definido de vezes (por exemplo, "uma vez para cada venda na lista de vendas"), e `while`, que repete enquanto uma condição continuar sendo verdadeira (por exemplo, "enquanto o estoque não tiver acabado").

Loops são um dos motivos pelos quais programação é tão poderosa para análise de dados: em vez de calcular manualmente o total de 500 vendas uma por uma, você escreve a regra de cálculo uma vez e deixa o `for` aplicar essa regra a cada item automaticamente. Neste tópico, ainda vamos usar loops com dados simples (sequências de números); em `16-listas.md` você vai ver como combinar `for` com listas de verdade, o que é onde loops realmente brilham.

## Como funciona (com exemplo comentado)

```python
# for com range(): repete um número definido de vezes
# range(5) gera os números 0, 1, 2, 3, 4 (começa em 0, não inclui o 5)
for dia in range(5):
    print("Processando dados do dia", dia)

# range(inicio, fim) permite escolher onde começar
for dia in range(1, 6):  # 1, 2, 3, 4, 5
    print("Dia", dia, "de vendas")

# Loops são ótimos para acumular um resultado, como somar vendas
faturamento_total = 0
vendas_do_dia = 150  # imaginando o mesmo valor todo dia, por simplicidade
for dia in range(1, 8):
    faturamento_total = faturamento_total + vendas_do_dia
print("Faturamento estimado da semana:", faturamento_total)

# while: repete enquanto a condição for True
estoque = 5
vendas_feitas = 0
while estoque > 0:
    print("Vendendo 1 unidade. Estoque restante:", estoque - 1)
    estoque = estoque - 1
    vendas_feitas = vendas_feitas + 1

print("Total de vendas até esgotar o estoque:", vendas_feitas)

# Cuidado: while precisa de uma condição que eventualmente vire False,
# senão o loop nunca para (loop infinito) -- por isso sempre atualizamos
# a variável "estoque" dentro do próprio loop.
```

## Erros comuns de quem está começando

- Esquecer de atualizar a variável de controle dentro do `while`, criando um loop infinito que nunca termina (o programa "trava").
- Achar que `range(5)` começa em 1. Ele começa em 0 e não inclui o número final — `range(5)` gera 0, 1, 2, 3, 4 (cinco números no total).
- Usar `while` quando `for` resolveria de forma mais simples. Se você já sabe quantas vezes quer repetir, `for` costuma ser a escolha mais clara; `while` é melhor quando a repetição depende de uma condição que só se resolve durante a execução.

## Exercício prático

A Loja da Ana quer saber quanto teria faturado ao longo de 6 dias, sabendo que o faturamento cresce R$ 20,00 por dia a partir de uma base de R$ 100,00 no primeiro dia (dia 1: R$ 100, dia 2: R$ 120, dia 3: R$ 140, e assim por diante).

1. Use um `for` com `range()` para simular os 6 dias.
2. A cada dia, calcule o faturamento daquele dia e some em uma variável `faturamento_total`.
3. Ao final, mostre o faturamento total da semana.

**Desafio bônus (opcional):** usando `while`, simule quantos dias são necessários para o faturamento acumulado ultrapassar R$ 900,00, mantendo a mesma regra de crescimento.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
faturamento_total = 0
faturamento_base = 100
crescimento_por_dia = 20

for dia in range(1, 7):  # dias 1 a 6
    faturamento_do_dia = faturamento_base + (dia - 1) * crescimento_por_dia
    faturamento_total = faturamento_total + faturamento_do_dia
    print("Dia", dia, "- Faturamento:", faturamento_do_dia)

print("Faturamento total da semana:", faturamento_total)

# Desafio bônus: usando while para achar quando ultrapassa R$ 900
faturamento_acumulado = 0
dia = 1

while faturamento_acumulado <= 900:
    faturamento_do_dia = faturamento_base + (dia - 1) * crescimento_por_dia
    faturamento_acumulado = faturamento_acumulado + faturamento_do_dia
    dia = dia + 1

# dia - 1 porque incrementamos antes de sair do loop
print("Dias necessários para ultrapassar R$ 900:", dia - 1)
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar a diferença entre `for` e `while` com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Entendo por que um `while` mal escrito pode virar um loop infinito
