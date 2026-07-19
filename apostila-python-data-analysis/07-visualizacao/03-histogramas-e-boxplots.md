# Histogramas e boxplots

> Módulo 7 — Visualização · Tópico 3 de 7

## O que é e por que importa

No Módulo 6 (Tópico 3) você já usou `pd.cut` para "aproximar" um histograma
em texto, e mencionou que gráficos de verdade viriam neste módulo. Agora é
hora de desenhá-los de fato, junto com o **boxplot** — outro gráfico central
para entender a distribuição de uma variável numérica, especialmente útil
para comparar a dispersão entre grupos e identificar outliers visualmente
(retomando o Módulo 5, Tópico 6).

- **Histograma**: mostra a forma da distribuição — onde os valores se
  concentram, se há assimetria, se existem múltiplos "picos".
- **Boxplot** (ou "diagrama de caixa"): resume a distribuição usando os
  quartis (Q1, mediana, Q3) e destaca outliers como pontos fora dos
  "bigodes" — é uma forma compacta de comparar várias distribuições lado a
  lado.

## Como funciona (com exemplo comentado)

```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# HISTOGRAMA
np.random.seed(0)
precos = np.concatenate([np.random.normal(30, 5, 200), np.random.normal(80, 10, 30)])

fig, ax = plt.subplots()
ax.hist(precos, bins=20, color="steelblue", edgecolor="white")
ax.set_title("Distribuição de preços")
ax.set_xlabel("Preço (R$)")
ax.set_ylabel("Frequência")
plt.show()

# testar mais de um número de bins ajuda a não tirar conclusões precipitadas
# (revisão do Módulo 6, Tópico 3, sobre a escolha de bins)
fig, eixos = plt.subplots(1, 3, figsize=(12, 4))
for ax, bins in zip(eixos, [5, 20, 50]):
    ax.hist(precos, bins=bins, color="steelblue", edgecolor="white")
    ax.set_title(f"bins={bins}")
plt.tight_layout()
plt.show()

# BOXPLOT com Matplotlib puro
fig, ax = plt.subplots()
ax.boxplot(precos, vert=True)
ax.set_title("Boxplot de preços")
ax.set_ylabel("Preço (R$)")
plt.show()
# a "caixa" vai de Q1 a Q3 (Módulo 5/6); a linha no meio é a mediana; os
# "bigodes" se estendem até 1.5x o IQR (mesma regra do Módulo 5, Tópico 6);
# pontos além disso são desenhados individualmente como possíveis outliers

# Boxplot comparando grupos -- muito mais informativo que um só
df = pd.DataFrame({
    "loja": ["A"] * 100 + ["B"] * 100,
    "venda_diaria": np.concatenate([
        np.random.normal(1000, 100, 100),
        np.random.normal(1000, 300, 100),  # mesma média, muito mais variação
    ]),
})

fig, ax = plt.subplots()
df.boxplot(column="venda_diaria", by="loja", ax=ax)
# boxplot direto do Pandas, agrupando por uma coluna categórica
ax.set_title("Vendas diárias por loja")
ax.set_ylabel("Venda diária (R$)")
plt.suptitle("")  # remove o título automático duplicado que o Pandas adiciona
plt.show()
# mesmo com médias parecidas, a caixa da loja B é bem mais "alta" (mais dispersão)
# -- o mesmo insight do Módulo 6, Tópico 2, agora visível de relance

# Histograma direto do Pandas (revisão do Módulo 6)
pd.Series(precos).plot(kind="hist", bins=20, title="Preços (via Pandas)")
plt.show()
```

## Erros comuns de quem está começando

- Usar poucos `bins` num histograma e concluir que a distribuição é
  simétrica, quando mais faixas revelariam uma cauda ou um segundo pico —
  vale sempre testar mais de uma quantidade de bins antes de decidir sobre a
  forma da distribuição.
- Interpretar todo ponto fora dos "bigodes" de um boxplot como erro de dado
  — como visto no Módulo 5 (Tópico 6), nem todo outlier é um erro; o boxplot
  só sinaliza que o valor é estatisticamente incomum, a decisão sobre o que
  fazer com ele exige contexto.
- Comparar boxplots de grupos com tamanhos de amostra muito diferentes sem
  mencionar isso — um grupo com poucos pontos pode ter uma caixa
  "enganosamente" pequena ou grande só por ter menos dados.

## Exercício prático

```python
import numpy as np
np.random.seed(1)
tempo_atendimento_a = np.random.normal(5, 1, 150)   # minutos, atendente A
tempo_atendimento_b = np.random.normal(5, 3, 150)   # mesma média, mais variação
```

1. Crie um histograma de `tempo_atendimento_a` com 15 bins.
2. Crie um boxplot comparando `tempo_atendimento_a` e `tempo_atendimento_b`
   lado a lado (dica: `ax.boxplot([tempo_atendimento_a, tempo_atendimento_b],
   labels=["Atendente A", "Atendente B"])`).
3. Com base no boxplot, escreva (em um comentário) qual atendente tem tempo
   de atendimento mais previsível.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(1)
tempo_atendimento_a = np.random.normal(5, 1, 150)
tempo_atendimento_b = np.random.normal(5, 3, 150)

fig, ax = plt.subplots()
ax.hist(tempo_atendimento_a, bins=15, color="steelblue", edgecolor="white")
ax.set_title("Tempo de atendimento -- Atendente A")
plt.show()

fig, ax = plt.subplots()
ax.boxplot([tempo_atendimento_a, tempo_atendimento_b], labels=["Atendente A", "Atendente B"])
ax.set_title("Comparação de tempo de atendimento")
ax.set_ylabel("Minutos")
plt.show()

# a caixa do Atendente A é visivelmente mais compacta (menor dispersão),
# indicando tempo de atendimento mais previsível/consistente, mesmo com
# média parecida à do Atendente B
```

</details>

## Checklist antes de avançar

- [ ] Sei criar um histograma e testar diferentes valores de `bins`
- [ ] Sei ler um boxplot (Q1, mediana, Q3, bigodes, outliers)
- [ ] Sei comparar distribuições de grupos diferentes com boxplot
- [ ] Resolvi o exercício sem olhar a solução
