# Variáveis e print()

> Módulo 1 — Fundamentos de Python · Tópico 3 de 25

## O que é e por que importa

Uma variável é uma "caixa com nome" onde você guarda um valor para usar depois. Se você já usou uma célula do Excel (tipo `B2`), a ideia é parecida: você dá um nome a um espaço de memória e guarda algo lá dentro — só que, em vez de `B2`, você escolhe o nome, tipo `faturamento_do_dia`.

Em análise de dados, quase tudo começa guardando um dado em uma variável: o preço de um produto, o total de vendas, o nome de um cliente. Sem variáveis, você teria que reescrever o valor toda vez que precisasse dele — e não conseguiria fazer contas com valores que mudam.

A função `print()` é a forma mais simples de "mostrar" alguma coisa na tela. Pensa nela como o equivalente a olhar o resultado de uma célula do Excel: você calculou algo, e agora quer ver o resultado. Sem `print()`, o Python calcula tudo "por baixo dos panos", mas você não vê nada aparecer.

Juntas, variáveis e `print()` são a base de qualquer programa: guardar dados e mostrar resultados.

## Como funciona (com exemplo comentado)

```python
# Guardando o nome da loja em uma variável (texto/string)
nome_da_loja = "Loja da Ana"

# Guardando o faturamento do dia em uma variável (número)
faturamento_do_dia = 458.90

# Guardando quantas vendas aconteceram no dia
numero_de_vendas = 5

# print() mostra o valor na tela. Podemos passar vários itens separados por vírgula.
print("Loja:", nome_da_loja)
print("Faturamento do dia:", faturamento_do_dia)
print("Número de vendas:", numero_de_vendas)

# Variáveis podem ser reaproveitadas em contas
ticket_medio = faturamento_do_dia / numero_de_vendas
print("Ticket médio:", ticket_medio)

# Uma variável pode ser substituída por um novo valor a qualquer momento
faturamento_do_dia = 500.00
print("Faturamento atualizado:", faturamento_do_dia)
```

## Erros comuns de quem está começando

- Usar nomes de variável que não dizem nada (`x`, `a1`, `coisa`). Fica difícil ler o código depois — prefira nomes que descrevem o dado, como `faturamento_do_dia`.
- Esquecer que nomes de variável não podem começar com número nem ter espaço (`2vendas` ou `total vendas` dão erro). Use `_` no lugar do espaço: `total_vendas`.
- Achar que `print()` "guarda" o valor. Ele só mostra na tela — se quiser usar o valor depois, precisa estar em uma variável.

## Exercício prático

Crie três variáveis para representar uma venda da Loja da Ana: `produto` (o nome do produto vendido), `preco` (o preço unitário) e `quantidade` (quantas unidades foram vendidas). Depois:

1. Calcule o valor total da venda (`preco * quantidade`) e guarde em uma variável `valor_total`.
2. Use `print()` para mostrar uma mensagem parecida com: `Venda: 3x Caneta Azul - Total: R$ 15.00`.

**Desafio bônus (opcional):** crie uma segunda venda (outras três variáveis) e mostre o faturamento somado das duas vendas.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
# Dados da primeira venda
produto = "Caneta Azul"
preco = 5.00
quantidade = 3

# Calculando o total dessa venda
valor_total = preco * quantidade

# Mostrando a mensagem formatada
print("Venda:", quantidade, "x", produto, "- Total: R$", valor_total)

# Desafio bônus: segunda venda
produto_2 = "Caderno"
preco_2 = 12.50
quantidade_2 = 2
valor_total_2 = preco_2 * quantidade_2

faturamento_somado = valor_total + valor_total_2
print("Faturamento das duas vendas:", faturamento_somado)
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar o que é uma variável com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Sei usar `print()` para mostrar mais de um valor na mesma linha
