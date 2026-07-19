# Scatter plots e relação entre variáveis

> Módulo 7 — Visualização · Tópico 4 de 7

## O que é e por que importa

No Módulo 6 (Tópico 4) você calculou correlação como um **número**. O
**scatter plot** (gráfico de dispersão) é a forma visual dessa mesma
pergunta: cada ponto representa uma linha do dataset, posicionado pelo valor
de duas variáveis numéricas (uma no eixo X, outra no eixo Y). É a melhor
ferramenta para checar visualmente se duas variáveis parecem relacionadas, e
principalmente para detectar relações **não-lineares** que o coeficiente de
correlação de Pearson pode não capturar bem (mencionado no Módulo 6, Tópico
4).

## Como funciona (com exemplo comentado)

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

np.random.seed(0)
horas_estudo = np.random.uniform(0, 10, 50)
nota = horas_estudo * 0.8 + np.random.normal(0, 1, 50)  # relação aproximadamente linear

# scatter plot básico
fig, ax = plt.subplots()
ax.scatter(horas_estudo, nota, alpha=0.7)
# alpha controla transparência -- útil quando há pontos sobrepostos
ax.set_title("Horas de estudo x Nota")
ax.set_xlabel("Horas de estudo")
ax.set_ylabel("Nota")
plt.show()

# Colorindo pontos por uma terceira variável categórica -- adiciona uma dimensão
df = pd.DataFrame({
    "horas_estudo": horas_estudo,
    "nota": nota,
    "turno": np.random.choice(["Manhã", "Noite"], size=50),
})

fig, ax = plt.subplots()
for turno, cor in [("Manhã", "steelblue"), ("Noite", "orange")]:
    subset = df[df["turno"] == turno]
    ax.scatter(subset["horas_estudo"], subset["nota"], label=turno, alpha=0.7, color=cor)
ax.set_title("Horas de estudo x Nota, por turno")
ax.legend()
plt.show()

# Tamanho do ponto representando uma quarta variável (bubble chart)
tamanho_turma = np.random.uniform(10, 100, 50)
fig, ax = plt.subplots()
ax.scatter(horas_estudo, nota, s=tamanho_turma, alpha=0.5, color="steelblue")
ax.set_title("Horas de estudo x Nota (tamanho = alunos na turma)")
plt.show()

# Adicionando uma linha de tendência simples (regressão linear com numpy)
coeficientes = np.polyfit(horas_estudo, nota, deg=1)  # deg=1 = linha reta
linha_tendencia = np.poly1d(coeficientes)

fig, ax = plt.subplots()
ax.scatter(horas_estudo, nota, alpha=0.6, color="steelblue")
x_ordenado = np.sort(horas_estudo)
ax.plot(x_ordenado, linha_tendencia(x_ordenado), color="red", linewidth=2, label="Tendência")
ax.legend()
ax.set_title("Horas de estudo x Nota, com linha de tendência")
plt.show()

# Relação não-linear -- correlação de Pearson pode enganar aqui
x_curva = np.linspace(-5, 5, 100)
y_curva = x_curva ** 2 + np.random.normal(0, 2, 100)  # relação em U, não-linear

fig, ax = plt.subplots()
ax.scatter(x_curva, y_curva, alpha=0.6, color="steelblue")
ax.set_title("Relação não-linear (correlação de Pearson pode ser perto de 0)")
plt.show()
print("Correlação (Pearson):", np.corrcoef(x_curva, y_curva)[0, 1])
# o número pode ficar perto de 0, mesmo havendo uma relação clara (em U) --
# reforça a importância de visualizar, não só calcular
```

## Erros comuns de quem está começando

- Calcular só a correlação numérica (Módulo 6) sem nunca visualizar os
  dados com scatter plot — relações não-lineares, agrupamentos ou outliers
  que distorcem o coeficiente ficam invisíveis olhando só para o número.
- Usar muitos pontos sobrepostos sem `alpha` (transparência), fazendo a
  região mais densa parecer uma "mancha" sólida sem noção de quantos pontos
  realmente existem ali.
- Adicionar uma linha de tendência linear (`np.polyfit` com `deg=1`) em
  dados que claramente têm uma relação não-linear (como o exemplo em U) —
  isso sugere visualmente uma relação que não existe da forma representada.

## Exercício prático

```python
import numpy as np
np.random.seed(3)
tamanho_casa = np.random.uniform(50, 300, 60)  # m²
preco_casa = tamanho_casa * 3000 + np.random.normal(0, 30000, 60)  # reais
regiao = np.random.choice(["Centro", "Periferia"], size=60)
```

1. Crie um scatter plot de `tamanho_casa` (X) por `preco_casa` (Y).
2. Colora os pontos por `regiao`, com legenda.
3. Adicione uma linha de tendência linear ao gráfico do item 1 (sem a
   separação por região).
4. Calcule a correlação entre `tamanho_casa` e `preco_casa` e confirme que
   ela é coerente com o padrão visual do gráfico.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

np.random.seed(3)
tamanho_casa = np.random.uniform(50, 300, 60)
preco_casa = tamanho_casa * 3000 + np.random.normal(0, 30000, 60)
regiao = np.random.choice(["Centro", "Periferia"], size=60)

fig, ax = plt.subplots()
ax.scatter(tamanho_casa, preco_casa, alpha=0.7, color="steelblue")
ax.set_title("Tamanho x Preço")
ax.set_xlabel("Tamanho (m²)")
ax.set_ylabel("Preço (R$)")
plt.show()

df = pd.DataFrame({"tamanho": tamanho_casa, "preco": preco_casa, "regiao": regiao})
fig, ax = plt.subplots()
for r, cor in [("Centro", "steelblue"), ("Periferia", "orange")]:
    subset = df[df["regiao"] == r]
    ax.scatter(subset["tamanho"], subset["preco"], label=r, alpha=0.7, color=cor)
ax.legend()
plt.show()

coeficientes = np.polyfit(tamanho_casa, preco_casa, deg=1)
linha_tendencia = np.poly1d(coeficientes)
x_ordenado = np.sort(tamanho_casa)

fig, ax = plt.subplots()
ax.scatter(tamanho_casa, preco_casa, alpha=0.6, color="steelblue")
ax.plot(x_ordenado, linha_tendencia(x_ordenado), color="red", linewidth=2)
plt.show()

print(np.corrcoef(tamanho_casa, preco_casa)[0, 1])  # forte positiva, coerente com o gráfico
```

</details>

## Checklist antes de avançar

- [ ] Sei criar um scatter plot e interpretar o padrão de pontos
- [ ] Sei colorir pontos por uma variável categórica adicional
- [ ] Sei adicionar uma linha de tendência linear
- [ ] Entendo por que relações não-lineares podem enganar a correlação de Pearson
- [ ] Resolvi o exercício sem olhar a solução
