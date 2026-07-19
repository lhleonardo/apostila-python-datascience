# Condicionais (if/elif/else)

> Módulo 1 — Fundamentos de Python · Tópico 11 de 25

## O que é e por que importa

Condicional é a estrutura que faz o código tomar decisões: "se isso for verdade, faça aquilo; senão, faça outra coisa". Em Python, isso se escreve com `if` (se), `elif` (senão-se, contração de "else if") e `else` (senão). Se você já usou a função `SE()` do Excel, a ideia é idêntica — só que em Python dá para encadear quantas condições quiser, de forma mais clara.

Todos os tópicos anteriores — tipos de dado, operadores de comparação (`09-operadores-de-comparacao.md`) e operadores lógicos (`10-operadores-logicos.md`) — existiam, em parte, para chegar até aqui: eles produzem os `True`/`False` que o `if` usa para decidir qual caminho o código deve seguir.

Em análise de dados, condicionais aparecem para classificar informação: "essa venda é grande ou pequena?", "esse cliente é novo ou recorrente?", "essa nota é aprovação ou reprovação?". É a ferramenta que transforma uma regra de negócio (escrita em português) em uma decisão automática que o código toma sozinho para cada dado que ele processa.

## Como funciona (com exemplo comentado)

```python
valor_venda = 175.00

# if sozinho: só executa o bloco de baixo se a condição for True
if valor_venda > 100:
    print("Venda considerada grande")

# if/else: um caminho para True, outro para False
if valor_venda > 100:
    print("Venda grande")
else:
    print("Venda pequena")

# if/elif/else: várias faixas de classificação, verificadas em ordem
if valor_venda >= 200:
    categoria = "grande"
elif valor_venda >= 100:
    categoria = "media"
else:
    categoria = "pequena"

print("Categoria da venda:", categoria)

# Repare que a indentação (espaços no início da linha) define o que pertence a cada bloco.
# Isso não é estético -- em Python, indentação é parte da sintaxe da linguagem.
forma_pagamento = "cartao"
cliente_fidelidade = True

if valor_venda > 150 and forma_pagamento == "cartao":
    print("Cliente ganha 5% de desconto")
elif cliente_fidelidade:
    print("Cliente ganha 3% de desconto por fidelidade")
else:
    print("Sem desconto")
```

## Erros comuns de quem está começando

- Esquecer os dois-pontos (`:`) no final da linha do `if`/`elif`/`else`. Python exige isso para saber onde o bloco começa.
- Bagunçar a indentação (misturar espaços de forma inconsistente). Cada bloco dentro de um `if` precisa estar alinhado da mesma forma — o recomendado é sempre 4 espaços por nível.
- Usar vários `if` separados quando o certo seria `elif`. Com `if` separados, o Python testa todas as condições, mesmo que a primeira já tenha sido `True` — com `elif`, ele para no primeiro caminho verdadeiro, o que costuma ser o comportamento esperado e mais eficiente.

## Exercício prático

A Loja da Ana quer classificar suas vendas em três categorias:

- "grande": valor maior ou igual a R$ 200
- "média": valor entre R$ 50 (inclusive) e R$ 200 (exclusive)
- "pequena": valor menor que R$ 50

Para as vendas 35.00, 89.90 e 300.00:

1. Para cada uma, use `if`/`elif`/`else` para descobrir a categoria.
2. Mostre com `print()` o valor da venda e sua categoria.

**Desafio bônus (opcional):** adicione a regra de que, se a venda for "grande" **e** o pagamento for em dinheiro, a loja dá 5% de desconto — mostre também se o desconto se aplica.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
def classificar(venda):
    if venda >= 200:
        return "grande"
    elif venda >= 50:
        return "media"
    else:
        return "pequena"

# Nota: usamos uma função aqui só para não repetir o mesmo bloco de if/elif/else
# três vezes. Funções ainda serão formalizadas em 22-definindo-funcoes.md --
# se preferir, resolva copiando o if/elif/else três vezes, também está certo.

venda_1 = 35.00
venda_2 = 89.90
venda_3 = 300.00

print("Venda 1:", venda_1, "- Categoria:", classificar(venda_1))
print("Venda 2:", venda_2, "- Categoria:", classificar(venda_2))
print("Venda 3:", venda_3, "- Categoria:", classificar(venda_3))

# Desafio bônus
forma_pagamento = "dinheiro"
categoria_venda_3 = classificar(venda_3)

if categoria_venda_3 == "grande" and forma_pagamento == "dinheiro":
    print("Desconto de 5% aplicado")
else:
    print("Sem desconto")
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar a diferença entre `if`, `elif` e `else` com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Entendo por que a indentação é obrigatória em Python
