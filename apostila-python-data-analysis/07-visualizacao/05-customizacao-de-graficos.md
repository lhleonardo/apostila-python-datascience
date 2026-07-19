# Customização de gráficos

> Módulo 7 — Visualização · Tópico 5 de 7

## O que é e por que importa

Um gráfico tecnicamente correto ainda pode comunicar mal se estiver
confuso, com cores aleatórias, sem contexto ou difícil de ler. Este tópico
reúne os ajustes que separam um gráfico "de exploração rápida" (para você
mesmo entender os dados) de um gráfico "pronto para apresentar" (para
comunicar um achado a outra pessoa) — cores consistentes, anotações, grades
e tamanho adequado.

## Como funciona (com exemplo comentado)

```python
import matplotlib.pyplot as plt
import numpy as np

meses = ["Jan", "Fev", "Mar", "Abr", "Mai", "Jun"]
faturamento = [12000, 13500, 11800, 15200, 16000, 21000]

# Tamanho da figura -- figsize=(largura, altura) em polegadas
fig, ax = plt.subplots(figsize=(8, 5))
ax.plot(meses, faturamento, marker="o", color="#2b6cb0", linewidth=2)

# Título e rótulos com controle de tamanho de fonte
ax.set_title("Faturamento mensal — 2024", fontsize=14, fontweight="bold")
ax.set_xlabel("Mês", fontsize=11)
ax.set_ylabel("Faturamento (R$)", fontsize=11)

# Grade (grid) -- ajuda a ler valores aproximados sem poluir o gráfico
ax.grid(True, alpha=0.3)

# Anotando um ponto específico -- útil para destacar um evento ou marco
ax.annotate(
    "Recorde!",
    xy=(5, 21000),          # ponto que está sendo anotado
    xytext=(3.5, 19500),    # posição do texto
    arrowprops=dict(arrowstyle="->", color="gray"),
)

# Formatando o eixo Y para mostrar como moeda (sem depender de biblioteca extra)
ax.set_yticks([10000, 12500, 15000, 17500, 20000])
ax.set_yticklabels([f"R$ {v:,.0f}".replace(",", ".") for v in ax.get_yticks()])

plt.show()

# Paletas de cores consistentes para categorias -- evita cores aleatórias
# entre gráficos diferentes do mesmo relatório
categorias = ["Papelaria", "Eletrônicos", "Roupas", "Casa"]
valores = [12000, 25000, 18000, 9000]
cores = ["#2b6cb0", "#dd6b20", "#38a169", "#805ad5"]  # uma cor fixa por categoria

fig, ax = plt.subplots()
ax.bar(categorias, valores, color=cores)
ax.set_title("Faturamento por categoria")
plt.show()

# Removendo "bordas" desnecessárias (spines) -- comum em gráficos mais limpos
fig, ax = plt.subplots()
ax.plot(meses, faturamento, marker="o", color="#2b6cb0")
ax.spines["top"].set_visible(False)
ax.spines["right"].set_visible(False)
ax.set_title("Faturamento mensal (visual mais limpo)")
plt.show()

# Definindo um "estilo" global do Matplotlib -- muda a aparência de todos os
# gráficos seguintes de uma vez (fontes, cores de fundo, grade padrão, etc.)
plt.style.use("seaborn-v0_8-whitegrid")  # nome pode variar conforme a versão instalada
fig, ax = plt.subplots()
ax.plot(meses, faturamento, marker="o")
ax.set_title("Com estilo pré-definido")
plt.show()
plt.style.use("default")  # volta ao estilo padrão para os próximos gráficos
```

## Erros comuns de quem está começando

- Usar cores diferentes para a mesma categoria em gráficos diferentes do
  mesmo relatório — isso confunde quem está lendo, que naturalmente espera
  que uma cor "signifique" sempre a mesma coisa ao longo de uma apresentação.
- Exagerar em anotações, grades e cores a ponto do gráfico ficar poluído —
  cada elemento visual deveria ajudar a entender o dado, não competir por
  atenção; menos costuma ser mais em visualização de dados.
- Deixar o `figsize` padrão (pequeno) para gráficos com muitos rótulos ou
  categorias, gerando texto sobreposto e ilegível — ajustar `figsize` (e
  `plt.tight_layout()`) resolve a maior parte desses casos.

## Exercício prático

```python
produtos = ["Caneta", "Caderno", "Mochila", "Estojo", "Lapis"]
vendas = [320, 150, 45, 90, 280]
```

1. Crie um gráfico de barra com `figsize=(8, 5)`, título em negrito, e uma
   cor fixa diferente para cada barra (defina uma lista de 5 cores).
2. Adicione uma grade horizontal sutil (`alpha` baixo).
3. Anote com uma seta o produto de menor venda (`Mochila`), destacando que é
   o "menos vendido".
4. Remova as bordas superior e direita do gráfico.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import matplotlib.pyplot as plt

produtos = ["Caneta", "Caderno", "Mochila", "Estojo", "Lapis"]
vendas = [320, 150, 45, 90, 280]
cores = ["#2b6cb0", "#dd6b20", "#38a169", "#805ad5", "#d53f8c"]

fig, ax = plt.subplots(figsize=(8, 5))
ax.bar(produtos, vendas, color=cores)
ax.set_title("Vendas por produto", fontweight="bold")
ax.grid(True, axis="y", alpha=0.3)

ax.annotate(
    "Menos vendido",
    xy=(2, 45),
    xytext=(2.3, 150),
    arrowprops=dict(arrowstyle="->", color="gray"),
)

ax.spines["top"].set_visible(False)
ax.spines["right"].set_visible(False)

plt.show()
```

</details>

## Checklist antes de avançar

- [ ] Sei ajustar `figsize`, título, rótulos e cores de um gráfico
- [ ] Sei adicionar grades e anotações sem poluir o gráfico
- [ ] Sei manter cores consistentes para as mesmas categorias entre gráficos
- [ ] Resolvi o exercício sem olhar a solução
