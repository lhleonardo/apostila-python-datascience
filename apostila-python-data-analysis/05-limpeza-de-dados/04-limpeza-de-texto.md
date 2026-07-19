# Limpeza de texto

> Módulo 5 — Limpeza de Dados · Tópico 4 de 7

## O que é e por que importa

Colunas de texto são as que mais sofrem com inconsistência: a mesma cidade
escrita como `"São Paulo"`, `"sao paulo"`, `" São Paulo "` (com espaços
extras) ou `"SP"` — para um humano é óbvio que é a mesma coisa, mas para o
Pandas são valores completamente diferentes, o que quebra `groupby`,
`value_counts()` e filtros. Padronizar texto é um passo quase obrigatório
antes de qualquer análise séria envolvendo colunas categóricas.

Pandas expõe operações de string através do acessor `.str`, que aplica
métodos de string do Python (que você já viu no Módulo 1, tópicos 14-15) a
uma coluna inteira de uma vez, de forma vetorizada.

## Como funciona (com exemplo comentado)

```python
import pandas as pd

df = pd.DataFrame({
    "cidade": [" São Paulo", "sao paulo", "SÃO PAULO ", "Rio de Janeiro", "RIO DE JANEIRO"],
    "email": ["Marcos@Email.com", " julia@email.com", "PEDRO@EMAIL.COM", "ana@email.com ", "carlos@email.com"],
})

# .str.strip() -- remove espaços extras no início/fim (igual ao .strip() de string comum)
df["cidade"] = df["cidade"].str.strip()

# .str.lower() / .str.upper() / .str.title() -- padroniza capitalização
df["cidade"] = df["cidade"].str.lower()
print(df["cidade"].unique())
# ['são paulo' 'sao paulo' 'rio de janeiro']
# -- "são paulo" e "sao paulo" ainda são diferentes por causa do acento!

# Removendo acentos para padronizar de verdade (usando unicodedata, do Python puro)
import unicodedata

def remover_acentos(texto):
    nfkd = unicodedata.normalize("NFKD", texto)
    return "".join(c for c in nfkd if not unicodedata.combining(c))

df["cidade"] = df["cidade"].apply(remover_acentos)
print(df["cidade"].unique())
# ['sao paulo' 'rio de janeiro'] -- agora sim, valores únicos de verdade

# .str.title() -- deixa com a primeira letra de cada palavra maiúscula, para exibição
df["cidade_exibicao"] = df["cidade"].str.title()
print(df["cidade_exibicao"])  # "Sao Paulo", "Rio De Janeiro"

# .str.contains() -- filtra linhas cujo texto contém um padrão (aceita regex, ver Módulo 2 Tópico 3)
gmail_ou_email = df[df["email"].str.strip().str.contains("email.com")]
print(gmail_ou_email)

# .str.replace() -- substituir parte do texto (vetorizado, igual visto no Tópico 3)
df["email"] = df["email"].str.strip().str.lower()
print(df["email"])

# .str.split() -- divide o texto em partes, retorna listas (ou colunas separadas com expand=True)
nomes = pd.Series(["Marcos Silva", "Julia Santos", "Pedro Costa"])
partes = nomes.str.split(" ", expand=True)
print(partes)
#          0       1
# 0   Marcos   Silva
# 1    Julia  Santos
# 2    Pedro   Costa

# map() com dicionário -- para padronizar abreviações conhecidas em valores completos
mapa_estados = {"SP": "São Paulo", "RJ": "Rio de Janeiro", "MG": "Minas Gerais"}
siglas = pd.Series(["SP", "RJ", "SP", "MG"])
print(siglas.map(mapa_estados))
```

## Erros comuns de quem está começando

- Rodar `.unique()` ou `.value_counts()` numa coluna de texto e assumir que
  os valores estão corretos, sem notar variações sutis de espaço, acento ou
  capitalização que fazem o Pandas contar "São Paulo" e "sao paulo" como
  categorias diferentes.
- Esquecer o `.str` antes do método de string (`df["cidade"].lower()` em vez
  de `df["cidade"].str.lower()`) — sem o acessor `.str`, o Pandas tenta
  achar um método `lower()` na própria Series (que não existe) e gera erro.
- Aplicar `.str.strip()`/`.str.lower()` só nas colunas que "parecem"
  precisar, sem checar todas as colunas de texto do dataset — inconsistência
  de espaço/capitalização costuma aparecer em mais lugares do que se espera.

## Exercício prático

```python
df = pd.DataFrame({
    "categoria": [" Eletrônicos", "eletronicos", "ELETRÔNICOS ", "Roupas", "roupas "],
    "cliente": ["Ana Paula Souza", "Jose Roberto Lima", "Marcia Andrade"],
})
```
(considere só a coluna `categoria` para os itens 1-3, com 5 valores)

1. Remova espaços extras e converta `categoria` para minúsculas.
2. Remova os acentos da coluna `categoria` (use a função `remover_acentos`
   do exemplo) e confirme com `.unique()` que sobraram só 2 categorias
   distintas.
3. Na coluna `cliente` (3 valores), separe em duas colunas `primeiro_nome` e
   `sobrenome_completo` usando `.str.split(" ", n=1, expand=True)` (o
   parâmetro `n=1` limita a divisão ao primeiro espaço).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd
import unicodedata

def remover_acentos(texto):
    nfkd = unicodedata.normalize("NFKD", texto)
    return "".join(c for c in nfkd if not unicodedata.combining(c))

categorias = pd.Series([" Eletrônicos", "eletronicos", "ELETRÔNICOS ", "Roupas", "roupas "])
categorias = categorias.str.strip().str.lower()
categorias = categorias.apply(remover_acentos)
print(categorias.unique())  # ['eletronicos' 'roupas']

clientes = pd.Series(["Ana Paula Souza", "Jose Roberto Lima", "Marcia Andrade"])
partes = clientes.str.split(" ", n=1, expand=True)
partes.columns = ["primeiro_nome", "sobrenome_completo"]
print(partes)
```

</details>

## Checklist antes de avançar

- [ ] Sei usar `.str.strip()`, `.str.lower()`/`.upper()`/`.title()` para padronizar texto
- [ ] Sei que acentos precisam de tratamento à parte (não bastam `.lower()`/`.strip()`)
- [ ] Sei usar `.str.split(expand=True)` para dividir texto em colunas
- [ ] Resolvi o exercício sem olhar a solução
