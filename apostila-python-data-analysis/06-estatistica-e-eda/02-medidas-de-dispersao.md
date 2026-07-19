# Medidas de dispersão

> Módulo 6 — Estatística e EDA · Tópico 2 de 8

## O que é e por que importa

Saber o "valor típico" (Tópico 1) não conta a história toda. Duas turmas
podem ter a mesma média de notas (7.0), mas uma com notas todas próximas de
7 (6.8, 7.0, 7.2) e outra com notas muito espalhadas (2.0, 7.0, 12.0 — bom,
notas não passam de 10, mas a ideia é essa). **Medidas de dispersão** dizem
o quanto os dados variam em torno do centro — sem elas, comparar dois
conjuntos de dados só pela média pode esconder diferenças importantes.

As principais são:

- **Amplitude (range)**: diferença entre o maior e o menor valor. Simples,
  mas muito sensível a um único outlier.
- **Variância**: média dos quadrados das diferenças entre cada valor e a
  média. Difícil de interpretar diretamente (está na unidade "ao quadrado").
- **Desvio padrão (standard deviation)**: raiz quadrada da variância —
  volta para a unidade original dos dados, por isso é mais usado na prática
  que a variância pura.
- **Amplitude interquartil (IQR)**: diferença entre o terceiro quartil (Q3)
  e o primeiro quartil (Q1) — já visto no Módulo 5, Tópico 6, para detectar
  outliers. Mede a dispersão só da "metade do meio" dos dados, ignorando os
  extremos.

## Como funciona (com exemplo comentado)

```python
import pandas as pd

turma_a = pd.Series([6.8, 7.0, 7.2, 6.9, 7.1])
turma_b = pd.Series([2.0, 5.0, 7.0, 9.0, 12.0])

print(turma_a.mean(), turma_b.mean())  # 7.0, 7.0 -- MESMA média!

# Amplitude -- diferença entre máximo e mínimo
amplitude_a = turma_a.max() - turma_a.min()
amplitude_b = turma_b.max() - turma_b.min()
print(amplitude_a, amplitude_b)  # 0.4, 10.0 -- turma B muito mais espalhada

# Variância
print(turma_a.var())  # bem pequena
print(turma_b.var())  # bem maior

# Desvio padrão -- raiz quadrada da variância, na mesma unidade dos dados originais
print(turma_a.std())  # ~0.16 -- notas bem próximas da média
print(turma_b.std())  # ~3.87 -- notas bem espalhadas em torno da média

# Coeficiente de variação -- desvio padrão relativo à média, útil para
# comparar dispersão de colunas com escalas diferentes (ex: preço vs quantidade)
cv_a = turma_a.std() / turma_a.mean()
cv_b = turma_b.std() / turma_b.mean()
print(cv_a, cv_b)  # quanto maior, mais disperso em relação ao próprio tamanho

# Quartis e IQR (revisão do Módulo 5, Tópico 6)
q1 = turma_b.quantile(0.25)
q3 = turma_b.quantile(0.75)
iqr = q3 - q1
print(f"Q1={q1}, Q3={q3}, IQR={iqr}")

# .describe() já traz quartis e desvio padrão juntos
print(turma_b.describe())
# count     5.000000
# mean      7.000000
# std       3.872983
# min       2.000000
# 25%       5.000000
# 50%       7.000000
# 75%       9.000000
# max      12.000000

# Aplicando a colunas de um DataFrame -- útil para comparar dispersão entre grupos
df = pd.DataFrame({
    "loja": ["A", "A", "A", "B", "B", "B"],
    "venda_diaria": [1000, 1050, 980, 500, 1500, 800],
})
resumo = df.groupby("loja")["venda_diaria"].agg(["mean", "std"])
print(resumo)
# mesmo com médias parecidas, a loja B pode ter desvio padrão bem maior --
# suas vendas são mais imprevisíveis dia a dia
```

## Erros comuns de quem está começando

- Comparar apenas as médias de dois grupos e concluir que são "iguais" sem
  olhar a dispersão — como no exemplo das turmas A e B, médias iguais podem
  esconder distribuições completamente diferentes.
- Usar amplitude (`max - min`) como medida principal de dispersão em dados
  com outliers — como ela só olha os dois valores extremos, um único ponto
  fora do padrão distorce a métrica inteira; desvio padrão ou IQR costumam
  ser mais robustos.
- Confundir variância com desvio padrão ao interpretar um resultado — a
  variância está numa unidade "ao quadrado" (ex: reais², anos²), o que não
  tem interpretação prática direta; o desvio padrão (raiz da variância)
  volta para a unidade original e é o que normalmente se usa para comunicar
  dispersão.

## Exercício prático

```python
vendedor_x = pd.Series([500, 520, 480, 510, 490])
vendedor_y = pd.Series([200, 800, 300, 700, 500])
```

1. Calcule a média de vendas de cada vendedor e compare.
2. Calcule o desvio padrão de cada um e compare.
3. Com base nos dois resultados, escreva (em um comentário) qual vendedor
   tem performance mais **consistente** (não necessariamente quem vende
   mais em média).
4. Calcule o IQR de cada vendedor.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

vendedor_x = pd.Series([500, 520, 480, 510, 490])
vendedor_y = pd.Series([200, 800, 300, 700, 500])

print(vendedor_x.mean(), vendedor_y.mean())  # 500.0, 500.0 -- mesma média!

print(vendedor_x.std())  # ~15.8 -- bem consistente
print(vendedor_y.std())  # ~250.9 -- muito mais variável
# vendedor X é mais consistente: mesma média, mas desvio padrão muito menor

iqr_x = vendedor_x.quantile(0.75) - vendedor_x.quantile(0.25)
iqr_y = vendedor_y.quantile(0.75) - vendedor_y.quantile(0.25)
print(iqr_x, iqr_y)
```

</details>

## Checklist antes de avançar

- [ ] Sei calcular amplitude, variância, desvio padrão e IQR com Pandas
- [ ] Entendo por que desvio padrão é preferido à variância para comunicar resultados
- [ ] Sei que duas séries com médias iguais podem ter dispersões muito diferentes
- [ ] Resolvi o exercício sem olhar a solução
