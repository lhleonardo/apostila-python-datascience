# Lista de exercícios — Módulo 5

> Módulo 5 — Limpeza de Dados · Lista de exercícios de revisão

Esta lista reúne 10 exercícios práticos para cada tópico do módulo, para
consolidar o que foi aprendido antes de avançar. Tente resolver cada
exercício sem consultar o tópico original primeiro — as soluções vêm logo
depois de cada bloco, dentro de um "clique para ver".

## 1. Estratégias para valores ausentes

1. Dado o DataFrame abaixo, calcule a porcentagem de valores ausentes em
   cada coluna.

   ```python
   df = pd.DataFrame({
       "produto": ["Mouse", "Teclado", "Monitor", "Cabo", "Headset"],
       "preco": [45.0, np.nan, 890.0, 12.0, np.nan],
       "marca": ["Logitech", "Dell", None, "Generico", "JBL"],
   })
   ```

2. No `df` do item 1, remova a coluna caso ela tenha mais de 50% de valores
   ausentes (verifique programaticamente, não "no olho").

3. Dado

   ```python
   df = pd.DataFrame({
       "cliente": ["A", "B", "C", "D"],
       "idade": [25, np.nan, 40, np.nan],
   })
   ```

   preencha `idade` com a mediana da coluna.

4. Dado

   ```python
   df = pd.DataFrame({
       "produto": ["Caneta", "Caderno", "Mochila"],
       "categoria": ["Papelaria", None, "Acessorios"],
   })
   ```

   preencha `categoria` ausente com o texto `"Não informado"`.

5. Dado

   ```python
   df = pd.DataFrame({
       "regiao": ["Norte", "Norte", "Sul", "Sul", "Sul"],
       "vendas": [100.0, np.nan, 300.0, 320.0, np.nan],
   })
   ```

   preencha `vendas` usando a média **por região** (`groupby` + `transform`).

6. Dado

   ```python
   serie = pd.Series([100, 105, np.nan, np.nan, 120])
   ```

   preencha os valores ausentes por interpolação linear.

7. Dado

   ```python
   df = pd.DataFrame({
       "loja": ["A", "A", "B", "C"],
       "categoria": ["Eletronicos", "Eletronicos", "Roupas", None],
       "estoque": [10, np.nan, 5, 8],
   })
   ```

   remova as linhas em que `estoque` está ausente, mas preencha
   `categoria` ausente com a moda da coluna. Aplique nessa ordem e explique
   (em um comentário) por que a ordem escolhida importa aqui.

8. Dado

   ```python
   df = pd.DataFrame({
       "filial": ["Centro", "Centro", "Norte", "Norte", "Sul"],
       "faturamento": [12000.0, np.nan, 8000.0, 8500.0, np.nan],
   })
   ```

   preencha `faturamento` por grupo (`filial`) e identifique, ao final,
   quais linhas continuam com `NaN` porque o grupo inteiro não tinha
   nenhum valor válido para calcular a média. Trate esse caso residual
   preenchendo com a média geral da coluna.

9. Dado

   ```python
   df = pd.DataFrame({
       "produto": ["A", "B", "C", "D", "E"],
       "preco": [10.0, 0.0, np.nan, 15.0, 0.0],
   })
   ```

   decida (com base no que foi discutido sobre `0` não ser sempre
   "neutro") se os valores `0.0` deveriam ser tratados como ausentes.
   Substitua os `0.0` por `NaN` e, em seguida, preencha todos os ausentes
   com a mediana calculada sobre os valores originalmente válidos
   (diferentes de `0` e não nulos).

10. Dado

    ```python
    df = pd.DataFrame({
        "cliente": ["Marcos", "Julia", "Pedro", "Ana", "Carlos", "Bia"],
        "cidade": ["SP", "SP", "RJ", "RJ", "MG", None],
        "renda": [3500.0, np.nan, 4200.0, np.nan, 2800.0, 3100.0],
    })
    ```

    monte uma estratégia completa: preencha `renda` por grupo (`cidade`),
    depois preencha qualquer `renda` residual com a mediana geral, e
    preencha `cidade` ausente com `"Não informado"`. Confirme ao final que
    não sobrou nenhum valor ausente.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "produto": ["Mouse", "Teclado", "Monitor", "Cabo", "Headset"],
    "preco": [45.0, np.nan, 890.0, 12.0, np.nan],
    "marca": ["Logitech", "Dell", None, "Generico", "JBL"],
})

print((df.isnull().sum() / len(df) * 100).round(1))
```

**2.**
```python
percentual_ausente = df.isnull().sum() / len(df) * 100
colunas_para_remover = percentual_ausente[percentual_ausente > 50].index
df = df.drop(columns=colunas_para_remover)
print(df)
```

**3.**
```python
df = pd.DataFrame({
    "cliente": ["A", "B", "C", "D"],
    "idade": [25, np.nan, 40, np.nan],
})
df["idade"] = df["idade"].fillna(df["idade"].median())
print(df)
```

**4.**
```python
df = pd.DataFrame({
    "produto": ["Caneta", "Caderno", "Mochila"],
    "categoria": ["Papelaria", None, "Acessorios"],
})
df["categoria"] = df["categoria"].fillna("Não informado")
print(df)
```

**5.**
```python
df = pd.DataFrame({
    "regiao": ["Norte", "Norte", "Sul", "Sul", "Sul"],
    "vendas": [100.0, np.nan, 300.0, 320.0, np.nan],
})
df["vendas"] = df.groupby("regiao")["vendas"].transform(lambda s: s.fillna(s.mean()))
print(df)
```

**6.**
```python
serie = pd.Series([100, 105, np.nan, np.nan, 120])
print(serie.interpolate())
```

**7.**
```python
df = pd.DataFrame({
    "loja": ["A", "A", "B", "C"],
    "categoria": ["Eletronicos", "Eletronicos", "Roupas", None],
    "estoque": [10, np.nan, 5, 8],
})
# preenche categoria antes de remover linhas por estoque ausente, para não
# perder a chance de calcular a moda usando a linha que será removida
df["categoria"] = df["categoria"].fillna(df["categoria"].mode()[0])
df = df.dropna(subset=["estoque"])
print(df)
```

**8.**
```python
df = pd.DataFrame({
    "filial": ["Centro", "Centro", "Norte", "Norte", "Sul"],
    "faturamento": [12000.0, np.nan, 8000.0, 8500.0, np.nan],
})
media_geral = df["faturamento"].mean()
df["faturamento"] = df.groupby("filial")["faturamento"].transform(lambda s: s.fillna(s.mean()))
print(df[df["faturamento"].isnull()])  # linha da filial "Sul" (grupo sem nenhum valor válido)
df["faturamento"] = df["faturamento"].fillna(media_geral)
print(df)
```

**9.**
```python
df = pd.DataFrame({
    "produto": ["A", "B", "C", "D", "E"],
    "preco": [10.0, 0.0, np.nan, 15.0, 0.0],
})
mediana_valida = df.loc[(df["preco"] != 0) & (df["preco"].notnull()), "preco"].median()
df["preco"] = df["preco"].replace(0.0, np.nan)
df["preco"] = df["preco"].fillna(mediana_valida)
print(df)
```

**10.**
```python
df = pd.DataFrame({
    "cliente": ["Marcos", "Julia", "Pedro", "Ana", "Carlos", "Bia"],
    "cidade": ["SP", "SP", "RJ", "RJ", "MG", None],
    "renda": [3500.0, np.nan, 4200.0, np.nan, 2800.0, 3100.0],
})
mediana_geral = df["renda"].median()
df["renda"] = df.groupby("cidade")["renda"].transform(lambda s: s.fillna(s.mean()))
df["renda"] = df["renda"].fillna(mediana_geral)
df["cidade"] = df["cidade"].fillna("Não informado")
print(df.isnull().sum().sum())  # 0
print(df)
```

</details>

## 2. Duplicatas

1. Dado

   ```python
   df = pd.DataFrame({
       "pedido_id": [1, 2, 3, 3, 4],
       "valor": [50.0, 30.0, 20.0, 20.0, 90.0],
   })
   ```

   descubra quantas linhas são duplicatas exatas.

2. No `df` do item 1, remova as duplicatas exatas mantendo a primeira
   ocorrência.

3. Dado

   ```python
   df = pd.DataFrame({
       "cliente_id": [10, 11, 10, 12],
       "email": ["a@x.com", "b@x.com", "a@x.com", "c@x.com"],
   })
   ```

   remova as duplicatas mantendo a **última** ocorrência.

4. Dado

   ```python
   df = pd.DataFrame({
       "produto_id": [1, 2, 1, 3],
       "preco": [10.0, 20.0, 15.0, 30.0],
   })
   ```

   identifique quais linhas têm `produto_id` repetido, usando
   `subset=["produto_id"]`.

5. No `df` do item 4, remova todas as linhas envolvidas em duplicação por
   `produto_id` (nenhuma cópia deve sobrar), usando `keep=False`.

6. Dado

   ```python
   df = pd.DataFrame({
       "nota_fiscal": [100, 101, 100, 102, 101],
       "valor": [500.0, 300.0, 500.0, 700.0, 300.0],
       "vendedor": ["Ana", "Bia", "Ana", "Caio", "Bia"],
   })
   ```

   calcule o faturamento total somando `valor` (a) sem remover duplicatas e
   (b) depois de remover duplicatas exatas. Compare os dois resultados.

7. Dado

   ```python
   df = pd.DataFrame({
       "cliente_id": [1, 2, 1, 3],
       "cadastro": ["2024-01-10", "2024-02-01", "2024-01-05", "2024-03-01"],
   })
   ```

   remova duplicatas por `cliente_id`, mantendo a linha com a data de
   `cadastro` mais **antiga** (ordene antes de usar `drop_duplicates`).

8. Dado

   ```python
   df = pd.DataFrame({
       "pedido_id": [1, 2, 3, 4],
       "produto": ["Caneta", "Caneta ", "caneta", "Lapis"],
       "valor": [2.5, 2.5, 2.5, 1.2],
   })
   ```

   explique (com um comentário no código) por que `df.duplicated()` não
   detecta as linhas 0, 1 e 2 como duplicadas mesmo representando o mesmo
   produto, e mostre o resultado de `df.duplicated()` para comprovar.

9. Dado

   ```python
   df = pd.DataFrame({
       "pedido_id": [5, 6, 7, 6, 8, 5],
       "cliente": ["Rui", "Sara", "Tais", "Sara", "Ugo", "Rui"],
       "valor": [100.0, 200.0, 300.0, 200.0, 400.0, 100.0],
   })
   ```

   remova duplicatas por `pedido_id`, depois reindexe o DataFrame resultante
   (`reset_index(drop=True)`) e confirme que o índice ficou sequencial de 0
   a N-1.

10. Dado

    ```python
    df = pd.DataFrame({
        "transacao_id": [1, 2, 3, 4, 5, 3],
        "conta": ["C1", "C1", "C2", "C2", "C3", "C2"],
        "valor": [1000.0, 1000.0, 500.0, 500.0, 200.0, 500.0],
    })
    ```

    identifique separadamente (a) quantas linhas são duplicatas 100%
    idênticas e (b) quantos `transacao_id` aparecem mais de uma vez. Depois
    remova apenas as duplicatas 100% idênticas e explique, em um
    comentário, se isso já resolve o problema de negócio (transações
    repetidas) ou não.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd

df = pd.DataFrame({
    "pedido_id": [1, 2, 3, 3, 4],
    "valor": [50.0, 30.0, 20.0, 20.0, 90.0],
})
print(df.duplicated().sum())  # 1
```

**2.**
```python
df_limpo = df.drop_duplicates(keep="first").reset_index(drop=True)
print(df_limpo)
```

**3.**
```python
df = pd.DataFrame({
    "cliente_id": [10, 11, 10, 12],
    "email": ["a@x.com", "b@x.com", "a@x.com", "c@x.com"],
})
df_limpo = df.drop_duplicates(keep="last").reset_index(drop=True)
print(df_limpo)
```

**4.**
```python
df = pd.DataFrame({
    "produto_id": [1, 2, 1, 3],
    "preco": [10.0, 20.0, 15.0, 30.0],
})
print(df[df.duplicated(subset=["produto_id"], keep=False)])
```

**5.**
```python
df_limpo = df.drop_duplicates(subset=["produto_id"], keep=False)
print(df_limpo)
```

**6.**
```python
df = pd.DataFrame({
    "nota_fiscal": [100, 101, 100, 102, 101],
    "valor": [500.0, 300.0, 500.0, 700.0, 300.0],
    "vendedor": ["Ana", "Bia", "Ana", "Caio", "Bia"],
})
total_com_duplicatas = df["valor"].sum()
total_sem_duplicatas = df.drop_duplicates()["valor"].sum()
print(total_com_duplicatas, total_sem_duplicatas)  # 2300.0 vs 1500.0
```

**7.**
```python
df = pd.DataFrame({
    "cliente_id": [1, 2, 1, 3],
    "cadastro": ["2024-01-10", "2024-02-01", "2024-01-05", "2024-03-01"],
})
df_ordenado = df.sort_values("cadastro")
df_mais_antigo = df_ordenado.drop_duplicates(subset=["cliente_id"], keep="first")
print(df_mais_antigo.sort_values("cliente_id"))
```

**8.**
```python
df = pd.DataFrame({
    "pedido_id": [1, 2, 3, 4],
    "produto": ["Caneta", "Caneta ", "caneta", "Lapis"],
    "valor": [2.5, 2.5, 2.5, 1.2],
})
# duplicated() exige igualdade EXATA de texto -- espaço extra e diferença de
# capitalização fazem "Caneta", "Caneta " e "caneta" serem tratados como
# valores diferentes, mesmo representando o mesmo produto
print(df.duplicated())  # todas False
```

**9.**
```python
df = pd.DataFrame({
    "pedido_id": [5, 6, 7, 6, 8, 5],
    "cliente": ["Rui", "Sara", "Tais", "Sara", "Ugo", "Rui"],
    "valor": [100.0, 200.0, 300.0, 200.0, 400.0, 100.0],
})
df_limpo = df.drop_duplicates(subset=["pedido_id"]).reset_index(drop=True)
print(df_limpo)
print(list(df_limpo.index))  # [0, 1, 2, 3]
```

**10.**
```python
df = pd.DataFrame({
    "transacao_id": [1, 2, 3, 4, 5, 3],
    "conta": ["C1", "C1", "C2", "C2", "C3", "C2"],
    "valor": [1000.0, 1000.0, 500.0, 500.0, 200.0, 500.0],
})
duplicatas_exatas = df.duplicated().sum()
duplicatas_por_id = df.duplicated(subset=["transacao_id"]).sum()
print(duplicatas_exatas, duplicatas_por_id)  # 1, 1

df_limpo = df.drop_duplicates()
# neste caso resolve, porque a única transacao_id repetida (3) também é uma
# duplicata exata em todas as colunas -- mas isso não seria garantido em
# geral: se os valores diferissem entre as linhas com mesmo transacao_id,
# duplicatas de negócio ficariam sem ser detectadas por drop_duplicates() sem subset
print(df_limpo)
```

</details>

## 3. Tipos de dados e conversão

1. Dado

   ```python
   df = pd.DataFrame({
       "produto": ["Caneta", "Caderno"],
       "preco": ["R$ 3,00", "R$ 12,50"],
   })
   ```

   limpe e converta `preco` para `float`.

2. Dado

   ```python
   quantidades = pd.Series(["10", "20", "trinta", "40"])
   ```

   converta para número usando `pd.to_numeric` com `errors="coerce"` e
   conte quantos valores viraram `NaN`.

3. Dado

   ```python
   df = pd.DataFrame({
       "em_promocao": ["sim", "nao", "sim", "sim"],
   })
   ```

   converta `em_promocao` para `bool` usando `.map()`.

4. Dado

   ```python
   df = pd.DataFrame({
       "categoria": ["Livros", "Livros", "Eletronicos", "Livros", "Eletronicos"],
   })
   ```

   converta `categoria` para o tipo `category` e confirme o novo `dtype`.

5. Dado

   ```python
   df = pd.DataFrame({
       "avaliacao": [4.5, np.nan, 3.0, np.nan],
   })
   ```

   preencha os ausentes com `0` e converta a coluna para `int`, explicando
   em um comentário por que o `fillna` precisa vir antes do `astype(int)`.

6. Dado

   ```python
   df = pd.DataFrame({
       "codigo": ["A-001", "A-002", "A-003"],
       "peso_kg": ["1,5 kg", "2,0 kg", "0,750 kg"],
   })
   ```

   limpe `peso_kg` (remova `" kg"`, troque vírgula por ponto) e converta
   para `float`.

7. Dado

   ```python
   estoque = pd.Series(["120", "12O", "85", "9O"])
   ```

   (repare que alguns valores têm a letra "O" no lugar do número zero)
   converta para número com `errors="coerce"` e identifique quais posições
   viraram `NaN`.

8. Dado

   ```python
   df = pd.DataFrame({
       "ativo": ["1", "0", "1", "1", "0"],
   })
   ```

   converta `ativo` para `bool` usando `.astype(int).astype(bool)` e
   confirme o resultado.

9. Dado

   ```python
   df = pd.DataFrame({
       "produto": ["Mesa", "Cadeira", "Sofa"],
       "preco_texto": ["R$ 350,00", "R$ 120,50", "preço sob consulta"],
   })
   ```

   converta `preco_texto` para número usando `errors="coerce"` depois de
   limpar os símbolos (o valor `"preço sob consulta"` deve virar `NaN`).
   Em seguida, preencha o `NaN` resultante com a mediana dos preços
   válidos.

10. Dado

    ```python
    df = pd.DataFrame({
        "id": ["001", "002", "003"],
        "preco": ["R$ 10,00", "R$ 20,50", "invalido"],
        "quantidade": ["5", "N/A", "3"],
    })
    ```

    faça a limpeza completa: converta `preco` para `float` (com
    `errors="coerce"` depois de remover `"R$"` e trocar vírgula por
    ponto), converta `quantidade` para `Int64` (o tipo que aceita `NaN`,
    com I maiúsculo) usando `pd.to_numeric(..., errors="coerce")` seguido
    de `.astype("Int64")`, e informe quantos valores ficaram `NaN` em cada
    coluna ao final.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "produto": ["Caneta", "Caderno"],
    "preco": ["R$ 3,00", "R$ 12,50"],
})
df["preco"] = (
    df["preco"].str.replace("R$", "", regex=False)
    .str.replace(",", ".", regex=False)
    .str.strip()
    .astype(float)
)
print(df)
```

**2.**
```python
quantidades = pd.Series(["10", "20", "trinta", "40"])
convertido = pd.to_numeric(quantidades, errors="coerce")
print(convertido)
print(convertido.isnull().sum())  # 1
```

**3.**
```python
df = pd.DataFrame({
    "em_promocao": ["sim", "nao", "sim", "sim"],
})
df["em_promocao"] = df["em_promocao"].map({"sim": True, "nao": False})
print(df["em_promocao"].dtype)  # bool
```

**4.**
```python
df = pd.DataFrame({
    "categoria": ["Livros", "Livros", "Eletronicos", "Livros", "Eletronicos"],
})
df["categoria"] = df["categoria"].astype("category")
print(df["categoria"].dtype)  # category
```

**5.**
```python
df = pd.DataFrame({
    "avaliacao": [4.5, np.nan, 3.0, np.nan],
})
# int não aceita NaN -- é preciso resolver os ausentes com fillna antes de
# converter, senão astype(int) gera erro
df["avaliacao"] = df["avaliacao"].fillna(0).astype(int)
print(df)
```

**6.**
```python
df = pd.DataFrame({
    "codigo": ["A-001", "A-002", "A-003"],
    "peso_kg": ["1,5 kg", "2,0 kg", "0,750 kg"],
})
df["peso_kg"] = (
    df["peso_kg"].str.replace(" kg", "", regex=False)
    .str.replace(",", ".", regex=False)
    .astype(float)
)
print(df)
```

**7.**
```python
estoque = pd.Series(["120", "12O", "85", "9O"])
convertido = pd.to_numeric(estoque, errors="coerce")
print(convertido)
print(convertido[convertido.isnull()].index.tolist())  # [1, 3]
```

**8.**
```python
df = pd.DataFrame({
    "ativo": ["1", "0", "1", "1", "0"],
})
df["ativo"] = df["ativo"].astype(int).astype(bool)
print(df["ativo"])
```

**9.**
```python
df = pd.DataFrame({
    "produto": ["Mesa", "Cadeira", "Sofa"],
    "preco_texto": ["R$ 350,00", "R$ 120,50", "preço sob consulta"],
})
df["preco"] = (
    df["preco_texto"].str.replace("R$", "", regex=False)
    .str.replace(",", ".", regex=False)
    .str.strip()
)
df["preco"] = pd.to_numeric(df["preco"], errors="coerce")
mediana = df["preco"].median()
df["preco"] = df["preco"].fillna(mediana)
print(df)
```

**10.**
```python
df = pd.DataFrame({
    "id": ["001", "002", "003"],
    "preco": ["R$ 10,00", "R$ 20,50", "invalido"],
    "quantidade": ["5", "N/A", "3"],
})
df["preco"] = (
    df["preco"].str.replace("R$", "", regex=False)
    .str.replace(",", ".", regex=False)
    .str.strip()
)
df["preco"] = pd.to_numeric(df["preco"], errors="coerce")
df["quantidade"] = pd.to_numeric(df["quantidade"], errors="coerce").astype("Int64")

print(df.isnull().sum())
# preco: 1, quantidade: 1
```

</details>

## 4. Limpeza de texto

1. Dado

   ```python
   nomes = pd.Series([" Ana Paula", "ANA PAULA ", "ana paula"])
   ```

   padronize removendo espaços e convertendo para minúsculas, e confirme
   com `.unique()` que sobra só um valor.

2. Dado

   ```python
   cidades = pd.Series(["são paulo", "sao paulo", "SÃO PAULO"])
   ```

   remova acentos (use a função `remover_acentos` baseada em
   `unicodedata`, como no tópico) e padronize capitalização, confirmando
   que sobra um único valor único.

3. Dado

   ```python
   df = pd.DataFrame({
       "email": [" Marcos@Email.com", "julia@EMAIL.com ", "PEDRO@email.com"],
   })
   ```

   padronize `email` para minúsculas e sem espaços extras.

4. Dado

   ```python
   nomes = pd.Series(["Ana Souza", "Carlos Lima", "Beatriz Costa"])
   ```

   separe em duas colunas `primeiro_nome` e `sobrenome` usando
   `.str.split(" ", expand=True)`.

5. Dado

   ```python
   df = pd.DataFrame({
       "produto": ["caneta azul", "CADERNO GRANDE", "mochila escolar"],
   })
   ```

   crie uma coluna `produto_exibicao` com `.str.title()` para exibição
   (primeira letra de cada palavra maiúscula).

6. Dado

   ```python
   df = pd.DataFrame({
       "descricao": ["Produto com defeito", "Sem problemas", "Item com avaria"],
   })
   ```

   filtre as linhas cuja `descricao` contém a palavra `"defeito"` ou
   `"avaria"` usando `.str.contains()` com uma regex (`"defeito|avaria"`).

7. Dado

   ```python
   siglas = pd.Series(["SP", "RJ", "MG", "SP", "BA"])
   ```

   converta as siglas para nomes completos usando `.map()` com o
   dicionário `{"SP": "São Paulo", "RJ": "Rio de Janeiro", "MG": "Minas Gerais", "BA": "Bahia"}`.

8. Dado

   ```python
   df = pd.DataFrame({
       "categoria": [" Móveis", "moveis", "MÓVEIS ", "Decoração", "decoracao "],
   })
   ```

   padronize completamente `categoria` (espaços, capitalização e acentos)
   e confirme que sobram apenas 2 valores únicos.

9. Dado

   ```python
   df = pd.DataFrame({
       "telefone": ["(11) 98765-4321", "11987654321", "(11)98765-4321"],
   })
   ```

   remova todos os caracteres não numéricos de `telefone` usando
   `.str.replace(r"\D", "", regex=True)` e confirme que os três valores
   resultantes representam o mesmo número.

10. Dado

    ```python
    df = pd.DataFrame({
        "cliente": [" ana paula souza", "JOSÉ ROBERTO LIMA ", "márcia andrade"],
        "cidade": ["  São paulo", "RIO DE JANEIRO", "belo Horizonte "],
    })
    ```

    padronize as duas colunas de texto (remova espaços extras, acentos e
    deixe em formato título, ex: `"Ana Paula Souza"`), e separe `cliente`
    em `primeiro_nome` e `restante_do_nome` usando
    `.str.split(" ", n=1, expand=True)` após a padronização.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd
import unicodedata

nomes = pd.Series([" Ana Paula", "ANA PAULA ", "ana paula"])
nomes_padronizados = nomes.str.strip().str.lower()
print(nomes_padronizados.unique())  # ['ana paula']
```

**2.**
```python
def remover_acentos(texto):
    nfkd = unicodedata.normalize("NFKD", texto)
    return "".join(c for c in nfkd if not unicodedata.combining(c))

cidades = pd.Series(["são paulo", "sao paulo", "SÃO PAULO"])
cidades = cidades.str.strip().str.lower().apply(remover_acentos)
print(cidades.unique())  # ['sao paulo']
```

**3.**
```python
df = pd.DataFrame({
    "email": [" Marcos@Email.com", "julia@EMAIL.com ", "PEDRO@email.com"],
})
df["email"] = df["email"].str.strip().str.lower()
print(df)
```

**4.**
```python
nomes = pd.Series(["Ana Souza", "Carlos Lima", "Beatriz Costa"])
partes = nomes.str.split(" ", expand=True)
partes.columns = ["primeiro_nome", "sobrenome"]
print(partes)
```

**5.**
```python
df = pd.DataFrame({
    "produto": ["caneta azul", "CADERNO GRANDE", "mochila escolar"],
})
df["produto_exibicao"] = df["produto"].str.title()
print(df)
```

**6.**
```python
df = pd.DataFrame({
    "descricao": ["Produto com defeito", "Sem problemas", "Item com avaria"],
})
com_problema = df[df["descricao"].str.contains("defeito|avaria")]
print(com_problema)
```

**7.**
```python
siglas = pd.Series(["SP", "RJ", "MG", "SP", "BA"])
mapa = {"SP": "São Paulo", "RJ": "Rio de Janeiro", "MG": "Minas Gerais", "BA": "Bahia"}
print(siglas.map(mapa))
```

**8.**
```python
def remover_acentos(texto):
    nfkd = unicodedata.normalize("NFKD", texto)
    return "".join(c for c in nfkd if not unicodedata.combining(c))

df = pd.DataFrame({
    "categoria": [" Móveis", "moveis", "MÓVEIS ", "Decoração", "decoracao "],
})
df["categoria"] = df["categoria"].str.strip().str.lower().apply(remover_acentos)
print(df["categoria"].unique())  # ['moveis' 'decoracao']
```

**9.**
```python
df = pd.DataFrame({
    "telefone": ["(11) 98765-4321", "11987654321", "(11)98765-4321"],
})
df["telefone"] = df["telefone"].str.replace(r"\D", "", regex=True)
print(df["telefone"].unique())  # todos "11987654321"
```

**10.**
```python
def remover_acentos(texto):
    nfkd = unicodedata.normalize("NFKD", texto)
    return "".join(c for c in nfkd if not unicodedata.combining(c))

df = pd.DataFrame({
    "cliente": [" ana paula souza", "JOSÉ ROBERTO LIMA ", "márcia andrade"],
    "cidade": ["  São paulo", "RIO DE JANEIRO", "belo Horizonte "],
})

for coluna in ["cliente", "cidade"]:
    df[coluna] = (
        df[coluna].str.strip().str.lower().apply(remover_acentos).str.title()
    )

partes = df["cliente"].str.split(" ", n=1, expand=True)
partes.columns = ["primeiro_nome", "restante_do_nome"]
df = pd.concat([df, partes], axis=1)
print(df)
```

</details>

## 5. Trabalhando com datas

1. Dado

   ```python
   df = pd.DataFrame({
       "evento": ["Lançamento", "Fechamento", "Renovação"],
       "data_texto": ["01/03/2024", "15/03/2024", "30/03/2024"],
   })
   ```

   converta `data_texto` para `datetime`, especificando `format="%d/%m/%Y"`.

2. No `df` do item 1 (já convertido), crie colunas `ano`, `mes` e `dia`
   usando o acessor `.dt`.

3. Dado

   ```python
   df = pd.DataFrame({
       "pedido": [1, 2, 3],
       "data": pd.to_datetime(["10/01/2024", "20/02/2024", "05/03/2024"], format="%d/%m/%Y"),
   })
   ```

   filtre os pedidos com `data` a partir de `1º de fevereiro de 2024`
   (inclusive).

4. Dado

   ```python
   df = pd.DataFrame({
       "cliente": ["A", "B", "C"],
       "data_compra": pd.to_datetime(["01/01/2024", "15/02/2024", "10/03/2024"], format="%d/%m/%Y"),
   })
   ```

   calcule quantos dias se passaram desde cada `data_compra` até
   `pd.Timestamp("2024-04-01")`.

5. Dado

   ```python
   datas_texto = pd.Series(["10/05/2024", "não informado", "22/06/2024"])
   ```

   converta para `datetime` usando `errors="coerce"` e conte quantos
   valores viraram `NaT`.

6. Dado

   ```python
   df = pd.DataFrame({
       "venda_id": [1, 2, 3, 4],
       "data": pd.to_datetime(["05/01/2024", "12/01/2024", "03/02/2024", "20/02/2024"], format="%d/%m/%Y"),
       "valor": [100.0, 150.0, 200.0, 300.0],
   })
   ```

   agrupe as vendas por mês (`dt.to_period("M")`) e some `valor` em cada
   mês.

7. Dado

   ```python
   df = pd.DataFrame({
       "funcionario": ["Ana", "Bruno", "Carla"],
       "data_admissao": ["15/06/2020", "01/01/2022", "10/09/2018"],
   })
   ```

   converta `data_admissao` para `datetime` e crie uma coluna
   `dia_da_semana` com o nome do dia da semana em que cada um foi
   admitido (`.dt.day_name()`).

8. Dado

   ```python
   df = pd.DataFrame({
       "pedido": [1, 2, 3, 4],
       "data": ["01-03-2024", "15-03-2024", "data invalida", "30-03-2024"],
   })
   ```

   converta `data` para `datetime` com `format="%d-%m-%Y"` e
   `errors="coerce"`, depois remova as linhas em que a conversão falhou
   (usando o que foi visto no Tópico 1 sobre valores ausentes, já que
   `NaT` é tratado como ausente).

9. Dado

   ```python
   df = pd.DataFrame({
       "cliente": ["A", "B", "C", "D"],
       "data_cadastro": ["01/01/2023", "15/06/2023", "20/12/2023", "05/03/2024"],
   })
   ```

   converta `data_cadastro` para `datetime`, calcule os dias desde o
   cadastro até `pd.Timestamp("2024-07-01")`, e classifique cada cliente
   como `"antigo"` (mais de 300 dias) ou `"recente"` (300 dias ou menos)
   em uma nova coluna `perfil`.

10. Dado

    ```python
    df = pd.DataFrame({
        "pedido_id": [1, 2, 3, 4, 5],
        "data_pedido": ["10/01/2024", "12/01/2024", "invalido", "05/02/2024", "20/02/2024"],
        "valor": [100.0, 200.0, 150.0, 300.0, 250.0],
    })
    ```

    converta `data_pedido` com `errors="coerce"`, remova a linha com data
    inválida, crie a coluna `ano_mes` (`dt.to_period("M")`) e calcule o
    faturamento total por `ano_mes`, ordenado do mês mais antigo para o
    mais recente.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd

df = pd.DataFrame({
    "evento": ["Lançamento", "Fechamento", "Renovação"],
    "data_texto": ["01/03/2024", "15/03/2024", "30/03/2024"],
})
df["data"] = pd.to_datetime(df["data_texto"], format="%d/%m/%Y")
print(df)
```

**2.**
```python
df["ano"] = df["data"].dt.year
df["mes"] = df["data"].dt.month
df["dia"] = df["data"].dt.day
print(df)
```

**3.**
```python
df = pd.DataFrame({
    "pedido": [1, 2, 3],
    "data": pd.to_datetime(["10/01/2024", "20/02/2024", "05/03/2024"], format="%d/%m/%Y"),
})
inicio_fevereiro = pd.Timestamp("2024-02-01")
print(df[df["data"] >= inicio_fevereiro])
```

**4.**
```python
df = pd.DataFrame({
    "cliente": ["A", "B", "C"],
    "data_compra": pd.to_datetime(["01/01/2024", "15/02/2024", "10/03/2024"], format="%d/%m/%Y"),
})
referencia = pd.Timestamp("2024-04-01")
df["dias_desde_compra"] = (referencia - df["data_compra"]).dt.days
print(df)
```

**5.**
```python
datas_texto = pd.Series(["10/05/2024", "não informado", "22/06/2024"])
convertido = pd.to_datetime(datas_texto, format="%d/%m/%Y", errors="coerce")
print(convertido)
print(convertido.isnull().sum())  # 1
```

**6.**
```python
df = pd.DataFrame({
    "venda_id": [1, 2, 3, 4],
    "data": pd.to_datetime(["05/01/2024", "12/01/2024", "03/02/2024", "20/02/2024"], format="%d/%m/%Y"),
    "valor": [100.0, 150.0, 200.0, 300.0],
})
df["ano_mes"] = df["data"].dt.to_period("M")
print(df.groupby("ano_mes")["valor"].sum())
```

**7.**
```python
df = pd.DataFrame({
    "funcionario": ["Ana", "Bruno", "Carla"],
    "data_admissao": ["15/06/2020", "01/01/2022", "10/09/2018"],
})
df["data_admissao"] = pd.to_datetime(df["data_admissao"], format="%d/%m/%Y")
df["dia_da_semana"] = df["data_admissao"].dt.day_name()
print(df)
```

**8.**
```python
df = pd.DataFrame({
    "pedido": [1, 2, 3, 4],
    "data": ["01-03-2024", "15-03-2024", "data invalida", "30-03-2024"],
})
df["data"] = pd.to_datetime(df["data"], format="%d-%m-%Y", errors="coerce")
df = df.dropna(subset=["data"])
print(df)
```

**9.**
```python
df = pd.DataFrame({
    "cliente": ["A", "B", "C", "D"],
    "data_cadastro": ["01/01/2023", "15/06/2023", "20/12/2023", "05/03/2024"],
})
df["data_cadastro"] = pd.to_datetime(df["data_cadastro"], format="%d/%m/%Y")
referencia = pd.Timestamp("2024-07-01")
df["dias_cadastrado"] = (referencia - df["data_cadastro"]).dt.days
df["perfil"] = df["dias_cadastrado"].apply(lambda d: "antigo" if d > 300 else "recente")
print(df)
```

**10.**
```python
df = pd.DataFrame({
    "pedido_id": [1, 2, 3, 4, 5],
    "data_pedido": ["10/01/2024", "12/01/2024", "invalido", "05/02/2024", "20/02/2024"],
    "valor": [100.0, 200.0, 150.0, 300.0, 250.0],
})
df["data_pedido"] = pd.to_datetime(df["data_pedido"], format="%d/%m/%Y", errors="coerce")
df = df.dropna(subset=["data_pedido"])
df["ano_mes"] = df["data_pedido"].dt.to_period("M")
faturamento_por_mes = df.groupby("ano_mes")["valor"].sum().sort_index()
print(faturamento_por_mes)
```

</details>

## 6. Outliers: detecção e tratamento

1. Dado

   ```python
   salarios = pd.Series([3000, 3200, 3100, 3300, 25000])
   ```

   calcule Q1, Q3 e o IQR.

2. No `salarios` do item 1, calcule os limites inferior e superior pela
   regra 1.5×IQR e identifique quais valores são outliers.

3. Dado

   ```python
   df = pd.DataFrame({
       "produto": ["A", "B", "C", "D", "E"],
       "preco": [20.0, 22.0, 19.0, 21.0, 150.0],
   })
   ```

   calcule o z-score de cada preço e identifique quais linhas têm
   `|z-score| > 1.5`.

4. No `df` do item 3, crie uma coluna `preco_com_cap` usando `.clip()` com
   os limites do método IQR.

5. Dado

   ```python
   vendas = pd.Series([500, 520, 480, 510, -50])
   ```

   identifique o valor claramente impossível (negativo) usando um filtro
   direto (`vendas < 0`), sem precisar de IQR ou z-score.

6. Dado

   ```python
   df = pd.DataFrame({
       "item": ["A", "B", "C", "D", "E", "F"],
       "quantidade": [10, 12, 9, 11, 10, 500],
   })
   ```

   remova a linha identificada como outlier pelo método IQR e compare a
   média de `quantidade` antes e depois da remoção.

7. Dado

   ```python
   df = pd.DataFrame({
       "funcionario": ["A", "B", "C", "D", "E", "F", "G", "H"],
       "salario": [3500, 3800, 4000, 3600, 3900, 4100, 3700, 40000],
   })
   ```

   compare a média e a mediana de `salario` e explique, em um comentário,
   por que a mediana é mais representativa do "salário típico" neste
   caso.

8. Dado

   ```python
   df = pd.DataFrame({
       "cliente": ["A", "B", "C", "D", "E"],
       "gasto_mensal": [200.0, 250.0, 180.0, 5000.0, 220.0],
   })
   ```

   identifique o outlier usando z-score (`|z| > 1.5`) e decida (com um
   comentário justificando) se ele parece um erro de dados ou um cliente
   legítimo de alto gasto — depois aplique winsorização (`.clip()`) com os
   limites do IQR como tratamento conservador.

9. Dado

   ```python
   df = pd.DataFrame({
       "produto": ["A", "B", "C", "D", "E", "F", "G"],
       "preco": [15.0, 18.0, 16.0, 200.0, 17.0, 19.0, 2.0],
   })
   ```

   identifique **todos** os outliers (tanto para cima quanto para baixo)
   usando IQR, já que a coluna tem candidatos em ambas as direções.

10. Dado

    ```python
    df = pd.DataFrame({
        "loja": ["A", "B", "C", "D", "E", "F"],
        "faturamento_mensal": [12000.0, 13500.0, 11800.0, 12900.0, 12200.0, 95000.0],
    })
    ```

    aplique o método IQR para detectar outliers, o método z-score
    (`|z| > 2`) para o mesmo dado, e compare se os dois métodos concordam
    sobre quais linhas são outliers. Em seguida aplique `.clip()` com os
    limites do IQR e mostre o resultado final.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd

salarios = pd.Series([3000, 3200, 3100, 3300, 25000])
q1 = salarios.quantile(0.25)
q3 = salarios.quantile(0.75)
iqr = q3 - q1
print(f"Q1={q1}, Q3={q3}, IQR={iqr}")
```

**2.**
```python
limite_inferior = q1 - 1.5 * iqr
limite_superior = q3 + 1.5 * iqr
outliers = salarios[(salarios < limite_inferior) | (salarios > limite_superior)]
print(outliers)  # 25000
```

**3.**
```python
df = pd.DataFrame({
    "produto": ["A", "B", "C", "D", "E"],
    "preco": [20.0, 22.0, 19.0, 21.0, 150.0],
})
media = df["preco"].mean()
desvio = df["preco"].std()
df["z_score"] = (df["preco"] - media) / desvio
print(df[df["z_score"].abs() > 1.5])
```

**4.**
```python
q1 = df["preco"].quantile(0.25)
q3 = df["preco"].quantile(0.75)
iqr = q3 - q1
limite_inferior = q1 - 1.5 * iqr
limite_superior = q3 + 1.5 * iqr
df["preco_com_cap"] = df["preco"].clip(lower=limite_inferior, upper=limite_superior)
print(df)
```

**5.**
```python
vendas = pd.Series([500, 520, 480, 510, -50])
print(vendas[vendas < 0])  # -50
```

**6.**
```python
df = pd.DataFrame({
    "item": ["A", "B", "C", "D", "E", "F"],
    "quantidade": [10, 12, 9, 11, 10, 500],
})
q1 = df["quantidade"].quantile(0.25)
q3 = df["quantidade"].quantile(0.75)
iqr = q3 - q1
limite_superior = q3 + 1.5 * iqr
limite_inferior = q1 - 1.5 * iqr

media_antes = df["quantidade"].mean()
df_sem_outlier = df[(df["quantidade"] >= limite_inferior) & (df["quantidade"] <= limite_superior)]
media_depois = df_sem_outlier["quantidade"].mean()
print(media_antes, media_depois)
```

**7.**
```python
df = pd.DataFrame({
    "funcionario": ["A", "B", "C", "D", "E", "F", "G", "H"],
    "salario": [3500, 3800, 4000, 3600, 3900, 4100, 3700, 40000],
})
print("Média:", df["salario"].mean())      # puxada para cima pelo outlier
print("Mediana:", df["salario"].median())  # próxima do salário típico do grupo
# a mediana não é afetada pela magnitude do valor extremo, só pela posição
# dele na ordenação -- por isso representa melhor o "salário típico" aqui
```

**8.**
```python
df = pd.DataFrame({
    "cliente": ["A", "B", "C", "D", "E"],
    "gasto_mensal": [200.0, 250.0, 180.0, 5000.0, 220.0],
})
media = df["gasto_mensal"].mean()
desvio = df["gasto_mensal"].std()
df["z_score"] = (df["gasto_mensal"] - media) / desvio
print(df[df["z_score"].abs() > 1.5])  # cliente D
# sem mais contexto de negócio não dá para afirmar com certeza, mas um
# gasto 20x maior que os demais é um forte candidato a erro de digitação
# (ex: um zero a mais); por segurança, tratamos com clip em vez de remover

q1 = df["gasto_mensal"].quantile(0.25)
q3 = df["gasto_mensal"].quantile(0.75)
iqr = q3 - q1
limite_inferior = q1 - 1.5 * iqr
limite_superior = q3 + 1.5 * iqr
df["gasto_com_cap"] = df["gasto_mensal"].clip(lower=limite_inferior, upper=limite_superior)
print(df)
```

**9.**
```python
df = pd.DataFrame({
    "produto": ["A", "B", "C", "D", "E", "F", "G"],
    "preco": [15.0, 18.0, 16.0, 200.0, 17.0, 19.0, 2.0],
})
q1 = df["preco"].quantile(0.25)
q3 = df["preco"].quantile(0.75)
iqr = q3 - q1
limite_inferior = q1 - 1.5 * iqr
limite_superior = q3 + 1.5 * iqr
outliers = df[(df["preco"] < limite_inferior) | (df["preco"] > limite_superior)]
print(outliers)  # produtos D (200.0) e G (2.0)
```

**10.**
```python
df = pd.DataFrame({
    "loja": ["A", "B", "C", "D", "E", "F"],
    "faturamento_mensal": [12000.0, 13500.0, 11800.0, 12900.0, 12200.0, 95000.0],
})
q1 = df["faturamento_mensal"].quantile(0.25)
q3 = df["faturamento_mensal"].quantile(0.75)
iqr = q3 - q1
limite_inferior = q1 - 1.5 * iqr
limite_superior = q3 + 1.5 * iqr
outliers_iqr = df[(df["faturamento_mensal"] < limite_inferior) | (df["faturamento_mensal"] > limite_superior)]

media = df["faturamento_mensal"].mean()
desvio = df["faturamento_mensal"].std()
df["z_score"] = (df["faturamento_mensal"] - media) / desvio
outliers_zscore = df[df["z_score"].abs() > 2]

print(outliers_iqr[["loja", "faturamento_mensal"]])
print(outliers_zscore[["loja", "faturamento_mensal"]])
# neste caso os dois métodos concordam: a loja F é identificada como outlier em ambos

df["faturamento_com_cap"] = df["faturamento_mensal"].clip(lower=limite_inferior, upper=limite_superior)
print(df)
```

</details>

## 7. Checklist de qualidade de dados

Os exercícios deste tópico exigem aplicar várias técnicas do módulo em
sequência (ausentes, duplicatas, tipos, texto, datas e outliers) sobre
datasets com múltiplos problemas ao mesmo tempo — assim como no roteiro de
diagnóstico completo apresentado no tópico.

1. Dado

   ```python
   df = pd.DataFrame({
       "cliente": ["Ana", "Bruno", "Ana", "Carla"],
       "cidade": [" Sao Paulo", "rio de janeiro ", " Sao Paulo", "MG"],
       "compra": [150.0, np.nan, 150.0, 300.0],
   })
   ```

   rode o diagnóstico completo (`.info()`, `.isnull().sum()`,
   `.duplicated().sum()`, `.unique()` de `cidade`) e liste, em comentários,
   todos os problemas encontrados antes de corrigir qualquer coisa.

2. No `df` do item 1, remova as duplicatas exatas e depois padronize
   `cidade` (espaços e minúsculas).

3. Dado

   ```python
   df = pd.DataFrame({
       "produto": ["Caneta", "Caderno", "Mochila", "Lapis"],
       "preco": ["R$ 2,50", "R$ 15,90", "R$ 89,90", "R$ 1,20"],
       "estoque": [50, np.nan, 12, 300],
   })
   ```

   converta `preco` para `float` e depois preencha `estoque` ausente com a
   mediana (aplicando primeiro a conversão de tipo, já que ela não depende
   do valor ausente em `estoque`, e não altera a mediana calculada
   depois).

4. Dado

   ```python
   csv_texto = """cliente,cidade,valor,data
   Marcos,SP,R$ 100,00,01/02/2024
   Julia, sp ,R$ 250,00,05/02/2024
   Marcos,SP,R$ 100,00,01/02/2024
   Pedro,RJ,R$ -30,00,10/02/2024
   """
   df = pd.read_csv(StringIO(csv_texto))
   ```

   aplique o roteiro: remova duplicatas, padronize `cidade`, remova a
   linha com `valor` negativo e converta `data` para `datetime`.

5. Dado

   ```python
   df = pd.DataFrame({
       "pedido_id": [1, 2, 3, 4, 5],
       "quantidade": [3, 2, 1, 4, 999],
       "categoria": ["Roupas", "roupas ", "Calcados", "CALCADOS", "Roupas"],
   })
   ```

   padronize `categoria` e trate o outlier em `quantidade` (999 é
   claramente erro de digitação) com a estratégia que achar mais
   adequada, justificando em um comentário.

6. Dado

   ```python
   csv_texto = """produto,preco,categoria,data_venda
   Mouse,R$ 45,00, eletronicos ,12/01/2024
   Teclado,R$ 120,00,Eletronicos,15/01/2024
   Mouse,R$ 45,00, eletronicos ,12/01/2024
   Monitor,R$ 890,00,ELETRONICOS,,
   """
   df = pd.read_csv(StringIO(csv_texto))
   ```

   rode o diagnóstico completo, depois: remova duplicatas, converta
   `preco` para `float`, padronize `categoria`, e converta `data_venda`
   para `datetime` com `errors="coerce"` (a última linha não tem data).

7. Dado

   ```python
   df = pd.DataFrame({
       "funcionario": ["A", "B", "C", "D", "E", "F"],
       "salario": ["3500", "3800", "N/A", "4000", "3700", "150000"],
       "cidade": ["SP", "sp", "RJ", "RJ", " sp", "MG"],
   })
   ```

   converta `salario` para número (`errors="coerce"`), preencha o `NaN`
   resultante com a mediana calculada **sem considerar** o outlier
   150000, padronize `cidade`, e por fim trate o outlier de `salario`
   com `.clip()` usando os limites do IQR calculados também sem o valor
   ausente original.

8. Dado

   ```python
   csv_texto = """pedido_id,cliente,valor,status
   1,Marcos,R$ 200,00,Entregue
   2,Julia,R$ 150,00, entregue
   2,Julia,R$ 150,00, entregue
   3,Pedro,R$ -10,00,Cancelado
   4,Ana,R$ 99999,00,Entregue
   """
   df = pd.read_csv(StringIO(csv_texto))
   ```

   aplique o roteiro completo: diagnóstico, remoção de duplicatas,
   conversão de `valor` para `float`, padronização de `status`, remoção
   de valores negativos, e detecção (sem necessariamente remover) do
   outlier em `valor` usando IQR — comente se ele parece erro de dados ou
   uma compra grande legítima.

9. Dado

   ```python
   csv_texto = """cliente_id,nome,cidade,data_cadastro,gasto_total
   1,Ana Silva, sao paulo,10/01/2023,1200,00
   2,Bruno Costa,SAO PAULO,15/03/2023,890,50
   1,Ana Silva, sao paulo,10/01/2023,1200,00
   3,Carla Dias,rio de janeiro,20/06/2023,45000,00
   4,Diego Alves,belo horizonte,,780,00
   """
   df = pd.read_csv(StringIO(csv_texto))
   ```

   monte o roteiro completo: remova duplicatas, padronize `cidade`
   (espaços, acentos, minúsculas), converta `gasto_total` para `float`
   (repare que a vírgula decimal do CSV separa em duas colunas — trate
   isso reconstituindo o valor correto a partir das colunas geradas antes
   de seguir), converta `data_cadastro` com `errors="coerce"`, e trate o
   outlier em `gasto_total` com a estratégia que achar mais adequada.

10. Dado

    ```python
    csv_texto = """venda_id,vendedor,cidade,valor,data,categoria
    1,Rui,  Sao Paulo,R$ 500,00,10/04/2024,Eletronicos
    2,Sara,rio de janeiro,R$ 320,00,12/04/2024, eletronicos
    1,Rui,  Sao Paulo,R$ 500,00,10/04/2024,Eletronicos
    3,Tais,SAO PAULO,R$ -50,00,15/04/2024,Roupas
    4,Ugo,Belo Horizonte,R$ 8000,00,invalido,roupas
    5,Vera,rio de janeiro,R$ 410,00,20/04/2024,ELETRONICOS
    """
    df = pd.read_csv(StringIO(csv_texto))
    ```

    aplique o roteiro de diagnóstico e limpeza completo, na ordem que
    fizer sentido dado as dependências entre os problemas: (a) diagnóstico
    inicial completo, (b) remoção de duplicatas exatas, (c) conversão de
    `valor` para `float`, (d) remoção de valores negativos, (e)
    padronização de `cidade` e `categoria`, (f) conversão de `data` com
    `errors="coerce"` e tratamento das linhas resultantes com `NaT`
    (decida remover), (g) detecção de outlier em `valor` com IQR, e (h)
    validação final confirmando que não sobrou nenhum problema.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "cliente": ["Ana", "Bruno", "Ana", "Carla"],
    "cidade": [" Sao Paulo", "rio de janeiro ", " Sao Paulo", "MG"],
    "compra": [150.0, np.nan, 150.0, 300.0],
})
df.info()
print(df.isnull().sum())      # compra: 1 ausente
print(df.duplicated().sum())  # 1 duplicata exata (linha da Ana repetida)
print(df["cidade"].unique())  # espaços extras e "MG" fora do padrão de nome completo
```

**2.**
```python
df = df.drop_duplicates().reset_index(drop=True)
df["cidade"] = df["cidade"].str.strip().str.lower()
print(df)
```

**3.**
```python
df = pd.DataFrame({
    "produto": ["Caneta", "Caderno", "Mochila", "Lapis"],
    "preco": ["R$ 2,50", "R$ 15,90", "R$ 89,90", "R$ 1,20"],
    "estoque": [50, np.nan, 12, 300],
})
df["preco"] = (
    df["preco"].str.replace("R$", "", regex=False)
    .str.replace(",", ".", regex=False)
    .str.strip()
    .astype(float)
)
df["estoque"] = df["estoque"].fillna(df["estoque"].median())
print(df)
```

**4.**
```python
from io import StringIO
import pandas as pd

csv_texto = """cliente,cidade,valor,data
Marcos,SP,100.00,01/02/2024
Julia, sp ,250.00,05/02/2024
Marcos,SP,100.00,01/02/2024
Pedro,RJ,-30.00,10/02/2024
"""
# nota: assim como no tópico, "R$" foi removido direto do texto de entrada
# para simplificar o parse do CSV neste exemplo
df = pd.read_csv(StringIO(csv_texto))

df = df.drop_duplicates().reset_index(drop=True)
df["cidade"] = df["cidade"].str.strip().str.lower()
df = df[df["valor"] >= 0]
df["data"] = pd.to_datetime(df["data"], format="%d/%m/%Y")
print(df)
```

**5.**
```python
df = pd.DataFrame({
    "pedido_id": [1, 2, 3, 4, 5],
    "quantidade": [3, 2, 1, 4, 999],
    "categoria": ["Roupas", "roupas ", "Calcados", "CALCADOS", "Roupas"],
})
df["categoria"] = df["categoria"].str.strip().str.lower()

q1 = df["quantidade"].quantile(0.25)
q3 = df["quantidade"].quantile(0.75)
iqr = q3 - q1
limite_superior = q3 + 1.5 * iqr
# 999 é claramente um erro de digitação (não um evento real de venda em
# massa), então removemos a linha em vez de aplicar clip
df = df[df["quantidade"] <= limite_superior]
print(df)
```

**6.**
```python
from io import StringIO
import pandas as pd

csv_texto = """produto,preco,categoria,data_venda
Mouse,45.00, eletronicos ,12/01/2024
Teclado,120.00,Eletronicos,15/01/2024
Mouse,45.00, eletronicos ,12/01/2024
Monitor,890.00,ELETRONICOS,
"""
df = pd.read_csv(StringIO(csv_texto))

df.info()
print(df.isnull().sum())
print(df.duplicated().sum())
print(df["categoria"].unique())

df = df.drop_duplicates().reset_index(drop=True)
df["preco"] = df["preco"].astype(float)
df["categoria"] = df["categoria"].str.strip().str.lower()
df["data_venda"] = pd.to_datetime(df["data_venda"], format="%d/%m/%Y", errors="coerce")
print(df)
```

**7.**
```python
df = pd.DataFrame({
    "funcionario": ["A", "B", "C", "D", "E", "F"],
    "salario": ["3500", "3800", "N/A", "4000", "3700", "150000"],
    "cidade": ["SP", "sp", "RJ", "RJ", " sp", "MG"],
})
df["salario"] = pd.to_numeric(df["salario"], errors="coerce")

salarios_sem_outlier = df.loc[df["funcionario"] != "F", "salario"].dropna()
mediana_sem_outlier = salarios_sem_outlier.median()
df["salario"] = df["salario"].fillna(mediana_sem_outlier)

df["cidade"] = df["cidade"].str.strip().str.lower()

q1 = salarios_sem_outlier.quantile(0.25)
q3 = salarios_sem_outlier.quantile(0.75)
iqr = q3 - q1
limite_inferior = q1 - 1.5 * iqr
limite_superior = q3 + 1.5 * iqr
df["salario"] = df["salario"].clip(lower=limite_inferior, upper=limite_superior)
print(df)
```

**8.**
```python
from io import StringIO
import pandas as pd

csv_texto = """pedido_id,cliente,valor,status
1,Marcos,200.00,Entregue
2,Julia,150.00, entregue
2,Julia,150.00, entregue
3,Pedro,-10.00,Cancelado
4,Ana,99999.00,Entregue
"""
df = pd.read_csv(StringIO(csv_texto))

df.info()
print(df.isnull().sum())
print(df.duplicated().sum())

df = df.drop_duplicates().reset_index(drop=True)
df["valor"] = df["valor"].astype(float)
df["status"] = df["status"].str.strip().str.lower()
df = df[df["valor"] >= 0]

q1 = df["valor"].quantile(0.25)
q3 = df["valor"].quantile(0.75)
iqr = q3 - q1
limite_superior = q3 + 1.5 * iqr
outliers = df[df["valor"] > limite_superior]
print(outliers)
# sem mais contexto de negócio, um pedido de quase 100 mil ao lado de
# pedidos de 150-200 chama atenção como possível erro de digitação, mas
# poderia também ser uma compra corporativa legítima -- vale investigar
# antes de decidir remover
```

**9.**
```python
from io import StringIO
import pandas as pd
import unicodedata

def remover_acentos(texto):
    nfkd = unicodedata.normalize("NFKD", texto)
    return "".join(c for c in nfkd if not unicodedata.combining(c))

csv_texto = """cliente_id,nome,cidade,data_cadastro,gasto_parte1,gasto_parte2
1,Ana Silva, sao paulo,10/01/2023,1200,00
2,Bruno Costa,SAO PAULO,15/03/2023,890,50
1,Ana Silva, sao paulo,10/01/2023,1200,00
3,Carla Dias,rio de janeiro,20/06/2023,45000,00
4,Diego Alves,belo horizonte,,780,00
"""
# nota: para simplificar o parse do CSV com vírgula decimal, o valor de
# gasto foi lido em duas colunas separadas (parte inteira e parte decimal),
# que são reconstituídas logo abaixo
df = pd.read_csv(StringIO(csv_texto))

df = df.drop_duplicates().reset_index(drop=True)

df["cidade"] = df["cidade"].str.strip().str.lower().apply(remover_acentos)

df["gasto_total"] = (
    df["gasto_parte1"].astype(str) + "." + df["gasto_parte2"].astype(str).str.zfill(2)
).astype(float)
df = df.drop(columns=["gasto_parte1", "gasto_parte2"])

df["data_cadastro"] = pd.to_datetime(df["data_cadastro"], format="%d/%m/%Y", errors="coerce")

q1 = df["gasto_total"].quantile(0.25)
q3 = df["gasto_total"].quantile(0.75)
iqr = q3 - q1
limite_superior = q3 + 1.5 * iqr
df["gasto_total"] = df["gasto_total"].clip(upper=limite_superior)
print(df)
```

**10.**
```python
from io import StringIO
import pandas as pd

csv_texto = """venda_id,vendedor,cidade,valor,data,categoria
1,Rui,  Sao Paulo,500.00,10/04/2024,Eletronicos
2,Sara,rio de janeiro,320.00,12/04/2024, eletronicos
1,Rui,  Sao Paulo,500.00,10/04/2024,Eletronicos
3,Tais,SAO PAULO,-50.00,15/04/2024,Roupas
4,Ugo,Belo Horizonte,8000.00,invalido,roupas
5,Vera,rio de janeiro,410.00,20/04/2024,ELETRONICOS
"""
df = pd.read_csv(StringIO(csv_texto))

# a) diagnóstico inicial
df.info()
print(df.isnull().sum())
print(df.duplicated().sum())
print(df["cidade"].unique())
print(df["categoria"].unique())

# b) duplicatas exatas
df = df.drop_duplicates().reset_index(drop=True)

# c) tipo de valor (já numérico neste CSV simplificado, mas garantindo o tipo)
df["valor"] = df["valor"].astype(float)

# d) valores negativos
df = df[df["valor"] >= 0]

# e) padronização de texto
df["cidade"] = df["cidade"].str.strip().str.lower()
df["categoria"] = df["categoria"].str.strip().str.lower()

# f) conversão de data, com remoção das linhas que não converteram
df["data"] = pd.to_datetime(df["data"], format="%d/%m/%Y", errors="coerce")
df = df.dropna(subset=["data"])

# g) outlier em valor
q1 = df["valor"].quantile(0.25)
q3 = df["valor"].quantile(0.75)
iqr = q3 - q1
limite_superior = q3 + 1.5 * iqr
print(df[df["valor"] > limite_superior])

# h) validação final
print(df.isnull().sum().sum())   # 0
print(df.duplicated().sum())     # 0
print(df.dtypes)
print(df["cidade"].unique())
print(df["categoria"].unique())
print(df)
```

</details>
