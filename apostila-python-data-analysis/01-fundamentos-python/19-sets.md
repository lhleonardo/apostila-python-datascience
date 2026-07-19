# Sets

> Módulo 1 — Fundamentos de Python · Tópico 19 de 25

## O que é e por que importa

Set (conjunto) é uma coleção de valores parecida com lista, mas com duas diferenças importantes: não guarda itens duplicados, e não mantém uma ordem garantida. Pensa em set como uma "lista de presença" onde cada nome só pode aparecer uma vez, mesmo que a pessoa tente se cadastrar de novo.

Em análise de dados, sets resolvem um problema muito comum: descobrir os valores únicos de uma coluna. Por exemplo, se você tem uma lista com o produto de cada venda do mês, e quer saber "quais produtos diferentes foram vendidos" (sem repetição), transformar essa lista em set já te dá a resposta na hora, sem precisar escrever um loop manual para eliminar duplicatas.

Sets também são ótimos para operações de comparação entre grupos: "quais clientes compraram em janeiro E em fevereiro" (interseção), "quais produtos existem na loja A OU na loja B" (união), "quais clientes compraram em janeiro mas NÃO em fevereiro" (diferença). Essas operações, feitas na mão com listas e `for`, dariam bem mais trabalho.

## Como funciona (com exemplo comentado)

```python
# Lista de produtos vendidos ao longo do dia (com repetição)
produtos_vendidos = ["Caneta Azul", "Caderno", "Caneta Azul", "Borracha", "Caderno", "Caneta Azul"]

# set() remove as repetições automaticamente
produtos_unicos = set(produtos_vendidos)
print(produtos_unicos)  # {'Caneta Azul', 'Caderno', 'Borracha'} -- ordem pode variar

print("Quantidade de produtos diferentes vendidos:", len(produtos_unicos))

# in funciona em sets, e costuma ser mais rápido do que em listas grandes
print("Vendemos Borracha hoje?", "Borracha" in produtos_unicos)

# Sets também podem ser criados diretamente com chaves {}
clientes_janeiro = {"Ana", "Bruno", "Carla"}
clientes_fevereiro = {"Bruno", "Carla", "Diego"}

# Interseção: quem comprou nos dois meses
clientes_fieis = clientes_janeiro & clientes_fevereiro
print("Clientes que compraram nos dois meses:", clientes_fieis)

# União: todos os clientes distintos dos dois meses juntos
todos_os_clientes = clientes_janeiro | clientes_fevereiro
print("Todos os clientes (sem repetição):", todos_os_clientes)

# Diferença: quem comprou em janeiro mas não voltou em fevereiro
clientes_perdidos = clientes_janeiro - clientes_fevereiro
print("Clientes que sumiram em fevereiro:", clientes_perdidos)

# Adicionando um item a um set (não gera erro mesmo se já existir)
clientes_janeiro.add("Ana")  # já existe, não faz diferença
clientes_janeiro.add("Elias")  # novo cliente
print(clientes_janeiro)
```

## Erros comuns de quem está começando

- Tentar acessar um set por índice (`produtos_unicos[0]`), o que gera erro — sets não têm ordem garantida, então não existe "primeiro item" de forma confiável.
- Esquecer que transformar uma lista em set perde a ordem original e qualquer repetição intencional. Se a ordem ou a contagem de repetições importa para a análise, set não é a estrutura certa.
- Confundir set vazio: `{}` cria um dicionário vazio, não um set vazio. Para criar um set vazio, é preciso usar `set()`.

## Exercício prático

A Loja da Ana registrou os produtos vendidos ao longo da semana:

```python
produtos_vendidos = ["Caneta Azul", "Caderno", "Caneta Azul", "Borracha", "Caderno", "Mochila", "Caneta Azul"]
```

1. Use `set()` para descobrir quantos produtos diferentes foram vendidos na semana.
2. Mostre a lista de produtos únicos.
3. Verifique se `"Lápis"` foi vendido nessa semana, usando `in`.

**Desafio bônus (opcional):** a loja também tem uma lista de produtos em promoção: `{"Caderno", "Mochila", "Lápis"}`. Descubra quais produtos vendidos na semana também estavam em promoção, usando interseção (`&`).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
produtos_vendidos = ["Caneta Azul", "Caderno", "Caneta Azul", "Borracha", "Caderno", "Mochila", "Caneta Azul"]

# Removendo duplicatas
produtos_unicos = set(produtos_vendidos)
print("Quantidade de produtos diferentes:", len(produtos_unicos))
print("Produtos únicos:", produtos_unicos)

# Verificando se "Lápis" foi vendido
print("Vendemos Lápis?", "Lápis" in produtos_unicos)

# Desafio bônus
produtos_em_promocao = {"Caderno", "Mochila", "Lápis"}
produtos_vendidos_em_promocao = produtos_unicos & produtos_em_promocao
print("Produtos vendidos que estavam em promoção:", produtos_vendidos_em_promocao)
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar o que é um set e para que serve com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Sei usar interseção (`&`), união (`|`) e diferença (`-`) entre sets
