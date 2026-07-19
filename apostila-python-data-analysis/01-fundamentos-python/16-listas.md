# Listas

> Módulo 1 — Fundamentos de Python · Tópico 16 de 25

## O que é e por que importa

Lista é uma coleção ordenada de valores, guardada em uma única variável. Pensa nela como uma coluna inteira de uma planilha, em vez de uma célula só: em vez de ter `venda_1`, `venda_2`, `venda_3` como variáveis separadas (como fizemos em tópicos anteriores), você guarda tudo em uma única lista, `vendas = [45.90, 120.00, 15.50]`.

Isso muda tudo na prática: com uma lista, você pode usar um `for` (visto em `12-loops.md`) para processar cada valor automaticamente, não importa se são 3 vendas ou 3 mil. É exatamente assim que análise de dados funciona de verdade — você quase nunca sabe de antemão quantos registros vai ter, então precisa de uma estrutura que cresça e seja percorrida de forma genérica.

Listas em Python podem guardar qualquer tipo de dado (números, textos, booleanos, até outras listas), e são "mutáveis" — ou seja, dá para adicionar, remover e alterar itens depois de criadas.

## Como funciona (com exemplo comentado)

```python
# Lista com o valor de cada venda do dia, na Loja da Ana
vendas_do_dia = [45.90, 120.00, 15.50, 200.00, 33.00]

# len() mede quantos itens tem na lista
qtd_vendas = len(vendas_do_dia)
print("Número de vendas:", qtd_vendas)

# Acesso por índice, igual em strings (começa em 0)
primeira_venda = vendas_do_dia[0]
ultima_venda = vendas_do_dia[-1]
print("Primeira venda:", primeira_venda, "- Última venda:", ultima_venda)

# Percorrendo a lista inteira com for
for venda in vendas_do_dia:
    print("Processando venda de R$", venda)

# Funções prontas que funcionam direto em listas de números
print("Total do dia:", sum(vendas_do_dia))
print("Maior venda:", max(vendas_do_dia))
print("Menor venda:", min(vendas_do_dia))

# Adicionando um novo item ao final da lista
vendas_do_dia.append(89.00)
print("Depois de adicionar uma venda:", vendas_do_dia)

# Removendo um item específico
vendas_do_dia.remove(15.50)
print("Depois de remover a venda de 15.50:", vendas_do_dia)

# Fatiamento funciona igual em strings: pega um pedaço da lista
tres_primeiras = vendas_do_dia[0:3]
print("Três primeiras vendas:", tres_primeiras)

# Listas podem guardar qualquer tipo, inclusive misturado
produto = ["Caneta Azul", 5.90, 10, True]  # nome, preço, quantidade, ativo
print(produto)
```

## Erros comuns de quem está começando

- Tentar acessar um índice que não existe (`vendas_do_dia[10]` em uma lista de 5 itens), o que gera erro `IndexError`. Sempre confira o tamanho com `len()` quando tiver dúvida.
- Confundir `append()` (adiciona um item ao final) com tentar simplesmente somar (`lista + valor`), que não funciona da forma esperada para adicionar um único item.
- Esquecer que listas são "mutáveis": se duas variáveis apontam para a mesma lista, alterar uma afeta a outra. Isso é sutil e será revisitado com mais detalhe adiante — por ora, saiba que existe.

## Exercício prático

A Loja da Ana registrou as seguintes vendas em um dia: `[45.90, 120.00, 15.50, 200.00, 33.00, 89.90]`.

1. Guarde essas vendas em uma lista chamada `vendas_do_dia`.
2. Use `sum()` para calcular o faturamento total do dia.
3. Use `max()` e `min()` para descobrir a maior e a menor venda.
4. Use um `for` para mostrar cada venda, indicando se ela é maior que R$ 100 ou não.

**Desafio bônus (opcional):** adicione uma nova venda de R$ 75.00 à lista com `append()` e recalcule o faturamento total.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
vendas_do_dia = [45.90, 120.00, 15.50, 200.00, 33.00, 89.90]

# Faturamento total
faturamento_total = sum(vendas_do_dia)
print("Faturamento total:", faturamento_total)

# Maior e menor venda
maior_venda = max(vendas_do_dia)
menor_venda = min(vendas_do_dia)
print("Maior venda:", maior_venda, "- Menor venda:", menor_venda)

# Classificando cada venda
for venda in vendas_do_dia:
    if venda > 100:
        print(f"Venda de R$ {venda} - Grande")
    else:
        print(f"Venda de R$ {venda} - Pequena")

# Desafio bônus
vendas_do_dia.append(75.00)
novo_faturamento_total = sum(vendas_do_dia)
print("Novo faturamento total:", novo_faturamento_total)
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar o que é uma lista com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Sei usar `append()`, `sum()`, `max()` e `min()` em uma lista
