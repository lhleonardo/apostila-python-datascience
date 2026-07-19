# Distribuições e histogramas

> Módulo 6 — Estatística e EDA · Tópico 3 de 8

## O que é e por que importa

**Distribuição** é como os valores de uma coluna se espalham: quais faixas
de valor são mais comuns, quais são raras, se os dados são simétricos ou
"puxados" para um lado. Média, mediana e desvio padrão (Tópicos 1 e 2)
resumem a distribuição em números; um **histograma** mostra ela visualmente,
agrupando os valores em faixas (chamadas de *bins*) e contando quantos caem
em cada uma.

Este módulo usa gráficos de forma simples, via `.plot()` do próprio Pandas
(que por baixo usa Matplotlib) — o Módulo 7 (Visualização) aprofunda a
construção de gráficos com mais controle e qualidade visual. Aqui o
objetivo é usar o histograma como **ferramenta de investigação**, não como
gráfico final para apresentar.

## Como funciona (com exemplo comentado)

```python
import pandas as pd

precos = pd.Series([10, 12, 11, 13, 45, 12, 11, 10, 14, 13, 12, 46, 11, 12, 13])

# .plot(kind="hist") -- gera um histograma rapidamente, ótimo para exploração
# (requer matplotlib instalado: pip install matplotlib)
precos.plot(kind="hist", bins=8, title="Distribuição de preços")
# em um notebook Jupyter, o gráfico aparece direto; em um script .py,
# use plt.show() do matplotlib.pyplot para abrir a janela do gráfico

# Sem depender de gráfico, dá pra "aproximar" um histograma com pd.cut,
# que divide os valores em faixas (bins) e conta quantos caem em cada uma
faixas = pd.cut(precos, bins=5)
print(faixas.value_counts().sort_index())
# (9.964, 17.2]    12
# (17.2, 24.4]      0
# (24.4, 31.6]      0
# (31.6, 38.8]      0
# (38.8, 46.0]      3
# -- confirma visualmente (em texto) que a maioria dos valores está entre 10-17,
#    com um grupo separado bem mais alto (perto de 45)

# Formas comuns de distribuição, e o que dizem sobre os dados:
# - Simétrica (parecida com um sino): média e mediana próximas
# - Assimétrica à direita (cauda longa de valores altos): média > mediana
#   (comum em preços, salários, tempos de espera)
# - Assimétrica à esquerda (cauda longa de valores baixos): média < mediana
# - Bimodal (dois "picos"): sugere que os dados vêm de dois grupos misturados
#   (ex: preços de produtos populares E de produtos de luxo juntos na mesma coluna)

print(precos.mean(), precos.median())
# média puxada para cima pela cauda de valores altos (45, 46) -> assimetria à direita

# .skew() -- mede numericamente a assimetria (skewness)
print(precos.skew())
# positivo -> assimetria à direita (cauda para valores altos)
# negativo -> assimetria à esquerda
# perto de 0 -> distribuição aproximadamente simétrica

# Detectando possível bimodalidade com value_counts de faixas (bins)
vendas_por_horario = pd.Series([9, 9, 10, 12, 12, 13, 18, 19, 19, 20, 12, 13])
faixas_horario = pd.cut(vendas_por_horario, bins=4)
print(faixas_horario.value_counts().sort_index())
# se os valores se concentrarem em dois grupos separados (não um centro só),
# é um indício de bimodalidade -- vale investigar se há dois "tipos" de
# situação misturados na mesma coluna (ex: horário de almoço x horário de jantar)
```

## Erros comuns de quem está começando

- Escolher um número de `bins` (faixas) arbitrário sem testar variações —
  poucos bins escondem detalhes da distribuição; bins demais criam ruído
  visual que parece padrão sem ser. Vale testar 2-3 valores diferentes de
  `bins` antes de tirar conclusões.
- Olhar só a média e ignorar a forma da distribuição — como visto no
  exemplo, uma cauda de valores altos distorce a média sem necessariamente
  "quebrar" nada; entender a forma da distribuição evita interpretar mal
  esse tipo de padrão.
- Confundir distribuição bimodal com outliers — os dois são fenômenos
  diferentes: outliers são poucos pontos isolados fora do padrão; uma
  distribuição bimodal tem **dois grupos inteiros** de dados concentrados em
  faixas diferentes, cada um com vários pontos.

## Exercício prático

```python
tempos_de_espera = pd.Series([2, 3, 3, 4, 2, 3, 5, 4, 3, 25, 2, 3, 4, 3, 28])
```

(tempos de espera em minutos de atendimentos, com dois atendimentos que
demoraram muito mais que o normal)

1. Calcule média, mediana e `.skew()` dessa série.
2. Use `pd.cut` com 5 faixas e `.value_counts()` para ver como os valores se
   distribuem.
3. Com base nos resultados, escreva (em um comentário) se a distribuição
   parece simétrica, assimétrica à direita, ou à esquerda.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

tempos_de_espera = pd.Series([2, 3, 3, 4, 2, 3, 5, 4, 3, 25, 2, 3, 4, 3, 28])

print(tempos_de_espera.mean())    # bem puxada para cima
print(tempos_de_espera.median())  # bem mais baixa, perto de 3
print(tempos_de_espera.skew())    # positivo -- assimetria à direita

faixas = pd.cut(tempos_de_espera, bins=5)
print(faixas.value_counts().sort_index())
# a maioria concentrada nas faixas baixas, com pouquíssimos valores nas faixas
# mais altas -- distribuição assimétrica à direita (cauda longa de valores altos),
# consistente com o skew positivo
```

</details>

## Checklist antes de avançar

- [ ] Sei explicar o que é um histograma e o que ele revela sobre os dados
- [ ] Sei interpretar assimetria comparando média e mediana, e usando `.skew()`
- [ ] Sei diferenciar uma distribuição bimodal de outliers isolados
- [ ] Resolvi o exercício sem olhar a solução
