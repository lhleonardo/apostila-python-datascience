# Gráficos de linha e barra

> Módulo 7 — Visualização · Tópico 2 de 7

## O que é e por que importa

Linha e barra são os dois gráficos mais usados em análise de dados de
negócio, e cada um tem um propósito claro:

- **Gráfico de linha**: mostra **evolução ao longo de uma sequência
  contínua** — quase sempre tempo (vendas por mês, usuários ativos por dia).
  A linha conecta pontos, sugerindo continuidade entre eles.
- **Gráfico de barra**: compara **valores entre categorias distintas** —
  faturamento por produto, número de clientes por cidade. Cada barra é
  independente das outras, sem sugerir uma sequência contínua.

Usar o gráfico errado para o tipo de dado (por exemplo, linha para comparar
categorias sem ordem natural) pode sugerir uma tendência que não existe.

## Como funciona (com exemplo comentado)

```python
import matplotlib.pyplot as plt
import pandas as pd

# GRÁFICO DE LINHA -- para série temporal / sequência contínua
meses = ["Jan", "Fev", "Mar", "Abr", "Mai", "Jun"]
faturamento = [12000, 13500, 11800, 15200, 16000, 17500]

fig, ax = plt.subplots()
ax.plot(meses, faturamento, marker="o")  # marker="o" destaca cada ponto com um círculo
ax.set_title("Faturamento mensal")
ax.set_xlabel("Mês")
ax.set_ylabel("Faturamento (R$)")
plt.show()

# múltiplas linhas na mesma figura -- útil para comparar séries
faturamento_2023 = [10000, 11000, 10500, 12000, 13000, 14000]
fig, ax = plt.subplots()
ax.plot(meses, faturamento, marker="o", label="2024")
ax.plot(meses, faturamento_2023, marker="s", label="2023")
ax.set_title("Faturamento mensal: 2023 vs 2024")
ax.legend()  # mostra a legenda com os "label" de cada linha
plt.show()

# GRÁFICO DE BARRA -- para comparar categorias
produtos = ["Caneta", "Caderno", "Mochila", "Estojo"]
vendas = [320, 150, 45, 90]

fig, ax = plt.subplots()
ax.bar(produtos, vendas, color="steelblue")
ax.set_title("Vendas por produto")
ax.set_xlabel("Produto")
ax.set_ylabel("Unidades vendidas")
plt.show()

# barra horizontal -- útil quando os nomes das categorias são longos
fig, ax = plt.subplots()
ax.barh(produtos, vendas, color="steelblue")
ax.set_title("Vendas por produto (horizontal)")
plt.show()

# ordenando as barras do maior para o menor -- quase sempre melhora a leitura
df = pd.DataFrame({"produto": produtos, "vendas": vendas}).sort_values("vendas", ascending=True)
fig, ax = plt.subplots()
ax.barh(df["produto"], df["vendas"], color="steelblue")
ax.set_title("Vendas por produto (ordenado)")
plt.show()

# Gerando um gráfico direto de um DataFrame com .plot() (visto de leve no Módulo 6)
# combina groupby (Módulo 4) + plot em uma linha só, muito comum no dia a dia
vendas_df = pd.DataFrame({
    "mes": meses,
    "faturamento": faturamento,
})
vendas_df.plot(x="mes", y="faturamento", kind="line", marker="o", title="Faturamento mensal")
plt.show()
```

## Erros comuns de quem está começando

- Usar gráfico de linha para comparar categorias sem ordem natural (como
  produtos, cidades) — a linha sugere uma progressão contínua entre os
  pontos que não existe nesse tipo de dado; o correto é barra.
- Não ordenar as barras quando a comparação entre categorias é o ponto
  principal do gráfico — barras em ordem alfabética ou "como vieram no
  dataset" dificultam identificar rapidamente o maior e o menor valor;
  ordenar (Módulo 4, Tópico 7) quase sempre melhora a leitura.
- Esquecer `ax.legend()` ao desenhar múltiplas linhas/barras com `label`
  definido — sem essa chamada, os rótulos passados em `label=...` não
  aparecem no gráfico, mesmo estando corretamente atribuídos.

## Exercício prático

```python
trimestres = ["T1", "T2", "T3", "T4"]
vendas_loja_a = [5000, 6200, 5800, 7100]
vendas_loja_b = [4800, 5100, 6000, 6500]

categorias_populares = ["Eletrônicos", "Roupas", "Casa", "Beleza"]
receita_categoria = [45000, 32000, 18000, 27000]
```

1. Crie um gráfico de linha comparando `vendas_loja_a` e `vendas_loja_b` ao
   longo dos trimestres, com legenda.
2. Crie um gráfico de barra vertical com a receita por categoria.
3. Ordene as categorias da maior para a menor receita e refaça o gráfico
   como barra horizontal.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import matplotlib.pyplot as plt
import pandas as pd

trimestres = ["T1", "T2", "T3", "T4"]
vendas_loja_a = [5000, 6200, 5800, 7100]
vendas_loja_b = [4800, 5100, 6000, 6500]

fig, ax = plt.subplots()
ax.plot(trimestres, vendas_loja_a, marker="o", label="Loja A")
ax.plot(trimestres, vendas_loja_b, marker="s", label="Loja B")
ax.set_title("Vendas por trimestre")
ax.legend()
plt.show()

categorias_populares = ["Eletrônicos", "Roupas", "Casa", "Beleza"]
receita_categoria = [45000, 32000, 18000, 27000]

fig, ax = plt.subplots()
ax.bar(categorias_populares, receita_categoria, color="steelblue")
ax.set_title("Receita por categoria")
plt.show()

df = pd.DataFrame({
    "categoria": categorias_populares,
    "receita": receita_categoria,
}).sort_values("receita")

fig, ax = plt.subplots()
ax.barh(df["categoria"], df["receita"], color="steelblue")
ax.set_title("Receita por categoria (ordenado)")
plt.show()
```

</details>

## Checklist antes de avançar

- [ ] Sei quando usar gráfico de linha e quando usar gráfico de barra
- [ ] Sei desenhar múltiplas linhas/barras na mesma figura, com legenda
- [ ] Sei ordenar as categorias de um gráfico de barra para facilitar a leitura
- [ ] Resolvi o exercício sem olhar a solução
