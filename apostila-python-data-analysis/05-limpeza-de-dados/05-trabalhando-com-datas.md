# Trabalhando com datas

> Módulo 5 — Limpeza de Dados · Tópico 5 de 7

## O que é e por que importa

Datas são um dos tipos de dado mais problemáticos em limpeza: vêm em
formatos diferentes (`"10/01/2024"`, `"2024-01-10"`, `"10 jan 2024"`),
frequentemente como texto em vez de um tipo de data de verdade, e análises
de negócio comuns ("vendas por mês", "quantos dias desde a última compra")
exigem que o Pandas reconheça a coluna como data para funcionar. O tipo
correto para isso é o `datetime64`, e o Pandas converte para ele com
`pd.to_datetime()`.

## Como funciona (com exemplo comentado)

```python
import pandas as pd

df = pd.DataFrame({
    "pedido_id": [1, 2, 3, 4],
    "data_texto": ["10/01/2024", "15/01/2024", "02/02/2024", "28/02/2024"],
    "valor": [150.0, 89.9, 45.0, 200.0],
})
print(df.dtypes)  # data_texto é "object" (texto), não data

# pd.to_datetime -- converte texto para datetime
# format especifica o padrão esperado -- sem isso, o Pandas tenta adivinhar,
# o que pode confundir dia e mês (10/01 pode virar 10 de janeiro OU 1 de outubro
# dependendo de qual convenção o Pandas assumir)
df["data"] = pd.to_datetime(df["data_texto"], format="%d/%m/%Y")
print(df["data"])
print(df["data"].dtype)  # datetime64[ns]

# Códigos de formato mais comuns: %d dia, %m mês, %Y ano com 4 dígitos,
# %y ano com 2 dígitos, %H:%M:%S horário

# Uma vez convertida, a coluna ganha o acessor .dt, com componentes da data
df["ano"] = df["data"].dt.year
df["mes"] = df["data"].dt.month
df["dia"] = df["data"].dt.day
df["dia_da_semana"] = df["data"].dt.day_name()  # nome do dia (em inglês por padrão)
print(df[["data", "ano", "mes", "dia", "dia_da_semana"]])

# Comparações e filtros com datas -- funcionam como comparações numéricas normais
inicio_fevereiro = pd.Timestamp("2024-02-01")
vendas_fevereiro = df[df["data"] >= inicio_fevereiro]
print(vendas_fevereiro)

# Diferença entre datas -- retorna um Timedelta
hoje = pd.Timestamp("2024-03-01")
df["dias_desde_pedido"] = (hoje - df["data"]).dt.days
print(df[["data", "dias_desde_pedido"]])

# Agrupando por mês -- combina com groupby (Módulo 4, Tópico 8)
df["ano_mes"] = df["data"].dt.to_period("M")  # "2024-01", "2024-02", ...
vendas_por_mes = df.groupby("ano_mes")["valor"].sum()
print(vendas_por_mes)

# errors="coerce" -- igual visto em pd.to_numeric (Tópico 3): datas inválidas viram NaT
# (Not a Time, o equivalente a NaN para datas) em vez de quebrar a conversão inteira
datas_com_erro = pd.Series(["10/01/2024", "data invalida", "15/02/2024"])
convertido = pd.to_datetime(datas_com_erro, format="%d/%m/%Y", errors="coerce")
print(convertido)
# 0   2024-01-10
# 1          NaT
# 2   2024-02-15
```

## Erros comuns de quem está começando

- Não especificar `format` ao converter datas ambíguas (como `10/01/2024`,
  que pode ser 10 de janeiro ou 1 de outubro dependendo da convenção) e
  deixar o Pandas adivinhar errado silenciosamente — sempre que souber o
  formato de origem, é mais seguro informá-lo explicitamente.
- Comparar uma coluna de data (já convertida) com uma **string** de data
  (`df["data"] >= "2024-02-01"`) — isso até funciona na maioria dos casos
  (o Pandas converte a string automaticamente), mas é menos explícito e
  mais propenso a erro do que comparar com um `pd.Timestamp(...)` de
  verdade.
- Esquecer de checar `NaT` depois de uma conversão com `errors="coerce"` —
  assim como `NaN` para números, `NaT` precisa ser tratado (Tópico 1) antes
  de seguir com cálculos de datas.

## Exercício prático

```python
df = pd.DataFrame({
    "cliente": ["Marcos", "Julia", "Pedro", "Ana"],
    "data_cadastro": ["05/03/2023", "12/07/2023", "20/11/2023", "01/01/2024"],
})
```

1. Converta `data_cadastro` para `datetime`, especificando o `format`
   correto (`"%d/%m/%Y"`).
2. Crie uma coluna `ano_cadastro` com o ano de cada data.
3. Calcule há quantos dias cada cliente está cadastrado, considerando "hoje"
   como `pd.Timestamp("2024-06-01")`.
4. Filtre os clientes cadastrados a partir de julho de 2023 (inclusive).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

df = pd.DataFrame({
    "cliente": ["Marcos", "Julia", "Pedro", "Ana"],
    "data_cadastro": ["05/03/2023", "12/07/2023", "20/11/2023", "01/01/2024"],
})

df["data_cadastro"] = pd.to_datetime(df["data_cadastro"], format="%d/%m/%Y")

df["ano_cadastro"] = df["data_cadastro"].dt.year

hoje = pd.Timestamp("2024-06-01")
df["dias_cadastrado"] = (hoje - df["data_cadastro"]).dt.days
print(df)

a_partir_de_julho = df[df["data_cadastro"] >= pd.Timestamp("2023-07-01")]
print(a_partir_de_julho)
```

</details>

## Checklist antes de avançar

- [ ] Sei converter texto para data com `pd.to_datetime()` especificando o `format`
- [ ] Sei extrair ano/mês/dia com o acessor `.dt`
- [ ] Sei filtrar e calcular diferenças entre datas
- [ ] Resolvi o exercício sem olhar a solução
