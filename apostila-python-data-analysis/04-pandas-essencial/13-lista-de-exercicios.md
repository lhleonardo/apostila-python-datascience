# Lista de exercícios — Módulo 4

> Módulo 4 — Pandas Essencial · Lista de exercícios de revisão

Esta lista reúne 10 exercícios práticos para cada tópico do módulo, para
consolidar o que foi aprendido antes de avançar. Tente resolver cada
exercício sem consultar o tópico original primeiro — as soluções vêm logo
depois de cada bloco, dentro de um "clique para ver".

## 1. Introdução ao Pandas: Series e DataFrame

1. Crie uma Series chamada `notas` com os valores `[8.5, 7.0, 9.5, 6.0]`,
   sem definir índice, e imprima-a.
2. Crie uma Series com índice `["Jan", "Fev", "Mar"]` e valores
   `[100, 150, 130]` representando vendas mensais. Acesse o valor de `"Fev"`
   pelo rótulo.
3. Crie um DataFrame `alunos` com colunas `nome` (`["Ana", "Bruno", "Carla"]`)
   e `nota` (`[8.0, 6.5, 9.0]`).
4. Imprima o `shape` do DataFrame `alunos`.
5. Imprima `alunos.columns` e `alunos.index`.
6. Selecione a coluna `nome` de `alunos` como Series e confirme o tipo com
   `type(...)`.
7. Selecione a coluna `nome` de `alunos` como DataFrame de uma coluna só
   (usando colchete duplo).
8. Imprima `alunos.dtypes` e explique (em comentário) por que a coluna
   `nome` aparece como `object`.
9. Crie um DataFrame `estoque` com colunas `produto`
   (`["Caneta", "Caderno", "Mochila"]`), `quantidade` (`[50, 20, 5]`) e
   `preco` (`[2.5, 15.9, 89.9]`), com índice `["p1", "p2", "p3"]`.
10. A partir de `estoque`, imprima só a coluna `quantidade` como Series e
    depois as colunas `produto` e `preco` juntas como DataFrame.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd

notas = pd.Series([8.5, 7.0, 9.5, 6.0])
print(notas)
```

**2.**
```python
import pandas as pd

vendas = pd.Series([100, 150, 130], index=["Jan", "Fev", "Mar"])
print(vendas["Fev"])  # 150
```

**3.**
```python
import pandas as pd

alunos = pd.DataFrame({
    "nome": ["Ana", "Bruno", "Carla"],
    "nota": [8.0, 6.5, 9.0],
})
print(alunos)
```

**4.**
```python
print(alunos.shape)  # (3, 2)
```

**5.**
```python
print(alunos.columns)  # Index(['nome', 'nota'], dtype='object')
print(alunos.index)    # RangeIndex(start=0, stop=3, step=1)
```

**6.**
```python
nomes = alunos["nome"]
print(type(nomes))  # <class 'pandas.core.series.Series'>
```

**7.**
```python
nomes_df = alunos[["nome"]]
print(type(nomes_df))  # <class 'pandas.core.frame.DataFrame'>
```

**8.**
```python
print(alunos.dtypes)
# nome aparece como object porque colunas de texto guardam referências a
# objetos Python, não um tipo numérico "puro" do NumPy
```

**9.**
```python
import pandas as pd

estoque = pd.DataFrame({
    "produto": ["Caneta", "Caderno", "Mochila"],
    "quantidade": [50, 20, 5],
    "preco": [2.5, 15.9, 89.9],
}, index=["p1", "p2", "p3"])
print(estoque)
```

**10.**
```python
print(estoque["quantidade"])
print(estoque[["produto", "preco"]])
```

</details>

## 2. Lendo e escrevendo dados (CSV, Excel, JSON)

1. Usando `StringIO`, crie um CSV inline com colunas `produto,preco` e 3
   linhas de dados, e carregue-o com `pd.read_csv`.
2. Crie um CSV inline usando `;` como separador (colunas `nome;idade`) e
   leia-o corretamente com `pd.read_csv(..., sep=";")`.
3. A partir do DataFrame do exercício 1, salve-o em `produtos_ex2.csv` com
   `index=False`.
4. Leia `produtos_ex2.csv` de volta e confirme que tem as mesmas colunas do
   original.
5. Crie um CSV inline com uma coluna a mais do que você precisa e leia
   apenas duas colunas específicas usando `usecols`.
6. Crie um CSV inline com pelo menos 5 linhas e leia só as 2 primeiras
   usando `nrows`.
7. Crie uma lista de dicionários em Python representando 2 pedidos
   (`pedido_id`, `valor`), converta para uma string JSON com `json.dumps` e
   carregue com `pd.read_json` (via `StringIO`).
8. Salve o DataFrame do exercício 7 em `pedidos_ex7.json` usando
   `orient="records"`.
9. Crie um CSV inline com uma coluna que deveria ser o índice (por exemplo
   `id`) e leia usando `index_col=0`.
10. Repita o exercício 3, mas agora sem `index=False`; leia o arquivo gerado
    de volta e observe a coluna extra `Unnamed: 0` que aparece.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd
from io import StringIO

csv_texto = """produto,preco
Caneta,2.5
Caderno,15.9
Mochila,89.9
"""
df = pd.read_csv(StringIO(csv_texto))
print(df)
```

**2.**
```python
import pandas as pd
from io import StringIO

csv_texto = "nome;idade\nMarcos;34\nJulia;28\n"
df = pd.read_csv(StringIO(csv_texto), sep=";")
print(df)
```

**3.**
```python
df.to_csv("produtos_ex2.csv", index=False)
```

**4.**
```python
df_lido = pd.read_csv("produtos_ex2.csv")
print(df_lido.columns.tolist() == df.columns.tolist())  # True
```

**5.**
```python
import pandas as pd
from io import StringIO

csv_texto = """produto,preco,fabricante
Caneta,2.5,ACME
Caderno,15.9,ACME
"""
df_parcial = pd.read_csv(StringIO(csv_texto), usecols=["produto", "preco"])
print(df_parcial)
```

**6.**
```python
import pandas as pd
from io import StringIO

csv_texto = """produto,preco
A,1
B,2
C,3
D,4
E,5
"""
df_top = pd.read_csv(StringIO(csv_texto), nrows=2)
print(df_top)
```

**7.**
```python
import pandas as pd
import json
from io import StringIO

pedidos = [
    {"pedido_id": 1, "valor": 150.0},
    {"pedido_id": 2, "valor": 89.9},
]
dados_json = json.dumps(pedidos)
df_json = pd.read_json(StringIO(dados_json))
print(df_json)
```

**8.**
```python
df_json.to_json("pedidos_ex7.json", orient="records", indent=2)
```

**9.**
```python
import pandas as pd
from io import StringIO

csv_texto = """id,nome
1,Marcos
2,Julia
"""
df_indexado = pd.read_csv(StringIO(csv_texto), index_col=0)
print(df_indexado)
```

**10.**
```python
df.to_csv("produtos_ex10.csv")  # sem index=False
df_com_extra = pd.read_csv("produtos_ex10.csv")
print(df_com_extra.columns.tolist())  # inclui "Unnamed: 0"
```

</details>

## 3. Explorando um DataFrame

Use este DataFrame para os exercícios:

```python
import pandas as pd
from io import StringIO

csv_texto = """produto,categoria,quantidade,preco_unitario
Caneta,Papelaria,10,2.5
Caderno,Papelaria,5,15.9
Mochila,Acessorios,3,89.9
Estojo,Acessorios,,25.0
Lapis,Papelaria,20,1.2
"""
df = pd.read_csv(StringIO(csv_texto))
```

1. Rode `.head(2)` e `.tail(2)`.
2. Imprima o `.shape` do DataFrame.
3. Rode `.info()` e identifique qual coluna tem valor ausente.
4. Rode `.describe()` e identifique o `preco_unitario` médio.
5. Rode `.describe(include="object")` e identifique quantos valores únicos a
   coluna `categoria` tem.
6. Use `.value_counts()` na coluna `categoria`.
7. Use `.nunique()` na coluna `produto`.
8. Use `.isnull().sum()` para contar valores ausentes por coluna.
9. Imprima `.dtypes` e `.columns.tolist()`.
10. Descubra, usando `.describe()`, qual é o maior valor de `quantidade` sem
    olhar o DataFrame inteiro (só a saída do `describe`).

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
print(df.head(2))
print(df.tail(2))
```

**2.**
```python
print(df.shape)  # (5, 4)
```

**3.**
```python
df.info()
# "quantidade" tem 1 valor ausente
```

**4.**
```python
print(df.describe())
# mean de preco_unitario é aproximadamente 26.9
```

**5.**
```python
print(df.describe(include="object"))
# categoria tem 2 valores únicos
```

**6.**
```python
print(df["categoria"].value_counts())
```

**7.**
```python
print(df["produto"].nunique())  # 5
```

**8.**
```python
print(df.isnull().sum())
```

**9.**
```python
print(df.dtypes)
print(df.columns.tolist())
```

**10.**
```python
print(df.describe())
# max de quantidade é 20
```

</details>

## 4. Seleção e indexação (loc, iloc)

Use este DataFrame para os exercícios:

```python
import pandas as pd

df = pd.DataFrame({
    "cidade": ["São Paulo", "Rio de Janeiro", "Curitiba", "Salvador", "Recife"],
    "populacao_milhoes": [12.3, 6.7, 1.9, 2.9, 1.6],
    "regiao": ["Sudeste", "Sudeste", "Sul", "Nordeste", "Nordeste"],
}, index=["c1", "c2", "c3", "c4", "c5"])
```

1. Use `.loc` para selecionar a linha `"c1"`.
2. Use `.iloc` para selecionar a linha de posição 2.
3. Use `.loc` para selecionar as linhas de `"c2"` até `"c4"` (inclusive).
4. Use `.iloc` para selecionar as linhas de posição 1 até 3 (sem incluir a
   posição 3).
5. Use `.loc` para pegar a `populacao_milhoes` da cidade `"c5"`.
6. Use `.iloc` para pegar a célula da linha de posição 0, coluna de posição
   1.
7. Use `.loc` para selecionar as colunas `cidade` e `regiao` das linhas
   `"c1"` e `"c3"`.
8. Use `.iloc` para selecionar as linhas de posição 0 e 4, colunas de
   posição 0 e 2.
9. Use `.loc[:, "regiao"]` para pegar a coluna `regiao` inteira.
10. Crie `df_padrao = df.reset_index(drop=True)` e mostre a diferença entre
    `df_padrao.loc[0:2]` e `df_padrao.iloc[0:2]`.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
print(df.loc["c1"])
```

**2.**
```python
print(df.iloc[2])
```

**3.**
```python
print(df.loc["c2":"c4"])
```

**4.**
```python
print(df.iloc[1:3])
```

**5.**
```python
print(df.loc["c5", "populacao_milhoes"])  # 1.6
```

**6.**
```python
print(df.iloc[0, 1])  # 12.3
```

**7.**
```python
print(df.loc[["c1", "c3"], ["cidade", "regiao"]])
```

**8.**
```python
print(df.iloc[[0, 4], [0, 2]])
```

**9.**
```python
print(df.loc[:, "regiao"])
```

**10.**
```python
df_padrao = df.reset_index(drop=True)
print(df_padrao.loc[0:2])   # inclui as posições 0, 1 e 2
print(df_padrao.iloc[0:2])  # inclui só as posições 0 e 1
```

</details>

## 5. Filtragem de dados

Use este DataFrame para os exercícios:

```python
import pandas as pd

df = pd.DataFrame({
    "produto": ["Caneta", "Caderno", "Mochila", "Estojo", "Lapis", "Borracha"],
    "categoria": ["Papelaria", "Papelaria", "Acessorios", "Acessorios", "Papelaria", "Papelaria"],
    "quantidade": [10, 5, 3, 4, 20, 15],
    "preco_unitario": [2.5, 15.9, 89.9, 25.0, 1.2, 0.9],
})
```

1. Filtre os produtos com `quantidade` maior que 5.
2. Filtre os produtos com `preco_unitario` menor ou igual a 2.
3. Filtre os produtos da categoria `"Acessorios"`.
4. Filtre os produtos da categoria `"Papelaria"` com `quantidade` maior que
   10 (use `&`).
5. Filtre os produtos com `preco_unitario` maior que 50 ou `quantidade`
   maior que 15 (use `|`).
6. Use `.isin()` para filtrar os produtos `"Caneta"`, `"Lapis"` e
   `"Borracha"`.
7. Use `~` para filtrar os produtos que NÃO são da categoria `"Papelaria"`.
8. Use `.query()` para obter os produtos com `preco_unitario > 10` e
   `categoria == 'Acessorios'`.
9. Use `.loc` para obter só a coluna `produto` dos itens com `quantidade`
   menor que 5.
10. Combine três condições: produtos da categoria `"Papelaria"`, com
    `quantidade` maior que 5 e `preco_unitario` menor que 2.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
print(df[df["quantidade"] > 5])
```

**2.**
```python
print(df[df["preco_unitario"] <= 2])
```

**3.**
```python
print(df[df["categoria"] == "Acessorios"])
```

**4.**
```python
print(df[(df["categoria"] == "Papelaria") & (df["quantidade"] > 10)])
```

**5.**
```python
print(df[(df["preco_unitario"] > 50) | (df["quantidade"] > 15)])
```

**6.**
```python
print(df[df["produto"].isin(["Caneta", "Lapis", "Borracha"])])
```

**7.**
```python
print(df[~(df["categoria"] == "Papelaria")])
```

**8.**
```python
print(df.query("preco_unitario > 10 and categoria == 'Acessorios'"))
```

**9.**
```python
print(df.loc[df["quantidade"] < 5, "produto"])
```

**10.**
```python
print(df[(df["categoria"] == "Papelaria") & (df["quantidade"] > 5) & (df["preco_unitario"] < 2)])
```

</details>

## 6. Criando e modificando colunas

Use este DataFrame para os exercícios:

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "produto": ["Caneta", "Caderno", "Mochila", "Estojo"],
    "quantidade": [10, 5, 3, 4],
    "preco_unitario": [2.5, 15.9, 89.9, 25.0],
})
```

1. Crie a coluna `total` (`quantidade * preco_unitario`).
2. Aplique um reajuste de 15% na coluna `preco_unitario` (multiplique por
   1.15).
3. Crie a coluna `caro` com `True` quando `total` for maior que 100, `False`
   caso contrário, usando `.loc`.
4. Crie a mesma coluna do item 3, mas chamada `caro_np`, usando `np.where`.
5. Renomeie a coluna `produto` para `nome_produto` (lembre de reatribuir).
6. Remova a coluna `caro_np` com `.drop(columns=...)`.
7. Use `.apply()` para criar a coluna `nivel_estoque`: `"alto"` se
   `quantidade >= 8`, `"medio"` se `quantidade >= 4`, senão `"baixo"`.
8. Use `.apply(..., axis=1)` para criar a coluna `descricao` com o texto
   `"{nome_produto}: R$ {preco_unitario}"`.
9. Mude o tipo da coluna `quantidade` para `float` usando `.astype()` e
   confirme com `.dtype`.
10. Crie a coluna `preco_com_desconto` aplicando 10% de desconto só nos
    produtos com `total` maior que 50, mantendo o preço original nos demais
    (dica: `.loc` combinado com filtro).

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
df["total"] = df["quantidade"] * df["preco_unitario"]
```

**2.**
```python
df["preco_unitario"] = df["preco_unitario"] * 1.15
```

**3.**
```python
df["caro"] = False
df.loc[df["total"] > 100, "caro"] = True
```

**4.**
```python
df["caro_np"] = np.where(df["total"] > 100, True, False)
```

**5.**
```python
df = df.rename(columns={"produto": "nome_produto"})
```

**6.**
```python
df = df.drop(columns=["caro_np"])
```

**7.**
```python
def classificar(qtd):
    if qtd >= 8:
        return "alto"
    elif qtd >= 4:
        return "medio"
    return "baixo"

df["nivel_estoque"] = df["quantidade"].apply(classificar)
```

**8.**
```python
df["descricao"] = df.apply(
    lambda linha: f"{linha['nome_produto']}: R$ {linha['preco_unitario']}", axis=1
)
```

**9.**
```python
df["quantidade"] = df["quantidade"].astype(float)
print(df["quantidade"].dtype)  # float64
```

**10.**
```python
df["preco_com_desconto"] = df["preco_unitario"]
df.loc[df["total"] > 50, "preco_com_desconto"] = df["preco_unitario"] * 0.9
```

</details>

## 7. Ordenação

Use este DataFrame para os exercícios:

```python
import pandas as pd

df = pd.DataFrame({
    "aluno": ["Marcos", "Julia", "Pedro", "Ana", "Carlos", "Beatriz"],
    "nota": [7.5, 9.0, 5.5, 9.0, 6.0, 8.5],
    "turma": ["A", "B", "A", "B", "A", "B"],
})
```

1. Ordene o DataFrame por `nota`, do menor para o maior.
2. Ordene o DataFrame por `nota`, do maior para o menor.
3. Obtenha os 3 alunos com as maiores notas usando `.nlargest()`.
4. Obtenha os 2 alunos com as menores notas usando `.nsmallest()`.
5. Ordene por `turma` (A-Z) e, dentro de cada turma, por `nota` (maior para
   menor).
6. Ordene por `nota` decrescente e resete o índice para ficar sequencial,
   descartando o índice antigo.
7. Embaralhe as linhas com `df.sample(frac=1)` e depois use `.sort_index()`
   para voltar à ordem original.
8. Ordene por `turma` (Z-A) e, dentro de cada turma, por `nota` (menor para
   maior).
9. Combine ordenação e filtragem: filtre só os alunos da turma `"A"` e
   ordene o resultado por `nota` decrescente.
10. Combine ordenação e seleção: descubra o nome do aluno com a maior nota
    usando `.sort_values()` e `.iloc[0]`.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
print(df.sort_values("nota"))
```

**2.**
```python
print(df.sort_values("nota", ascending=False))
```

**3.**
```python
print(df.nlargest(3, "nota"))
```

**4.**
```python
print(df.nsmallest(2, "nota"))
```

**5.**
```python
print(df.sort_values(["turma", "nota"], ascending=[True, False]))
```

**6.**
```python
resultado = df.sort_values("nota", ascending=False).reset_index(drop=True)
print(resultado)
```

**7.**
```python
embaralhado = df.sample(frac=1)
print(embaralhado.sort_index())
```

**8.**
```python
print(df.sort_values(["turma", "nota"], ascending=[False, True]))
```

**9.**
```python
turma_a = df[df["turma"] == "A"].sort_values("nota", ascending=False)
print(turma_a)
```

**10.**
```python
maior_nota = df.sort_values("nota", ascending=False).iloc[0]["aluno"]
print(maior_nota)  # Julia (empate com Ana, mas Julia aparece primeiro na ordenação estável)
```

</details>

## 8. Agrupamento com groupby

Use este DataFrame para os exercícios:

```python
import pandas as pd

df = pd.DataFrame({
    "vendedor": ["Marcos", "Julia", "Marcos", "Pedro", "Julia", "Marcos", "Pedro"],
    "categoria": ["Papelaria", "Acessorios", "Papelaria", "Acessorios", "Papelaria", "Acessorios", "Papelaria"],
    "quantidade": [3, 1, 2, 5, 4, 2, 6],
    "valor": [7.5, 89.9, 5.0, 125.0, 6.0, 179.8, 15.0],
})
```

1. Agrupe por `vendedor` e calcule a soma de `valor`.
2. Agrupe por `vendedor` e calcule a média de `quantidade`.
3. Agrupe por `categoria` e conte quantas vendas (linhas) existem em cada
   uma, usando `.size()`.
4. Agrupe por `vendedor` e descubra o maior `valor` de cada um.
5. Agrupe por `vendedor` e `categoria` juntos, somando `valor`.
6. Agrupe por `categoria` e agregue as colunas `quantidade` e `valor` de
   uma vez, somando ambas.
7. Depois do exercício 6, use `.reset_index()` no resultado para transformar
   `categoria` de volta em coluna normal.
8. Combine `groupby` com ordenação: agrupe por `vendedor`, some `valor`,
   resete o índice e ordene do maior para o menor.
9. Agrupe por `vendedor` e calcule a soma de `valor`, depois filtre (fora do
   groupby) só os vendedores com soma maior que 50.
10. Agrupe por `categoria` e calcule a média de `valor`; explique (em
    comentário) por que seria um erro tentar `.mean()` na coluna `vendedor`
    do mesmo agrupamento.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
print(df.groupby("vendedor")["valor"].sum())
```

**2.**
```python
print(df.groupby("vendedor")["quantidade"].mean())
```

**3.**
```python
print(df.groupby("categoria").size())
```

**4.**
```python
print(df.groupby("vendedor")["valor"].max())
```

**5.**
```python
print(df.groupby(["vendedor", "categoria"])["valor"].sum())
```

**6.**
```python
resumo = df.groupby("categoria")[["quantidade", "valor"]].sum()
print(resumo)
```

**7.**
```python
resumo_tabela = resumo.reset_index()
print(resumo_tabela)
```

**8.**
```python
total_por_vendedor = df.groupby("vendedor")["valor"].sum().reset_index()
print(total_por_vendedor.sort_values("valor", ascending=False))
```

**9.**
```python
soma = df.groupby("vendedor")["valor"].sum().reset_index()
print(soma[soma["valor"] > 50])
```

**10.**
```python
print(df.groupby("categoria")["valor"].mean())
# vendedor é uma coluna de texto -- .mean() não faz sentido matemático
# nela (o Pandas geraria erro ou exigiria seleção explícita de colunas
# numéricas)
```

</details>

## 9. Agregações com agg

Use este DataFrame para os exercícios:

```python
import pandas as pd

df = pd.DataFrame({
    "vendedor": ["Marcos", "Julia", "Marcos", "Pedro", "Julia", "Marcos", "Pedro"],
    "categoria": ["Papelaria", "Acessorios", "Papelaria", "Acessorios", "Papelaria", "Acessorios", "Papelaria"],
    "quantidade": [3, 1, 2, 5, 4, 2, 6],
    "valor": [7.5, 89.9, 5.0, 125.0, 6.0, 179.8, 15.0],
})
```

1. Agrupe por `vendedor` e use `.agg(["sum", "mean"])` na coluna `valor`.
2. Agrupe por `categoria` e use `.agg(["sum", "count", "max"])` na coluna
   `valor`.
3. Agrupe por `vendedor` e use um dicionário no `.agg()` para somar `valor`
   e calcular a média de `quantidade` ao mesmo tempo.
4. Agrupe por `categoria` e use named aggregation para criar `total_valor`
   (soma de `valor`) e `qtd_vendas` (contagem).
5. Agrupe por `vendedor` e use named aggregation para criar `ticket_medio`
   (média de `valor`) e `maior_venda` (máximo de `valor`).
6. Ordene o resultado do exercício 4 por `total_valor`, do maior para o
   menor.
7. Crie uma função personalizada `amplitude(serie)` que retorna
   `serie.max() - serie.min()` e use-a em `.agg()` na coluna `valor`,
   agrupado por `categoria`.
8. Combine `.agg(["mean", amplitude])` numa mesma chamada, agrupado por
   `vendedor`.
9. Sem `groupby`, use `.agg(["sum", "mean"])` diretamente nas colunas
   `quantidade` e `valor` do DataFrame inteiro, para obter um resumo geral.
10. Agrupe por `vendedor` e `categoria` juntos, usando named aggregation
    para `total_valor` (soma) e `qtd_vendas` (contagem), e depois resete o
    índice.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
print(df.groupby("vendedor")["valor"].agg(["sum", "mean"]))
```

**2.**
```python
print(df.groupby("categoria")["valor"].agg(["sum", "count", "max"]))
```

**3.**
```python
print(df.groupby("vendedor").agg({"valor": "sum", "quantidade": "mean"}))
```

**4.**
```python
resumo = df.groupby("categoria").agg(
    total_valor=("valor", "sum"),
    qtd_vendas=("valor", "count"),
)
print(resumo)
```

**5.**
```python
resumo_vendedor = df.groupby("vendedor").agg(
    ticket_medio=("valor", "mean"),
    maior_venda=("valor", "max"),
)
print(resumo_vendedor)
```

**6.**
```python
print(resumo.sort_values("total_valor", ascending=False))
```

**7.**
```python
def amplitude(serie):
    return serie.max() - serie.min()

print(df.groupby("categoria")["valor"].agg(amplitude))
```

**8.**
```python
print(df.groupby("vendedor")["valor"].agg(["mean", amplitude]))
```

**9.**
```python
print(df[["quantidade", "valor"]].agg(["sum", "mean"]))
```

**10.**
```python
resumo_dupla = df.groupby(["vendedor", "categoria"]).agg(
    total_valor=("valor", "sum"),
    qtd_vendas=("valor", "count"),
).reset_index()
print(resumo_dupla)
```

</details>

## 10. Merge, join e concatenação

Use estes DataFrames para os exercícios:

```python
import pandas as pd

clientes = pd.DataFrame({
    "cliente_id": [1, 2, 3],
    "nome": ["Marcos", "Julia", "Pedro"],
    "cidade": ["São Paulo", "Rio de Janeiro", "Curitiba"],
})

pedidos = pd.DataFrame({
    "pedido_id": [101, 102, 103, 104],
    "cliente_id": [1, 2, 1, 5],  # cliente_id 5 não existe em "clientes"
    "valor": [150.0, 89.9, 45.0, 200.0],
})

pedidos_marco = pd.DataFrame({
    "pedido_id": [105, 106],
    "cliente_id": [2, 3],
    "valor": [60.0, 30.0],
})
```

1. Empilhe `pedidos` e `pedidos_marco` com `pd.concat()`, usando
   `ignore_index=True`.
2. Faça `pd.merge(pedidos, clientes, on="cliente_id")` (padrão inner) e
   veja quantas linhas sobram.
3. Faça o mesmo merge com `how="left"`, mantendo todos os pedidos.
4. No resultado do item 3, identifique quais linhas têm `nome` como `NaN`.
5. Faça o merge com `how="right"`, mantendo todos os clientes (mesmo os sem
   pedidos).
6. Faça o merge com `how="outer"` e confira o número total de linhas.
7. No resultado do merge `how="left"` (item 3), crie uma coluna
   `pedido_valido` que seja `True` quando `nome` não é nulo, `False` caso
   contrário.
8. Concatene `clientes` com um novo DataFrame de mais um cliente
   (`cliente_id=4`, `nome="Ana"`, `cidade="Salvador"`) e confirme que o
   resultado tem 4 linhas.
9. Faça um merge entre `pedidos` e `clientes` usando `left_on="cliente_id"`
   e `right_on="cliente_id"` explicitamente (mesmo resultado que usar `on`).
10. A partir do merge `how="inner"` (item 2), agrupe por `cidade` e some
    `valor` (combinando com o Tópico 8).

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
todos_pedidos = pd.concat([pedidos, pedidos_marco], ignore_index=True)
print(todos_pedidos)
```

**2.**
```python
merge_inner = pd.merge(pedidos, clientes, on="cliente_id")
print(merge_inner.shape)  # 3 linhas (cliente_id 5 não bate)
```

**3.**
```python
merge_left = pd.merge(pedidos, clientes, on="cliente_id", how="left")
print(merge_left)
```

**4.**
```python
print(merge_left[merge_left["nome"].isnull()])
```

**5.**
```python
merge_right = pd.merge(pedidos, clientes, on="cliente_id", how="right")
print(merge_right)
```

**6.**
```python
merge_outer = pd.merge(pedidos, clientes, on="cliente_id", how="outer")
print(merge_outer.shape)
```

**7.**
```python
merge_left["pedido_valido"] = merge_left["nome"].notnull()
print(merge_left)
```

**8.**
```python
novo_cliente = pd.DataFrame({
    "cliente_id": [4],
    "nome": ["Ana"],
    "cidade": ["Salvador"],
})
clientes_atualizados = pd.concat([clientes, novo_cliente], ignore_index=True)
print(clientes_atualizados.shape)  # (4, 3)
```

**9.**
```python
merge_explicito = pd.merge(pedidos, clientes, left_on="cliente_id", right_on="cliente_id")
print(merge_explicito)
```

**10.**
```python
por_cidade = merge_inner.groupby("cidade")["valor"].sum()
print(por_cidade)
```

</details>

## 11. Introdução a valores ausentes

Use este DataFrame para os exercícios:

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "cliente": ["Marcos", "Julia", "Pedro", "Ana", "Carlos"],
    "email": ["marcos@x.com", None, "pedro@x.com", "ana@x.com", None],
    "telefone": [None, "11999990000", "11988880000", None, "11977770000"],
    "idade": [34, 28, np.nan, 41, 22],
    "cidade": ["São Paulo", "Rio de Janeiro", None, "Belo Horizonte", "Salvador"],
})
```

1. Conte quantos valores ausentes existem em cada coluna com
   `.isnull().sum()`.
2. Calcule a porcentagem de valores ausentes de cada coluna.
3. Filtre e imprima os clientes sem `email` cadastrado.
4. Filtre e imprima os clientes com `telefone` preenchido, usando
   `.notnull()`.
5. Filtre os clientes que não têm nem `email` nem `telefone` (combine duas
   condições de `.isnull()` com `&`).
6. Remova (sem alterar o `df` original) todas as linhas que têm qualquer
   valor ausente, usando `.dropna()`.
7. Remova só as linhas onde `cidade` está ausente, usando
   `dropna(subset=[...])`.
8. Preencha `email` ausente com `"não informado"` e `telefone` ausente com
   `"não informado"`, num DataFrame novo (use `.fillna()` com dicionário).
9. Preencha `idade` ausente com a média das idades existentes.
10. Combine os passos: crie uma cópia do `df` sem as linhas com `cidade`
    ausente, e nessa cópia preencha `email` ausente com `"não informado"`.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
print(df.isnull().sum())
```

**2.**
```python
print((df.isnull().sum() / len(df)) * 100)
```

**3.**
```python
print(df[df["email"].isnull()])
```

**4.**
```python
print(df[df["telefone"].notnull()])
```

**5.**
```python
print(df[df["email"].isnull() & df["telefone"].isnull()])
```

**6.**
```python
df_sem_nulos = df.dropna()
print(df_sem_nulos)
```

**7.**
```python
df_sem_cidade_ausente = df.dropna(subset=["cidade"])
print(df_sem_cidade_ausente)
```

**8.**
```python
df_preenchido = df.fillna({
    "email": "não informado",
    "telefone": "não informado",
})
print(df_preenchido)
```

**9.**
```python
df["idade"] = df["idade"].fillna(df["idade"].mean())
print(df["idade"])
```

**10.**
```python
df_copia = df.dropna(subset=["cidade"]).copy()
df_copia["email"] = df_copia["email"].fillna("não informado")
print(df_copia)
```

</details>

## 12. Tabelas dinâmicas (pivot_table)

Use este DataFrame para os exercícios:

```python
import pandas as pd

vendas = pd.DataFrame({
    "produto": ["Caneta", "Caneta", "Caderno", "Caderno", "Mochila", "Mochila", "Caneta"],
    "mes": ["Jan", "Fev", "Jan", "Fev", "Jan", "Fev", "Jan"],
    "quantidade": [10, 15, 5, 8, 2, 3, 4],
    "faturamento": [25.0, 37.5, 79.5, 127.2, 179.8, 269.7, 10.0],
})
```

1. Crie uma tabela dinâmica com `produto` nas linhas, `mes` nas colunas e
   `faturamento` somado (`aggfunc="sum"`) como valor.
2. Compare o resultado do item 1 com o `groupby(["produto", "mes"])
   ["faturamento"].sum()` equivalente.
3. Crie a mesma tabela do item 1, mas com `fill_value=0` para combinações
   sem dados.
4. Adicione `margins=True` e `margins_name="Total"` na tabela do item 1.
5. Crie uma tabela dinâmica com `produto` nas linhas, `mes` nas colunas e
   `quantidade` como valor, usando `aggfunc="mean"` (o padrão).
6. Crie uma tabela dinâmica com `values=["faturamento", "quantidade"]` de
   uma vez, `index="produto"`, `columns="mes"`, `aggfunc="sum"`.
7. Usando a tabela do item 1, identifique visualmente qual produto teve o
   maior faturamento total em fevereiro.
8. Transforme a tabela do item 1 de volta para o formato "comprido" usando
   `.reset_index()` seguido de `.melt()`.
9. Crie uma tabela dinâmica com `index="mes"` (ao invés de `produto`) e
   `columns="produto"`, valores de `quantidade`, `aggfunc="sum"`.
10. Crie uma tabela dinâmica com `produto` nas linhas, `mes` nas colunas,
    `faturamento` como valor, `aggfunc="count"` (contando quantas vendas
    existem em cada combinação produto/mês).

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
tabela = vendas.pivot_table(
    index="produto", columns="mes", values="faturamento", aggfunc="sum",
)
print(tabela)
```

**2.**
```python
equivalente = vendas.groupby(["produto", "mes"])["faturamento"].sum()
print(equivalente)
# mesmos números, só que em formato "comprido"
```

**3.**
```python
tabela_preenchida = vendas.pivot_table(
    index="produto", columns="mes", values="faturamento",
    aggfunc="sum", fill_value=0,
)
print(tabela_preenchida)
```

**4.**
```python
tabela_com_totais = vendas.pivot_table(
    index="produto", columns="mes", values="faturamento",
    aggfunc="sum", margins=True, margins_name="Total",
)
print(tabela_com_totais)
```

**5.**
```python
tabela_media = vendas.pivot_table(
    index="produto", columns="mes", values="quantidade", aggfunc="mean",
)
print(tabela_media)
```

**6.**
```python
tabela_multipla = vendas.pivot_table(
    index="produto", columns="mes",
    values=["faturamento", "quantidade"], aggfunc="sum",
)
print(tabela_multipla)
```

**7.**
```python
print(tabela)
# olhando a coluna "Fev": Caneta 37.5, Caderno 127.2, Mochila 269.7
# Mochila teve o maior faturamento em fevereiro
```

**8.**
```python
comprida = tabela.reset_index().melt(
    id_vars="produto", var_name="mes", value_name="faturamento",
)
print(comprida)
```

**9.**
```python
tabela_por_mes = vendas.pivot_table(
    index="mes", columns="produto", values="quantidade", aggfunc="sum",
)
print(tabela_por_mes)
```

**10.**
```python
tabela_contagem = vendas.pivot_table(
    index="produto", columns="mes", values="faturamento", aggfunc="count",
)
print(tabela_contagem)
```

</details>
