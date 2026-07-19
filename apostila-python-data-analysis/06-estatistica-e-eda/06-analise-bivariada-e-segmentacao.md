# Análise bivariada e segmentação

> Módulo 6 — Estatística e EDA · Tópico 6 de 8

## O que é e por que importa

Depois de entender cada coluna sozinha (Tópico 5), o próximo passo é
cruzá-las: "o gasto médio muda entre os planos Básico e Premium?", "clientes
de qual cidade têm mais atraso no pagamento?". Isso é análise **bivariada**
(duas variáveis) — e é aqui que `groupby` (Módulo 4, Tópico 8),
`pivot_table` (Módulo 4, Tópico 12) e correlação (Tópico 4 deste módulo) se
combinam para revelar padrões que uma coluna sozinha não mostra.

## Como funciona (com exemplo comentado)

```python
import pandas as pd

df = pd.DataFrame({
    "cliente": ["A", "B", "C", "D", "E", "F", "G", "H"],
    "plano": ["Basico", "Premium", "Basico", "Basico", "Premium", "Premium", "Basico", "Premium"],
    "cidade": ["SP", "SP", "RJ", "RJ", "SP", "RJ", "SP", "RJ"],
    "gasto_mensal": [50, 150, 45, 60, 200, 180, 55, 190],
    "meses_ativo": [12, 24, 6, 18, 30, 15, 9, 20],
})

# NUMÉRICA x CATEGÓRICA: comparar uma métrica entre grupos -- groupby + agg
resumo_por_plano = df.groupby("plano")["gasto_mensal"].agg(["mean", "median", "std", "count"])
print(resumo_por_plano)
#          mean  median        std  count
# plano
# Basico   52.5    52.5   6.454972      4
# Premium 180.0   185.0  20.816660      4
# -- Premium gasta bem mais em média, e tem mais variação entre clientes

# CATEGÓRICA x CATEGÓRICA: tabela de contingência com pd.crosstab
tabela_cruzada = pd.crosstab(df["plano"], df["cidade"])
print(tabela_cruzada)
# cidade   RJ  SP
# plano
# Basico    2   2
# Premium   2   2

# crosstab com porcentagens (normalize) -- mais fácil de comparar proporções
tabela_percentual = pd.crosstab(df["plano"], df["cidade"], normalize="index") * 100
print(tabela_percentual)
# dentro de cada plano, qual % está em cada cidade

# NUMÉRICA x NUMÉRICA: correlação (Tópico 4) e agrupamento por faixas
correlacao = df["meses_ativo"].corr(df["gasto_mensal"])
print(correlacao)  # clientes mais antigos gastam mais? checa aqui

# Segmentando uma variável numérica em faixas para cruzar como se fosse categórica
df["faixa_tempo"] = pd.cut(
    df["meses_ativo"],
    bins=[0, 10, 20, 31],
    labels=["novo (0-10m)", "intermediario (11-20m)", "antigo (21m+)"],
)
resumo_por_faixa = df.groupby("faixa_tempo", observed=True)["gasto_mensal"].mean()
print(resumo_por_faixa)

# pivot_table combina duas dimensões categóricas com uma métrica numérica
tabela_dinamica = df.pivot_table(
    index="plano", columns="cidade", values="gasto_mensal", aggfunc="mean"
)
print(tabela_dinamica)
```

O padrão geral da análise bivariada é sempre um destes três:

- **numérica x categórica** → `groupby` + agregação (comparar a métrica
  entre grupos)
- **categórica x categórica** → `pd.crosstab` (contar/cruzar combinações)
- **numérica x numérica** → `.corr()` (medir associação linear)

## Erros comuns de quem está começando

- Comparar médias entre grupos sem olhar também a dispersão (`std`) e o
  tamanho de cada grupo (`count`) — um grupo com poucas observações pode ter
  uma média enganosa, fácil de ser distorcida por um ou dois valores
  atípicos.
- Usar `pd.crosstab` com contagens absolutas quando os grupos têm tamanhos
  muito diferentes, dificultando a comparação — nesses casos,
  `normalize="index"` ou `normalize="columns"` deixa a comparação de
  proporções mais justa.
- Tentar cruzar uma variável numérica contínua diretamente com outra
  categórica através de `crosstab` (que espera categorias discretas) — o
  correto é primeiro discretizar a numérica com `pd.cut` (como no exemplo
  de `faixa_tempo`), ou usar `groupby` em vez de `crosstab`.

## Exercício prático

```python
df = pd.DataFrame({
    "funcionario": ["A", "B", "C", "D", "E", "F"],
    "departamento": ["Vendas", "TI", "Vendas", "TI", "Vendas", "TI"],
    "nivel": ["Junior", "Senior", "Pleno", "Junior", "Senior", "Pleno"],
    "salario": [3000, 8000, 5000, 3200, 9000, 5500],
})
```

1. Calcule média e desvio padrão de `salario` por `departamento`.
2. Crie uma tabela cruzada (`crosstab`) entre `departamento` e `nivel`.
3. Crie uma tabela dinâmica (`pivot_table`) com a média salarial por
   `departamento` e `nivel`.
4. Segmente `salario` em 3 faixas usando `pd.cut` e calcule a contagem de
   funcionários por faixa e departamento com `crosstab`.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

df = pd.DataFrame({
    "funcionario": ["A", "B", "C", "D", "E", "F"],
    "departamento": ["Vendas", "TI", "Vendas", "TI", "Vendas", "TI"],
    "nivel": ["Junior", "Senior", "Pleno", "Junior", "Senior", "Pleno"],
    "salario": [3000, 8000, 5000, 3200, 9000, 5500],
})

print(df.groupby("departamento")["salario"].agg(["mean", "std"]))

print(pd.crosstab(df["departamento"], df["nivel"]))

print(df.pivot_table(index="departamento", columns="nivel", values="salario", aggfunc="mean"))

df["faixa_salario"] = pd.cut(df["salario"], bins=3)
print(pd.crosstab(df["faixa_salario"], df["departamento"]))
```

</details>

## Checklist antes de avançar

- [ ] Sei escolher a técnica certa (groupby, crosstab ou corr) de acordo com os tipos das variáveis
- [ ] Sei usar `pd.crosstab` com `normalize` para comparar proporções
- [ ] Sei discretizar uma variável numérica com `pd.cut` para cruzá-la com outras
- [ ] Resolvi o exercício sem olhar a solução
