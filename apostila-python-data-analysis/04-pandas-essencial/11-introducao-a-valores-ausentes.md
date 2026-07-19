# Introdução a valores ausentes

> Módulo 4 — Pandas Essencial · Tópico 11 de 12

## O que é e por que importa

Dados reais quase sempre têm buracos: um cliente sem telefone cadastrado, uma
venda sem a categoria preenchida, uma medição que falhou naquele dia. Pandas
representa esses buracos como `NaN` (*Not a Number*), e saber identificá-los,
contá-los e decidir o que fazer com eles é essencial antes de calcular
qualquer estatística — uma média calculada sem perceber valores ausentes
pode dar um resultado enganoso.

Este tópico é só uma introdução ao tema — o **Módulo 5 (Limpeza de Dados)**
aprofunda estratégias de tratamento. Aqui o objetivo é reconhecer valores
ausentes e saber as operações básicas para lidar com eles.

## Como funciona (com exemplo comentado)

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "produto": ["Caneta Azul", "Caderno", "Mochila", "Lapis HB"],
    "categoria": ["Papelaria", None, "Acessorios", "Papelaria"],
    "quantidade": [3, 1, np.nan, 5],
    "preco_unitario": [2.50, 15.90, 89.90, np.nan],
})
print(df)
#        produto   categoria  quantidade  preco_unitario
# 0  Caneta Azul   Papelaria         3.0            2.50
# 1      Caderno        None         1.0           15.90
# 2      Mochila  Acessorios         NaN           89.90
# 3     Lapis HB   Papelaria         5.0             NaN

# .isnull() (ou .isna(), são sinônimos) -- retorna True onde o valor é ausente
print(df.isnull())

# Contar valores ausentes por coluna -- o padrão mais usado no dia a dia
print(df.isnull().sum())
# produto           0
# categoria         1
# quantidade        1
# preco_unitario    1
# dtype: int64

# Porcentagem de valores ausentes por coluna
print((df.isnull().sum() / len(df)) * 100)

# .notnull() -- o oposto, True onde o valor EXISTE
print(df["categoria"].notnull())

# Filtrar linhas com valor ausente numa coluna específica (combina com Tópico 5)
sem_categoria = df[df["categoria"].isnull()]
print(sem_categoria)

# Filtrar linhas SEM valores ausentes numa coluna
com_categoria = df[df["categoria"].notnull()]
print(com_categoria)

# .dropna() -- remove linhas com QUALQUER valor ausente (padrão)
df_sem_nulos = df.dropna()
print(df_sem_nulos)  # só sobra a linha 0, já que as outras têm pelo menos um NaN

# dropna(subset=[...]) -- remove linhas só considerando colunas específicas
df_sem_nulos_preco = df.dropna(subset=["preco_unitario"])
print(df_sem_nulos_preco)

# .fillna() -- preenche valores ausentes com algo no lugar de remover a linha
df_preenchido = df.fillna({
    "categoria": "Sem categoria",
    "quantidade": 0,
})
print(df_preenchido)
# preco_unitario continua com NaN porque não foi incluído no dicionário

# Preencher com a média da própria coluna -- estratégia comum para números
media_preco = df["preco_unitario"].mean()
df["preco_unitario"] = df["preco_unitario"].fillna(media_preco)
print(df["preco_unitario"])
```

A decisão entre **remover** (`dropna`) e **preencher** (`fillna`) depende do
contexto: remover é mais simples mas perde dados (e pode enviesar a análise
se os ausentes não forem aleatórios); preencher mantém as linhas mas exige
escolher um valor razoável — usar a média, um valor fixo, ou olhar para
colunas relacionadas. O Módulo 5 explora essas estratégias com mais calma.

## Erros comuns de quem está começando

- Calcular médias/somas sem checar `.isnull().sum()` antes, sem perceber que
  a agregação está "ignorando" os `NaN` silenciosamente (é o comportamento
  padrão do Pandas) e sem saber quantos valores ficaram de fora dessa conta.
- Usar `== np.nan` para checar se um valor é ausente — isso **nunca** funciona
  (`NaN != NaN` é uma peculiaridade matemática), o correto é sempre
  `.isnull()`/`.isna()`.
- Chamar `.dropna()` sem `subset` quando só uma coluna específica importa,
  perdendo linhas inteiras por causa de um valor ausente numa coluna que nem
  seria usada na análise.

## Exercício prático

```python
df = pd.DataFrame({
    "cliente": ["Marcos", "Julia", "Pedro", "Ana"],
    "email": ["marcos@x.com", None, "pedro@x.com", None],
    "idade": [34, 28, np.nan, 41],
    "cidade": ["São Paulo", "Rio de Janeiro", "Belo Horizonte", None],
})
```

1. Conte quantos valores ausentes existem em cada coluna.
2. Filtre e imprima só os clientes sem `email` cadastrado.
3. Crie uma cópia do DataFrame preenchendo `email` ausente com o texto
   `"não informado"` e `idade` ausente com a média das idades existentes.
4. Remova as linhas onde `cidade` está ausente (use `dropna` com `subset`).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "cliente": ["Marcos", "Julia", "Pedro", "Ana"],
    "email": ["marcos@x.com", None, "pedro@x.com", None],
    "idade": [34, 28, np.nan, 41],
    "cidade": ["São Paulo", "Rio de Janeiro", "Belo Horizonte", None],
})

print(df.isnull().sum())

sem_email = df[df["email"].isnull()]
print(sem_email)

df_preenchido = df.fillna({
    "email": "não informado",
    "idade": df["idade"].mean(),
})
print(df_preenchido)

df_sem_cidade_ausente = df.dropna(subset=["cidade"])
print(df_sem_cidade_ausente)
```

</details>

## Checklist antes de avançar

- [ ] Sei identificar e contar valores ausentes com `.isnull().sum()`
- [ ] Sei filtrar linhas com/sem valores ausentes numa coluna
- [ ] Sei a diferença entre `dropna()` e `fillna()` e quando usar cada um
- [ ] Resolvi o exercício sem olhar a solução
