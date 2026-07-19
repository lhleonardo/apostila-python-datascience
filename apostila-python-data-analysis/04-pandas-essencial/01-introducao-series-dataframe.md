# Introdução ao Pandas: Series e DataFrame

> Módulo 4 — Pandas Essencial · Tópico 1 de 12

## O que é e por que importa

Pandas é a biblioteca de Python para trabalhar com dados em formato de
**tabela** — como uma planilha do Excel, mas manipulável por código, com
operações rápidas (graças ao NumPy por baixo) e prontas para as tarefas mais
comuns de análise de dados: filtrar, ordenar, agrupar, juntar tabelas,
calcular estatísticas.

Pandas tem duas estruturas de dados centrais:

- **Series**: uma coluna só, uma sequência de valores com um **índice**
  (rótulo) associado a cada um. Pense nela como um array NumPy 1D, mas onde
  cada posição tem um "nome" além do número da posição.
- **DataFrame**: uma tabela inteira — várias colunas (cada uma uma Series),
  todas compartilhando o mesmo índice de linhas. É a estrutura que você vai
  usar o tempo todo.

Instalação (se ainda não tiver):

```bash
pip install pandas
```

A convenção universal é importar com o apelido `pd`:

```python
import pandas as pd
```

## Como funciona (com exemplo comentado)

```python
import pandas as pd

# Series: uma coluna de dados com índice
precos = pd.Series([10.0, 25.5, 8.75, 42.0])
print(precos)
# 0    10.00
# 1    25.50
# 2     8.75
# 3    42.00
# dtype: float64
# -- a coluna à esquerda (0, 1, 2, 3) é o ÍNDICE, criado automaticamente

# Você pode dar nomes ao índice em vez de usar números
precos_nomeados = pd.Series(
    [10.0, 25.5, 8.75],
    index=["Caneta", "Caderno", "Lapis"],
)
print(precos_nomeados)
# Caneta     10.00
# Caderno    25.50
# Lapis       8.75
# dtype: float64

print(precos_nomeados["Caderno"])  # 25.5 -- acessa pelo rótulo do índice

# DataFrame: criado a partir de um dicionário, onde cada chave vira uma coluna
loja = pd.DataFrame({
    "produto": ["Caneta Azul", "Caderno", "Mochila", "Lapis HB"],
    "quantidade": [3, 1, 2, 5],
    "preco_unitario": [2.50, 15.90, 89.90, 1.20],
})

print(loja)
#        produto  quantidade  preco_unitario
# 0  Caneta Azul           3            2.50
# 1      Caderno           1           15.90
# 2      Mochila           2           89.90
# 3     Lapis HB           5            1.20

# Cada coluna de um DataFrame é uma Series
print(type(loja["produto"]))  # <class 'pandas.core.series.Series'>
print(loja["produto"])
# 0    Caneta Azul
# 1        Caderno
# 2        Mochila
# 3       Lapis HB
# Name: produto, dtype: object

# Atributos úteis, parecidos com os de arrays NumPy (Módulo 3)
print(loja.shape)   # (4, 3) -- 4 linhas, 3 colunas
print(loja.columns) # Index(['produto', 'quantidade', 'preco_unitario'], dtype='object')
print(loja.index)   # RangeIndex(start=0, stop=4, step=1)
print(loja.dtypes)  # tipo de cada coluna (object, int64, float64, ...)
```

Repare que o `dtype` de colunas de texto aparece como `object` — é como o
Pandas representa strings (por baixo, guarda referências a objetos Python,
diferente das colunas numéricas que usam arrays NumPy "puros" de
int64/float64).

## Erros comuns de quem está começando

- Confundir Series com DataFrame: `loja["produto"]` (uma coluna) é uma
  Series; `loja[["produto"]]` (colchete duplo, com uma lista dentro) é um
  DataFrame de uma coluna só. A diferença de colchetes simples/duplos
  aparece bastante em Pandas e vale prestar atenção.
- Achar que o índice de um DataFrame é sempre uma sequência de números
  0, 1, 2... — ele pode ser texto, datas, ou qualquer coisa, e algumas
  operações (como as que vêm nos próximos tópicos) dependem de entender qual
  é o índice atual.
- Esquecer o `import pandas as pd` ou usar um apelido fora do padrão — assim
  como `np` para NumPy, `pd` é universalmente esperado ao ler código Pandas.

## Exercício prático

1. Crie uma Series com os índices `["Segunda", "Terça", "Quarta", "Quinta",
   "Sexta"]` e valores `[1200, 850, 2100, 400, 1750]` representando o
   faturamento diário da Loja da Ana.
2. Acesse e imprima o valor de "Quarta" usando o rótulo do índice.
3. Crie um DataFrame com colunas `produto` (`["Caneta", "Caderno",
   "Mochila"]`), `preco` (`[2.5, 15.9, 89.9]`) e `estoque` (`[100, 40, 15]`).
4. Imprima o `shape` e os `dtypes` do DataFrame criado.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

faturamento = pd.Series(
    [1200, 850, 2100, 400, 1750],
    index=["Segunda", "Terça", "Quarta", "Quinta", "Sexta"],
)
print(faturamento["Quarta"])  # 2100

produtos = pd.DataFrame({
    "produto": ["Caneta", "Caderno", "Mochila"],
    "preco": [2.5, 15.9, 89.9],
    "estoque": [100, 40, 15],
})
print(produtos.shape)   # (3, 3)
print(produtos.dtypes)
```

</details>

## Checklist antes de avançar

- [ ] Sei a diferença entre Series (uma coluna) e DataFrame (uma tabela)
- [ ] Sei criar um DataFrame a partir de um dicionário
- [ ] Entendo o que é o índice e sei acessar valores por ele
- [ ] Resolvi o exercício sem olhar a solução
