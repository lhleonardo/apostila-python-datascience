# Checklist de qualidade de dados

> Módulo 5 — Limpeza de Dados · Tópico 7 de 7 (último do módulo)

## O que é e por que importa

Os tópicos anteriores trataram cada problema de limpeza separadamente
(ausentes, duplicatas, tipos, texto, datas, outliers). Na prática, ao
receber um dataset novo, você não sabe de antemão quais desses problemas
existem — é preciso um **processo sistemático** para descobrir. Este último
tópico junta tudo em um roteiro de diagnóstico que você pode aplicar a
qualquer dataset novo, do início ao fim, antes de partir para análise de
verdade (Módulo 6).

## Como funciona (com exemplo comentado)

```python
import pandas as pd
import numpy as np

# Dataset fictício com vários problemas de uma vez, para praticar o roteiro completo
from io import StringIO

csv_texto = """produto,categoria,preco,quantidade,data_venda
Caneta Azul,Papelaria,R$ 2,50,3,10/01/2024
Caderno, papelaria ,R$ 15,90,1,15/01/2024
Mochila,Acessorios,R$ 89,90,2,02/02/2024
Caneta Azul,Papelaria,R$ 2,50,3,10/01/2024
Lapis HB,Papelaria,R$ 1,20,,28/02/2024
Estojo,acessorios,R$ 25,00,999,05/03/2024
"""
df = pd.read_csv(StringIO(csv_texto))

# ROTEIRO DE DIAGNÓSTICO

# 1. Visão geral: shape, tipos, primeiras linhas
print(df.shape)
df.info()
print(df.head())

# 2. Valores ausentes (Tópico 1)
print(df.isnull().sum())
# "quantidade" tem 1 ausente

# 3. Duplicatas (Tópico 2)
print(df.duplicated().sum())
# 1 linha duplicada (Caneta Azul aparece duas vezes, idêntica)

# 4. Tipos de dados suspeitos (Tópico 3)
print(df.dtypes)
# "preco" é object (por causa do "R$" e da vírgula) -- deveria ser float
# "data_venda" é object -- deveria ser datetime

# 5. Inconsistências de texto (Tópico 4)
print(df["categoria"].unique())
# ['Papelaria' ' papelaria ' 'Acessorios' 'acessorios'] -- 4 valores para só 2 categorias reais

# 6. Valores fora do esperado / outliers (Tópico 6)
print(df["quantidade"].describe())
# 999 destoa completamente do resto (3, 1, 2) -- provável erro de digitação

# APLICANDO AS CORREÇÕES, NA ORDEM QUE FAZ SENTIDO PARA ESTE CASO:

# a) remover duplicatas exatas primeiro (evita distorcer os passos seguintes)
df = df.drop_duplicates().reset_index(drop=True)

# b) corrigir tipo de preco
df["preco"] = (
    df["preco"].str.replace("R$", "", regex=False)
    .str.replace(",", ".", regex=False)
    .str.strip()
    .astype(float)
)

# c) corrigir tipo de data
df["data_venda"] = pd.to_datetime(df["data_venda"], format="%d/%m/%Y")

# d) padronizar texto de categoria
df["categoria"] = df["categoria"].str.strip().str.lower()

# e) tratar outlier em quantidade (999 claramente é erro -- decide-se remover a linha)
df = df[df["quantidade"] != 999]

# f) tratar valor ausente em quantidade (preenchendo com a mediana, já sem o outlier)
df["quantidade"] = df["quantidade"].fillna(df["quantidade"].median())

# Checagem final -- confirma que os problemas foram resolvidos
print(df.isnull().sum().sum())   # 0
print(df.duplicated().sum())     # 0
print(df.dtypes)                 # preco float64, data_venda datetime64
print(df["categoria"].unique())  # só 2 valores, padronizados
print(df)
```

## Erros comuns de quem está começando

- Aplicar as correções em ordem aleatória, sem pensar nas dependências entre
  elas — por exemplo, calcular uma mediana para preencher ausentes **antes**
  de remover um outlier que distorce essa mediana, ou tentar converter tipo
  antes de limpar o texto que impede a conversão.
- Corrigir só o que "salta aos olhos" numa primeira olhada, sem rodar o
  roteiro completo (ausentes, duplicatas, tipos, texto, outliers) em cada
  coluna — problemas de qualidade de dados raramente vêm um de cada vez.
- Não validar o resultado final. Depois de limpar, é fácil assumir que "deu
  certo" sem checar de novo `isnull().sum()`, `duplicated().sum()`,
  `dtypes` e `.unique()` das colunas de texto — a validação final é parte do
  processo, não um passo opcional.

## Exercício prático

```python
csv_texto = """cliente,cidade,valor_compra,data
Marcos,  Sao Paulo,R$ 150,00,12/03/2024
Julia,Rio de Janeiro ,R$ 89,90,15/03/2024
Marcos,  Sao Paulo,R$ 150,00,12/03/2024
Pedro,rio de janeiro,R$ -20,00,20/03/2024
Ana,Belo Horizonte,R$ 300,50,
"""
```

Aplique o roteiro completo de diagnóstico e limpeza neste dataset:

1. Rode o diagnóstico (`.info()`, `.isnull().sum()`, `.duplicated().sum()`,
   `.unique()` das colunas de texto) e liste os problemas encontrados.
2. Remova duplicatas exatas.
3. Converta `valor_compra` para `float` (removendo `"R$"` e trocando vírgula
   por ponto).
4. Padronize `cidade` (remova espaços, deixe minúsculo).
5. Trate o valor `R$ -20,00` (compra com valor negativo — decida remover a
   linha, já que valor de compra negativo não faz sentido de negócio).
6. Converta `data` para `datetime`, com `errors="coerce"` (a última linha
   não tem data).
7. Valide o resultado final.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd
from io import StringIO

csv_texto = """cliente,cidade,valor_compra,data
Marcos,  Sao Paulo,150.00,12/03/2024
Julia,Rio de Janeiro ,89.90,15/03/2024
Marcos,  Sao Paulo,150.00,12/03/2024
Pedro,rio de janeiro,-20.00,20/03/2024
Ana,Belo Horizonte,300.50,
"""
# nota: para simplificar o parse do CSV neste exemplo, "R$" foi removido direto
# do texto de entrada -- na prática, essa limpeza aconteceria em código, como
# visto no Tópico 3

df = pd.read_csv(StringIO(csv_texto))

df.info()
print(df.isnull().sum())
print(df.duplicated().sum())
print(df["cidade"].unique())

df = df.drop_duplicates().reset_index(drop=True)

df["cidade"] = df["cidade"].str.strip().str.lower()

df = df[df["valor_compra"] >= 0]

df["data"] = pd.to_datetime(df["data"], format="%d/%m/%Y", errors="coerce")

print(df.isnull().sum())
print(df.duplicated().sum())
print(df.dtypes)
print(df["cidade"].unique())
print(df)
```

</details>

## Checklist antes de avançar

- [ ] Tenho um roteiro mental para diagnosticar um dataset novo (ausentes, duplicatas, tipos, texto, outliers)
- [ ] Sei pensar na ordem correta de aplicar correções (dependências entre elas)
- [ ] Sempre valido o resultado final depois de limpar
- [ ] Resolvi o exercício sem olhar a solução

## Checklist do Módulo 5

Antes de seguir para o Módulo 6 (Estatística e EDA), confirme que você
consegue, sem consultar a apostila:

- [ ] Decidir entre remover, preencher com estatística geral ou preencher por grupo para valores ausentes
- [ ] Identificar e remover duplicatas, com e sem `subset`
- [ ] Converter colunas de texto "sujo" para tipos numéricos e de data
- [ ] Padronizar texto (espaços, capitalização, acentos)
- [ ] Detectar outliers com IQR ou z-score, e escolher um tratamento justificado
- [ ] Aplicar um roteiro completo de diagnóstico e limpeza a um dataset novo

Pronto? Siga para o [Módulo 6 — Estatística e EDA](../06-estatistica-e-eda/00-indice.md).
