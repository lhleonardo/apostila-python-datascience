# Outliers: detecção e tratamento

> Módulo 5 — Limpeza de Dados · Tópico 6 de 7

## O que é e por que importa

Outlier é um valor muito diferente do padrão dos demais — um funcionário com
salário de R$ 500.000 numa base onde a maioria ganha entre R$ 3.000 e
R$ 8.000, ou uma venda de R$ -50 (impossível) por erro de digitação. Alguns
outliers são erros de dados (e devem ser corrigidos ou removidos); outros são
eventos reais e importantes (e devem ser mantidos, só tratados com cuidado
nas análises). A parte difícil não é detectar valores extremos — é decidir
o que fazer com cada um.

Este módulo (05) foca na detecção mecânica; o Módulo 6 (Estatística e EDA)
aprofunda a interpretação estatística por trás disso.

## Como funciona (com exemplo comentado)

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "funcionario": ["A", "B", "C", "D", "E", "F", "G"],
    "salario": [3200, 3500, 4100, 3800, 3900, 4200, 50000],  # o último é bem fora do padrão
})

# Método 1: olhar estatísticas descritivas primeiro (Módulo 4, Tópico 3)
print(df["salario"].describe())
# a média fica bem puxada para cima pelo outlier; a mediana (50%) é mais "honesta"
# sobre o valor típico

# Método 2: IQR (Interquartile Range / Amplitude Interquartil) -- técnica clássica
q1 = df["salario"].quantile(0.25)
q3 = df["salario"].quantile(0.75)
iqr = q3 - q1

limite_inferior = q1 - 1.5 * iqr
limite_superior = q3 + 1.5 * iqr
print(f"Limites: {limite_inferior} a {limite_superior}")

outliers = df[(df["salario"] < limite_inferior) | (df["salario"] > limite_superior)]
print(outliers)  # funcionário G aparece como outlier

# Método 3: z-score -- quantos desvios padrão o valor está distante da média
# valores com |z-score| > 3 costumam ser considerados outliers
media = df["salario"].mean()
desvio_padrao = df["salario"].std()
df["z_score"] = (df["salario"] - media) / desvio_padrao
print(df[["funcionario", "salario", "z_score"]])

outliers_zscore = df[df["z_score"].abs() > 2]
print(outliers_zscore)

# Depois de identificar, as estratégias de tratamento são parecidas com as
# de valores ausentes (Tópico 1):

# Estratégia A: remover a linha (quando é claramente um erro de dados)
df_sem_outlier = df[(df["salario"] >= limite_inferior) & (df["salario"] <= limite_superior)]

# Estratégia B: "capping" (também chamado de winsorização) -- substitui o
# valor extremo pelo limite mais próximo, em vez de descartar a linha inteira
df["salario_com_cap"] = df["salario"].clip(lower=limite_inferior, upper=limite_superior)
print(df[["funcionario", "salario", "salario_com_cap"]])

# Estratégia C: manter o valor, mas usar estatísticas robustas a outliers
# na análise (mediana em vez de média, por exemplo) -- não altera o dado,
# só a forma de resumi-lo
print("Média:", df["salario"].mean())     # puxada pelo outlier
print("Mediana:", df["salario"].median())  # não afetada da mesma forma
```

## Erros comuns de quem está começando

- Remover todo outlier automaticamente sem investigar se é um erro de dados
  ou um evento real legítimo (uma venda excepcionalmente alta pode ser
  informação valiosa, não ruído) — a decisão deveria vir depois de olhar o
  contexto, não antes.
- Usar a **média** para resumir uma coluna que tem outliers, sem considerar
  a **mediana** como alternativa mais representativa do valor "típico" —
  isso volta com mais profundidade no Módulo 6.
- Aplicar o método IQR ou z-score cegamente em qualquer coluna, mesmo
  quando ela naturalmente tem distribuição bem espalhada (por exemplo, uma
  coluna de faturamento de empresas de tamanhos muito diferentes) — os
  "outliers" detectados nesse caso podem ser normais para o domínio, não
  erros.

## Exercício prático

```python
df = pd.DataFrame({
    "produto": ["A", "B", "C", "D", "E", "F"],
    "preco": [25.0, 30.0, 28.0, 32.0, 27.0, 999.0],  # o último parece erro de digitação
})
```

1. Calcule Q1, Q3 e o IQR da coluna `preco`.
2. Calcule os limites inferior e superior (regra 1.5×IQR) e identifique quais
   linhas são outliers.
3. Crie uma coluna `preco_com_cap` usando `.clip()` para limitar os valores
   extremos aos limites calculados.
4. Compare a média e a mediana de `preco` antes do tratamento, e comente
   (em um comentário no código) qual delas parece mais representativa do
   preço "típico" dos produtos.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

df = pd.DataFrame({
    "produto": ["A", "B", "C", "D", "E", "F"],
    "preco": [25.0, 30.0, 28.0, 32.0, 27.0, 999.0],
})

q1 = df["preco"].quantile(0.25)
q3 = df["preco"].quantile(0.75)
iqr = q3 - q1
print(f"Q1={q1}, Q3={q3}, IQR={iqr}")

limite_inferior = q1 - 1.5 * iqr
limite_superior = q3 + 1.5 * iqr
outliers = df[(df["preco"] < limite_inferior) | (df["preco"] > limite_superior)]
print(outliers)  # produto F

df["preco_com_cap"] = df["preco"].clip(lower=limite_inferior, upper=limite_superior)
print(df)

print("Média:", df["preco"].mean())      # puxada para cima pelo outlier
print("Mediana:", df["preco"].median())  # mais próxima do preço típico (~27-28)
# a mediana representa melhor o "preço típico" aqui, já que a média foi
# distorcida por um único valor muito fora do padrão
```

</details>

## Checklist antes de avançar

- [ ] Sei calcular limites de outlier com a regra IQR (1.5×IQR)
- [ ] Sei calcular z-score e usá-lo como critério alternativo de detecção
- [ ] Sei escolher entre remover, limitar (clip) ou manter um outlier, com justificativa
- [ ] Resolvi o exercício sem olhar a solução
