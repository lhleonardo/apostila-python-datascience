# Amostragem e introdução à inferência

> Módulo 6 — Estatística e EDA · Tópico 7 de 8

## O que é e por que importa

Até aqui, toda a estatística que você calculou foi **descritiva**: resume os
dados que você **tem**. Mas frequentemente os dados que você tem são só uma
**amostra** de um grupo maior (uma **população**) — uma pesquisa com 500
clientes representando milhões, um teste A/B com uma fração dos usuários de
um site. Estatística **inferencial** é o ramo que usa a amostra para tirar
conclusões sobre a população inteira, com um nível de confiança calculável.

Este tópico é só uma introdução conceitual — dá a base para você reconhecer
quando uma pergunta é de inferência (não só descrição) e entender a ideia de
intervalo de confiança. Testes de hipótese formais e inferência aprofundada
ficam fora do escopo desta apostila introdutória.

## Como funciona (com exemplo comentado)

```python
import pandas as pd
import numpy as np

# Simulando uma "população" inteira de 10.000 clientes (na prática você
# raramente tem a população inteira -- aqui é só para fins didáticos)
np.random.seed(42)
populacao = pd.Series(np.random.normal(loc=150, scale=40, size=10000))
# loc=150 é a média "real" da população, scale=40 é o desvio padrão "real"

print("Média real da população:", populacao.mean())  # próxima de 150

# Na prática, você não tem a população inteira -- só consegue uma AMOSTRA
amostra = populacao.sample(n=100, random_state=1)
print("Média da amostra:", amostra.mean())  # próxima de 150, mas não exatamente

# Quanto maior a amostra, mais a média da amostra tende a se aproximar da
# média real da população -- é a ideia central por trás de "quanto maior a
# amostra, mais confiável a estimativa"
for tamanho in [10, 50, 100, 1000]:
    amostra_teste = populacao.sample(n=tamanho, random_state=1)
    print(f"n={tamanho}: média da amostra = {amostra_teste.mean():.2f}")

# Erro padrão da média -- estima o quanto a média de UMA amostra tende a
# variar em torno da média real, dependendo do tamanho da amostra
erro_padrao = amostra.std() / np.sqrt(len(amostra))
print("Erro padrão:", erro_padrao)

# Intervalo de confiança de ~95% (aproximação simples, usando 1.96 desvios
# padrão -- regra prática para amostras razoavelmente grandes)
media_amostra = amostra.mean()
margem = 1.96 * erro_padrao
intervalo = (media_amostra - margem, media_amostra + margem)
print(f"Média estimada: {media_amostra:.2f}")
print(f"Intervalo de confiança de 95%: {intervalo[0]:.2f} a {intervalo[1]:.2f}")
# interpretação: "temos 95% de confiança de que a média REAL da população
# está entre esses dois valores" -- não é uma garantia absoluta, é uma
# estimativa com margem de erro conhecida

# Amostragem aleatória simples vs. amostragem estratificada
df = pd.DataFrame({
    "cliente": range(1, 11),
    "plano": ["Basico"] * 7 + ["Premium"] * 3,
    "gasto": [50, 55, 48, 60, 52, 58, 51, 200, 210, 195],
})

# amostra aleatória simples -- pode, por azar, pegar poucos ou nenhum Premium
amostra_simples = df.sample(n=4, random_state=1)
print(amostra_simples)

# amostragem estratificada -- garante representação proporcional de cada grupo
amostra_estratificada = df.groupby("plano", group_keys=False).apply(
    lambda grupo: grupo.sample(frac=0.4, random_state=1)
)
print(amostra_estratificada)
# mantém a PROPORÇÃO de Básico/Premium da população original na amostra
```

## Erros comuns de quem está começando

- Tratar qualquer conjunto de dados disponível como se fosse a população
  inteira, sem se perguntar se ele é representativo do grupo maior que
  realmente interessa (por exemplo, dados só de clientes que responderam
  uma pesquisa, ignorando os que não responderam).
- Tirar conclusões fortes de amostras muito pequenas, sem considerar que o
  erro padrão (e portanto a incerteza da estimativa) cresce bastante quando
  `n` é pequeno.
- Usar amostragem aleatória simples quando existem subgrupos importantes de
  tamanhos muito diferentes na população (como planos Básico e Premium com
  proporções bem desiguais) — isso pode gerar amostras que sub-representam
  ou super-representam um subgrupo por acaso; amostragem estratificada
  resolve esse problema.

## Exercício prático

```python
np.random.seed(7)
populacao_notas = pd.Series(np.random.normal(loc=7.0, scale=1.2, size=5000))
```

1. Calcule a média real dessa "população" de notas.
2. Retire uma amostra de 30 valores (`random_state=1`) e calcule sua média.
3. Calcule o erro padrão da amostra e o intervalo de confiança aproximado de
   95% (`1.96 * erro_padrao`).
4. Repita o processo com uma amostra de 300 valores e compare o tamanho do
   intervalo de confiança com o do item 3 — ele deveria ficar mais estreito
   (mais preciso) com a amostra maior.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd
import numpy as np

np.random.seed(7)
populacao_notas = pd.Series(np.random.normal(loc=7.0, scale=1.2, size=5000))

print("Média real:", populacao_notas.mean())

amostra_30 = populacao_notas.sample(n=30, random_state=1)
media_30 = amostra_30.mean()
erro_padrao_30 = amostra_30.std() / np.sqrt(30)
margem_30 = 1.96 * erro_padrao_30
print(f"n=30: média={media_30:.2f}, IC=({media_30-margem_30:.2f}, {media_30+margem_30:.2f})")

amostra_300 = populacao_notas.sample(n=300, random_state=1)
media_300 = amostra_300.mean()
erro_padrao_300 = amostra_300.std() / np.sqrt(300)
margem_300 = 1.96 * erro_padrao_300
print(f"n=300: média={media_300:.2f}, IC=({media_300-margem_300:.2f}, {media_300+margem_300:.2f})")

# o intervalo com n=300 é visivelmente mais estreito que com n=30 --
# amostras maiores dão estimativas mais precisas
```

</details>

## Checklist antes de avançar

- [ ] Sei explicar a diferença entre estatística descritiva e inferencial
- [ ] Sei calcular erro padrão e um intervalo de confiança aproximado
- [ ] Sei explicar por que amostras maiores dão estimativas mais precisas
- [ ] Sei quando amostragem estratificada é preferível à aleatória simples
- [ ] Resolvi o exercício sem olhar a solução
