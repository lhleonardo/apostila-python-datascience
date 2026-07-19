# Estruturando uma EDA completa

> Módulo 6 — Estatística e EDA · Tópico 8 de 8 (último do módulo)

## O que é e por que importa

Você já tem todas as ferramentas individuais (tendência central, dispersão,
distribuição, correlação, análise uni e bivariada, noção de amostragem).
Este último tópico junta tudo num **roteiro** que você pode aplicar a
qualquer dataset novo — a estrutura que analistas de dados seguem (com
variações) sempre que abrem um dataset pela primeira vez, antes de
visualizar (Módulo 7) ou modelar.

## Como funciona (com exemplo comentado)

```python
import pandas as pd
import numpy as np
from io import StringIO

csv_texto = """cliente,plano,cidade,idade,gasto_mensal,meses_ativo
1,Basico,SP,25,50,12
2,Premium,SP,34,150,24
3,Basico,RJ,41,45,6
4,Basico,RJ,29,60,18
5,Premium,SP,55,200,30
6,Premium,RJ,38,180,15
7,Basico,SP,45,55,9
8,Premium,RJ,31,190,20
"""
df = pd.read_csv(StringIO(csv_texto))

# ROTEIRO DE UMA EDA (assumindo que a limpeza do Módulo 5 já foi feita)

# 1. Visão geral do dataset
print(df.shape)
df.info()

# 2. Separar colunas numéricas e categóricas (Tópico 5)
numericas = df.select_dtypes(include="number").columns.tolist()
categoricas = df.select_dtypes(include="object").columns.tolist()
print("Numéricas:", numericas)
print("Categóricas:", categoricas)

# 3. Análise univariada de cada coluna numérica (Tópicos 1, 2, 3, 5)
for coluna in numericas:
    if coluna == "cliente":
        continue  # ID não é uma métrica de negócio, pular
    print(f"\n--- {coluna} ---")
    print(df[coluna].describe())
    print("Assimetria:", df[coluna].skew())

# 4. Análise univariada de cada coluna categórica (Tópico 5)
for coluna in categoricas:
    if coluna == "cliente":
        continue
    print(f"\n--- {coluna} ---")
    print(df[coluna].value_counts(normalize=True) * 100)

# 5. Matriz de correlação entre as numéricas (Tópico 4)
print(df[numericas].corr(numeric_only=True))

# 6. Cruzamentos relevantes para as perguntas de negócio (Tópico 6)
# pergunta: "clientes Premium gastam significativamente mais?"
print(df.groupby("plano")["gasto_mensal"].agg(["mean", "std", "count"]))

# pergunta: "há relação entre tempo de ativo e gasto mensal?"
print(df["meses_ativo"].corr(df["gasto_mensal"]))

# pergunta: "a distribuição de planos varia por cidade?"
print(pd.crosstab(df["cidade"], df["plano"], normalize="index") * 100)

# 7. Sintetizar achados em texto -- a EDA só é útil se comunicada.
# Um bom resumo de EDA responde:
# - Quantas linhas/colunas, e qual a qualidade geral dos dados?
# - Quais as principais métricas numéricas (tendência central e dispersão)?
# - Que padrões interessantes apareceram nos cruzamentos?
# - Que perguntas ficaram em aberto ou precisam de mais dados?

achados = """
Achados da EDA:
- Dataset com 8 clientes, sem valores ausentes.
- Clientes Premium gastam em média 180, contra 52.5 dos Básicos --
  diferença expressiva, mas amostra pequena para confirmar estatisticamente.
- Correlação entre meses_ativo e gasto_mensal: forte e positiva --
  clientes mais antigos tendem a gastar mais (ou vice-versa: quem gasta mais
  permanece mais tempo -- direção da causa não é possível afirmar só com isso).
- Distribuição de planos parece similar entre SP e RJ, sem padrão geográfico óbvio.
"""
print(achados)
```

## Erros comuns de quem está começando

- Rodar análises soltas, sem um roteiro, e esquecer de examinar alguma
  coluna importante — seguir uma sequência fixa (geral → univariada →
  bivariada → síntese) evita esse tipo de lacuna.
- Fazer toda a análise e não escrever uma síntese em texto — números e
  tabelas sozinhos raramente comunicam bem para quem vai usar a análise;
  o passo final de "traduzir em frases" é parte do trabalho, não um extra.
- Tirar conclusões fortes demais de amostras pequenas (como no exemplo, 8
  clientes) sem reconhecer a limitação — vale sempre mencionar o tamanho da
  amostra ao relatar um achado, especialmente quando ele é pequeno (conexão
  com o Tópico 7, sobre amostragem).

## Exercício prático

Usando o dataset abaixo, escreva o roteiro completo de EDA (visão geral,
univariada, bivariada, síntese em texto):

```python
df = pd.DataFrame({
    "produto": ["A", "B", "C", "D", "E", "F", "G", "H"],
    "categoria": ["Eletronico", "Roupa", "Eletronico", "Roupa", "Eletronico", "Casa", "Casa", "Roupa"],
    "preco": [899.0, 79.9, 1200.0, 129.9, 450.0, 199.9, 89.9, 59.9],
    "avaliacao": [4.5, 3.8, 4.7, 4.0, 4.2, 3.5, 4.1, 3.9],
    "vendas_mes": [50, 200, 20, 150, 80, 60, 100, 300],
})
```

1. Visão geral (`shape`, `info`).
2. Análise univariada de `preco`, `avaliacao` e `vendas_mes`.
3. Análise univariada de `categoria`.
4. Correlação entre `preco`, `avaliacao` e `vendas_mes` — o preço parece
   afetar as vendas?
5. Gasto/vendas médias por categoria (`groupby`).
6. Escreva 3-4 frases de síntese com os principais achados.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

df = pd.DataFrame({
    "produto": ["A", "B", "C", "D", "E", "F", "G", "H"],
    "categoria": ["Eletronico", "Roupa", "Eletronico", "Roupa", "Eletronico", "Casa", "Casa", "Roupa"],
    "preco": [899.0, 79.9, 1200.0, 129.9, 450.0, 199.9, 89.9, 59.9],
    "avaliacao": [4.5, 3.8, 4.7, 4.0, 4.2, 3.5, 4.1, 3.9],
    "vendas_mes": [50, 200, 20, 150, 80, 60, 100, 300],
})

print(df.shape)
df.info()

for coluna in ["preco", "avaliacao", "vendas_mes"]:
    print(f"\n--- {coluna} ---")
    print(df[coluna].describe())

print(df["categoria"].value_counts(normalize=True) * 100)

print(df[["preco", "avaliacao", "vendas_mes"]].corr())
# correlação entre preco e vendas_mes tende a ser fortemente negativa --
# produtos mais caros vendem menos unidades por mês

print(df.groupby("categoria")[["preco", "vendas_mes"]].mean())

achados = """
- Eletrônicos têm o maior preço médio e a menor quantidade vendida por mês,
  sugerindo elasticidade de preço: quanto mais caro, menos unidades vendidas.
- Roupas e itens de Casa, mais baratos, vendem em volume bem maior.
- A correlação entre preço e avaliação é fraca, sugerindo que preço alto
  não está necessariamente associado a produtos melhor avaliados.
"""
print(achados)
```

</details>

## Checklist antes de avançar

- [ ] Sei seguir um roteiro estruturado de EDA do início ao fim
- [ ] Sei sintetizar os achados numéricos em frases claras
- [ ] Reconheço as limitações de conclusões tiradas de amostras pequenas
- [ ] Resolvi o exercício sem olhar a solução

## Checklist do Módulo 6

Antes de seguir para o Módulo 7 (Visualização), confirme que você consegue,
sem consultar a apostila:

- [ ] Calcular e interpretar média, mediana e moda, sabendo quando cada uma é mais apropriada
- [ ] Calcular e interpretar variância, desvio padrão e IQR
- [ ] Reconhecer o formato de uma distribuição (simétrica, assimétrica, bimodal) a partir de estatísticas
- [ ] Calcular e interpretar correlação entre variáveis, sem confundir com causalidade
- [ ] Fazer análise univariada e bivariada de um dataset novo
- [ ] Explicar a diferença entre estatística descritiva e inferencial
- [ ] Estruturar e comunicar os achados de uma EDA completa

Pronto? Siga para o [Módulo 7 — Visualização](../07-visualizacao/00-indice.md).
