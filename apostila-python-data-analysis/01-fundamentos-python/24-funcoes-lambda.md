# Funções lambda

> Módulo 1 — Fundamentos de Python · Tópico 24 de 25

## O que é e por que importa

Função lambda é uma forma de criar uma função pequena, sem nome, em uma única linha — usada quando você precisa de uma lógica simples e rápida, geralmente para usar uma única vez ou passar como argumento para outra função. É uma alternativa mais curta ao `def` (visto em `22-definindo-funcoes.md`), reservada para casos bem simples.

Pensa em lambda como um "post-it" comparado a um "manual de instruções": se a lógica é tão simples que caberia em uma frase (como "multiplique por 2" ou "pegue o preço"), às vezes não vale a pena escrever uma função `def` completa com nome — um lambda resolve rapidinho, sem burocracia.

Em análise de dados, lambdas aparecem com muita frequência dentro de funções que esperam receber "uma regra" como argumento — por exemplo, dizer para o Python "ordene esta lista de produtos, mas pelo preço, não pelo nome" ou "aplique esta transformação em cada valor". Isso conecta diretamente com `25-funcoes-built-in.md`, onde `map()`, `filter()` e `sorted()` costumam usar lambda lado a lado.

## Como funciona (com exemplo comentado)

```python
# Uma função def tradicional, simples
def dobro(numero):
    return numero * 2

print(dobro(5))  # 10

# A mesma lógica, como lambda -- sem nome, sem "def", sem "return" explícito
dobro_lambda = lambda numero: numero * 2
print(dobro_lambda(5))  # 10

# Lambda pode receber mais de um parâmetro, separados por vírgula
calcular_total = lambda preco, quantidade: preco * quantidade
print(calcular_total(5.90, 3))  # 17.7

# O uso mais comum de lambda é como argumento de outra função, sem precisar
# nomear a função separadamente. Exemplo: ordenar uma lista de produtos pelo preço
produtos = [
    {"nome": "Mochila", "preco": 89.90},
    {"nome": "Caneta Azul", "preco": 5.90},
    {"nome": "Caderno", "preco": 12.50},
]

# sorted() aceita um parâmetro "key" -- uma função que diz "pelo que ordenar"
produtos_por_preco = sorted(produtos, key=lambda produto: produto["preco"])
for produto in produtos_por_preco:
    print(produto["nome"], "-", produto["preco"])

# Sem lambda, seria preciso definir uma função separada só para isso:
def pegar_preco(produto):
    return produto["preco"]

produtos_por_preco_v2 = sorted(produtos, key=pegar_preco)  # mesmo resultado
```

## Erros comuns de quem está começando

- Tentar escrever lógica complexa dentro de um lambda (com `if`/`elif`/`else` de várias linhas, laços, etc.). Lambda só aceita uma única expressão — se a lógica é complicada, use `def` normal.
- Esquecer que lambda não usa a palavra `return`: o valor depois dos dois-pontos já é devolvido automaticamente.
- Usar lambda "porque parece mais profissional", mesmo quando uma função `def` nomeada deixaria o código mais legível. Lambda é uma ferramenta de conveniência, não uma obrigação — clareza vem sempre primeiro.

## Exercício prático

A Loja da Ana tem a seguinte lista de produtos:

```python
produtos = [
    {"nome": "Mochila", "preco": 89.90},
    {"nome": "Caneta Azul", "preco": 5.90},
    {"nome": "Caderno", "preco": 12.50},
    {"nome": "Borracha", "preco": 2.25},
]
```

1. Use `sorted()` com uma lambda para ordenar os produtos do mais barato para o mais caro.
2. Use `sorted()` novamente, mas com `reverse=True`, para ordenar do mais caro para o mais barato.
3. Mostre os nomes dos produtos, na ordem resultante, em cada um dos dois casos.

**Desafio bônus (opcional):** crie uma lambda que recebe um produto e devolve `True` se o preço for maior que R$ 10 (útil para usar depois com `filter()`, que veremos em `25-funcoes-built-in.md`).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
produtos = [
    {"nome": "Mochila", "preco": 89.90},
    {"nome": "Caneta Azul", "preco": 5.90},
    {"nome": "Caderno", "preco": 12.50},
    {"nome": "Borracha", "preco": 2.25},
]

# Ordenando do mais barato para o mais caro
produtos_crescente = sorted(produtos, key=lambda produto: produto["preco"])
print("Do mais barato para o mais caro:")
for produto in produtos_crescente:
    print("-", produto["nome"])

# Ordenando do mais caro para o mais barato
produtos_decrescente = sorted(produtos, key=lambda produto: produto["preco"], reverse=True)
print("Do mais caro para o mais barato:")
for produto in produtos_decrescente:
    print("-", produto["nome"])

# Desafio bônus
produto_caro = lambda produto: produto["preco"] > 10
print(produto_caro(produtos[0]))  # True, Mochila custa 89.90
print(produto_caro(produtos[3]))  # False, Borracha custa 2.25
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar o que é uma função lambda e quando usá-la com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Sei usar lambda junto com `sorted()` e o parâmetro `key`
