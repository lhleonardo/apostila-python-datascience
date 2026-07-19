# *args e **kwargs

> Módulo 1 — Fundamentos de Python · Tópico 23 de 25

## O que é e por que importa

Em `22-definindo-funcoes.md` você aprendeu a criar funções com um número fixo de parâmetros. Mas e se você não souber, de antemão, quantos valores a função vai receber? Por exemplo, uma função que soma o total de vendas, que às vezes recebe 3 valores, às vezes 10. É para isso que existem `*args` e `**kwargs` — duas formas de uma função aceitar uma quantidade variável de argumentos.

`*args` (o nome "args" é só uma convenção, o `*` é o que importa) permite que a função receba qualquer quantidade de argumentos "soltos" (posicionais), que chegam dentro da função organizados automaticamente como uma tupla (vista em `17-tuplas.md`). Já `**kwargs` permite receber qualquer quantidade de argumentos "nomeados" (`chave=valor`), organizados como um dicionário (visto em `18-dicionarios.md`) dentro da função.

Pensa em `*args` como uma caixa que aceita quantos itens quiser, sem rótulo (só a ordem importa); e `**kwargs` como uma caixa que aceita quantos itens quiser, mas cada um com uma etiqueta escrita (o nome do argumento). Você provavelmente vai usar isso com menos frequência do que funções normais no dia a dia, mas é comum encontrar em bibliotecas de análise de dados (como pandas), então vale entender a ideia.

## Como funciona (com exemplo comentado)

```python
# *args: recebe qualquer quantidade de valores "soltos", vira uma tupla dentro da função
def somar_vendas(*valores):
    print("Valores recebidos (como tupla):", valores)
    return sum(valores)

print(somar_vendas(45.90, 120.00, 15.50))          # funciona com 3 valores
print(somar_vendas(10.00, 20.00, 30.00, 40.00))    # funciona com 4 valores

# **kwargs: recebe qualquer quantidade de argumentos nomeados, vira um dicionário
def cadastrar_produto(**dados):
    print("Dados recebidos (como dicionário):", dados)
    nome = dados.get("nome", "Produto sem nome")
    preco = dados.get("preco", 0)
    print(f"Cadastrando {nome} por R$ {preco}")

cadastrar_produto(nome="Caneta Azul", preco=5.90, categoria="Papelaria")
cadastrar_produto(nome="Caderno", preco=12.50)  # funciona mesmo sem "categoria"

# É possível combinar parâmetros fixos com *args e **kwargs na mesma função
def registrar_venda(vendedor, *itens, **detalhes):
    print("Vendedor:", vendedor)
    print("Itens vendidos:", itens)
    print("Detalhes extras:", detalhes)

registrar_venda("Ana", "Caneta Azul", "Caderno", forma_pagamento="cartao", parcelas=1)
```

## Erros comuns de quem está começando

- Achar que `*args` e `**kwargs` são nomes obrigatórios. O que importa é o `*` e o `**` — você poderia escrever `*valores` ou `**dados`, como no exemplo acima; `args` e `kwargs` são só o costume mais comum entre programadores Python.
- Tentar misturar a ordem errada: parâmetros fixos vêm primeiro, depois `*args`, depois `**kwargs`. Escrever na ordem errada gera erro de sintaxe.
- Usar `*args`/`**kwargs` quando uma função com parâmetros fixos resolveria de forma mais clara. Se você sabe exatamente quantos e quais valores a função vai receber, prefira parâmetros nomeados normais — são mais fáceis de entender e de usar corretamente.

## Exercício prático

Crie uma função `calcular_faturamento_total` que aceita uma quantidade variável de valores de venda (usando `*args`) e devolve a soma de todos.

1. Defina a função usando `*args`.
2. Chame-a com três valores de vendas da Loja da Ana: 45.90, 120.00, 15.50.
3. Chame-a novamente com cinco valores diferentes, para provar que funciona com quantidades variadas.

**Desafio bônus (opcional):** crie uma função `resumo_produto` que aceita `**kwargs` e monta uma frase descrevendo o produto usando os pares chave-valor recebidos (ex: `resumo_produto(nome="Mochila", preco=89.90, cor="azul")`).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
def calcular_faturamento_total(*valores):
    return sum(valores)

faturamento_1 = calcular_faturamento_total(45.90, 120.00, 15.50)
print("Faturamento (3 vendas):", faturamento_1)

faturamento_2 = calcular_faturamento_total(10.00, 20.00, 30.00, 15.00, 5.00)
print("Faturamento (5 vendas):", faturamento_2)

# Desafio bônus
def resumo_produto(**dados):
    partes = []
    for chave, valor in dados.items():
        partes.append(f"{chave}: {valor}")
    return ", ".join(partes)

print(resumo_produto(nome="Mochila", preco=89.90, cor="azul"))
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar a diferença entre `*args` e `**kwargs` com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Entendo que `*args` vira tupla e `**kwargs` vira dicionário dentro da função
