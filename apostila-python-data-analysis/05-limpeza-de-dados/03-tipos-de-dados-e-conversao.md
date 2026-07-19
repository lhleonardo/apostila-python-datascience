# Tipos de dados e conversão

> Módulo 5 — Limpeza de Dados · Tópico 3 de 7

## O que é e por que importa

Um problema muito comum em dados importados (de CSV, de planilhas, de
formulários) é o **tipo errado**: um preço lido como texto porque tinha um
"R$" na frente, uma data guardada como string, uma coluna numérica que virou
`object` porque um único valor estava escrito errado (como `"12O"` em vez de
`"120"`, com a letra O no lugar do número zero). Colunas com tipo errado
quebram cálculos, ordenações e comparações de forma silenciosa — o Pandas não
avisa, só produz resultado errado.

## Como funciona (com exemplo comentado)

```python
import pandas as pd

df = pd.DataFrame({
    "produto": ["Caneta", "Caderno", "Mochila", "Lapis"],
    "preco": ["R$ 2,50", "R$ 15,90", "R$ 89,90", "R$ 1,20"],  # texto, não número!
    "quantidade": ["3", "1", "2", "cinco"],  # texto, e um valor inválido
    "em_estoque": ["sim", "sim", "nao", "sim"],
})
print(df.dtypes)  # tudo "object" (texto), mesmo preco e quantidade

# Limpando texto antes de converter: remover "R$", espaço e trocar vírgula por ponto
df["preco"] = (
    df["preco"]
    .str.replace("R$", "", regex=False)
    .str.replace(",", ".", regex=False)
    .str.strip()
)
df["preco"] = df["preco"].astype(float)
print(df["preco"])
print(df["preco"].dtype)  # float64

# pd.to_numeric -- converte para número, com controle sobre erros de conversão
# errors="coerce" transforma valores que não dão para converter em NaN, em vez de quebrar
df["quantidade"] = pd.to_numeric(df["quantidade"], errors="coerce")
print(df["quantidade"])
# 0    3.0
# 1    1.0
# 2    2.0
# 3    NaN   <- "cinco" não é um número, virou NaN em vez de dar erro
print(df["quantidade"].dtype)  # float64 (NaN obriga o tipo a ser float, não int)

# errors="raise" (padrão) -- gera erro se algum valor não puder ser convertido,
# útil quando você QUER ser avisado de dados inválidos em vez de ignorá-los
# pd.to_numeric(df["quantidade"], errors="raise")  # ex: dispararia ValueError

# Convertendo texto para booleano
df["em_estoque"] = df["em_estoque"].map({"sim": True, "nao": False})
print(df["em_estoque"])
print(df["em_estoque"].dtype)  # bool

# .astype() -- forma geral de converter tipo, quando os dados já estão "limpos"
# (sem texto misturado, sem símbolos)
df["quantidade_int"] = df["quantidade"].fillna(0).astype(int)
# fillna antes do astype(int) porque int não aceita NaN -- precisa resolver os
# ausentes primeiro (Tópico 1)

# category -- tipo especial para colunas de texto com poucos valores únicos repetidos,
# economiza memória e deixa algumas operações mais rápidas
df["produto"] = df["produto"].astype("category")
print(df["produto"].dtype)  # category

print(df.dtypes)
```

## Erros comuns de quem está começando

- Usar `.astype(float)` direto numa coluna de texto com símbolos (`"R$"`,
  `","`, espaços) sem limpar antes — gera erro, porque `"R$ 2,50"` não é um
  número válido em Python/Pandas. Sempre limpar o texto primeiro (remover
  símbolos, trocar vírgula por ponto) e só depois converter.
- Usar `errors="coerce"` sem depois checar quantos `NaN` foram criados —
  isso silenciosamente descarta dados inválidos como se fossem ausentes; é
  importante rodar `.isnull().sum()` (Tópico 1) depois da conversão para
  saber quantos valores realmente não puderam ser convertidos.
- Tentar `.astype(int)` numa coluna com `NaN` — inteiros do NumPy/Pandas
  não suportam `NaN` nativamente (só float suporta), então é preciso
  resolver os valores ausentes antes (com `fillna`) ou usar o tipo especial
  `Int64` (com I maiúsculo) do Pandas, que aceita `NaN`.

## Exercício prático

```python
df = pd.DataFrame({
    "produto": ["Caneta", "Caderno", "Mochila"],
    "preco_texto": ["2.50 reais", "15.90 reais", "89.90 reais"],
    "avaliacao": ["4.5", "N/A", "3.8"],
})
```

1. Limpe a coluna `preco_texto` (remova o texto `" reais"`) e converta para
   `float`, guardando em uma nova coluna `preco`.
2. Converta `avaliacao` para número usando `pd.to_numeric` com
   `errors="coerce"`, guardando em uma coluna `avaliacao_num` (o valor
   `"N/A"` deve virar `NaN`).
3. Confira quantos valores viraram `NaN` na conversão do item 2.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

df = pd.DataFrame({
    "produto": ["Caneta", "Caderno", "Mochila"],
    "preco_texto": ["2.50 reais", "15.90 reais", "89.90 reais"],
    "avaliacao": ["4.5", "N/A", "3.8"],
})

df["preco"] = df["preco_texto"].str.replace(" reais", "", regex=False).astype(float)
print(df["preco"])

df["avaliacao_num"] = pd.to_numeric(df["avaliacao"], errors="coerce")
print(df["avaliacao_num"])

print(df["avaliacao_num"].isnull().sum())  # 1
```

</details>

## Checklist antes de avançar

- [ ] Sei limpar texto (remover símbolos, trocar separador decimal) antes de converter para número
- [ ] Sei usar `pd.to_numeric(..., errors="coerce")` e checar quantos `NaN` foram criados
- [ ] Sei que `int` não aceita `NaN` e por isso preciso tratar ausentes antes de converter
- [ ] Resolvi o exercício sem olhar a solução
