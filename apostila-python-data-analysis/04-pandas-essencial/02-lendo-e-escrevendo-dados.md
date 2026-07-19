# Lendo e escrevendo dados (CSV, Excel, JSON)

> Módulo 4 — Pandas Essencial · Tópico 2 de 12

## O que é e por que importa

Na prática, você quase nunca digita os dados na mão como no tópico anterior
— eles vêm de um arquivo (CSV exportado de um sistema, uma planilha Excel,
uma resposta de API em JSON) ou de um banco de dados. Pandas tem funções
`read_*` prontas para carregar os formatos mais comuns direto num DataFrame,
e `to_*` para salvar de volta.

Esse é o ponto em que a apostila passa a usar **datasets públicos reais**
além da Loja da Ana. Sempre que um exemplo depender de baixar um arquivo da
internet, ele também trará uma versão inline (uma string ou dicionário) como
backup, para o caso de você estar sem internet ou o link não funcionar mais.

## Como funciona (com exemplo comentado)

```python
import pandas as pd

# Lendo um CSV (o mais comum em análise de dados)
# df = pd.read_csv("vendas.csv")

# Exemplo prático: sem depender de um arquivo real, simulamos um CSV com StringIO
from io import StringIO

csv_texto = """produto,quantidade,preco_unitario
Caneta Azul,3,2.50
Caderno,1,15.90
Mochila,2,89.90
Lapis HB,5,1.20
"""

df = pd.read_csv(StringIO(csv_texto))
print(df)
#        produto  quantidade  preco_unitario
# 0  Caneta Azul           3            2.50
# 1      Caderno           1           15.90
# 2      Mochila           2           89.90
# 3     Lapis HB           5            1.20

# Parâmetros comuns do read_csv:
# pd.read_csv("arquivo.csv", sep=";")          -- separador diferente de vírgula
# pd.read_csv("arquivo.csv", encoding="latin1") -- arquivos com acentuação "quebrada"
# pd.read_csv("arquivo.csv", index_col=0)       -- usa a primeira coluna como índice
# pd.read_csv("arquivo.csv", usecols=["produto", "preco_unitario"])  -- só algumas colunas
# pd.read_csv("arquivo.csv", nrows=100)         -- só as 100 primeiras linhas (útil p/ arquivos grandes)

# Salvando de volta para CSV
df.to_csv("vendas_salvas.csv", index=False)
# index=False evita salvar o índice numérico (0, 1, 2...) como uma coluna extra
# -- normalmente é o que você quer, a menos que o índice tenha significado

# Lendo Excel (precisa da biblioteca openpyxl: pip install openpyxl)
# df_excel = pd.read_excel("vendas.xlsx", sheet_name="Vendas2024")
# df.to_excel("vendas_salvas.xlsx", index=False, sheet_name="Vendas")

# Lendo JSON
import json

dados_json = json.dumps([
    {"produto": "Caneta Azul", "quantidade": 3, "preco_unitario": 2.50},
    {"produto": "Caderno", "quantidade": 1, "preco_unitario": 15.90},
])
df_json = pd.read_json(StringIO(dados_json))
print(df_json)

# Salvando em JSON
df_json.to_json("vendas.json", orient="records", indent=2)
# orient="records" gera uma lista de objetos (o formato mais comum de JSON de tabela)

# Lendo direto de uma URL (quando o dataset é público) -- read_csv aceita URL como caminho
# df_publico = pd.read_csv("https://exemplo.com/dataset.csv")
```

## Erros comuns de quem está começando

- Não passar `index=False` ao salvar com `to_csv`/`to_excel`, gerando uma
  coluna extra sem nome (`Unnamed: 0`) toda vez que o arquivo é lido de
  volta — isso acontece porque o índice do DataFrame foi salvo como se fosse
  dado.
- Assumir que o separador é sempre vírgula. Muitos CSVs exportados no Brasil
  (Excel em português, por exemplo) usam ponto e vírgula (`;`) como
  separador — se as colunas aparecerem todas "grudadas" numa só ao ler,
  tente `sep=";"`.
- Esquecer de instalar a dependência extra do Excel (`openpyxl` para
  `.xlsx`) — Pandas lê CSV nativamente, mas Excel e alguns outros formatos
  exigem uma biblioteca auxiliar instalada à parte.

## Exercício prático

1. Usando `StringIO` (sem precisar de um arquivo real), crie um CSV inline
   com colunas `nome,idade,cidade` e pelo menos 3 linhas de dados fictícios.
   Carregue-o com `pd.read_csv`.
2. Salve esse DataFrame em um arquivo `pessoas.csv` de verdade, usando
   `index=False`.
3. Leia o arquivo `pessoas.csv` de volta com `pd.read_csv` e confirme
   (imprimindo) que os dados batem com o original.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd
from io import StringIO

csv_texto = """nome,idade,cidade
Marcos,34,São Paulo
Julia,28,Rio de Janeiro
Pedro,41,Belo Horizonte
"""

df = pd.read_csv(StringIO(csv_texto))
print(df)

df.to_csv("pessoas.csv", index=False)

df_lido = pd.read_csv("pessoas.csv")
print(df_lido)
```

</details>

## Checklist antes de avançar

- [ ] Sei ler um CSV com `pd.read_csv` e ajustar `sep`/`encoding` quando necessário
- [ ] Sei salvar um DataFrame com `to_csv(..., index=False)` e explicar por que o `index=False` importa
- [ ] Sei que Excel e outros formatos podem exigir bibliotecas extras instaladas
- [ ] Resolvi o exercício sem olhar a solução
