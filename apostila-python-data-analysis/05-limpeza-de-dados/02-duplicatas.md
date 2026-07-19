# Duplicatas

> Módulo 5 — Limpeza de Dados · Tópico 2 de 7

## O que é e por que importa

Linhas duplicadas aparecem por vários motivos: um formulário enviado duas
vezes por engano, um erro num `merge` (Módulo 4, Tópico 10) que multiplicou
linhas, uma importação de dados rodada mais de uma vez. Se não forem
tratadas, duplicatas inflam contagens e somas — um faturamento "duplicado"
parece maior do que realmente é. Identificar e remover duplicatas
corretamente é um passo básico de qualquer limpeza de dados.

## Como funciona (com exemplo comentado)

```python
import pandas as pd

df = pd.DataFrame({
    "pedido_id": [1, 2, 3, 2, 4, 3],
    "cliente": ["Marcos", "Julia", "Pedro", "Julia", "Ana", "Pedro"],
    "valor": [150.0, 89.9, 45.0, 89.9, 200.0, 45.0],
})
print(df)

# .duplicated() -- retorna True para linhas que são cópia EXATA de uma anterior
print(df.duplicated())
# 0    False
# 1    False
# 2    False
# 3     True   <- igual à linha 1
# 4    False
# 5     True   <- igual à linha 2
# dtype: bool

# Contar quantas linhas duplicadas existem
print(df.duplicated().sum())  # 2

# Ver quais linhas são as duplicadas
print(df[df.duplicated()])

# .drop_duplicates() -- remove as duplicatas, mantendo a PRIMEIRA ocorrência (padrão)
df_sem_duplicatas = df.drop_duplicates()
print(df_sem_duplicatas)

# keep="last" -- mantém a ÚLTIMA ocorrência em vez da primeira
df_mantendo_ultima = df.drop_duplicates(keep="last")

# keep=False -- remove TODAS as ocorrências envolvidas em duplicação (não sobra nenhuma)
df_remove_todas = df.drop_duplicates(keep=False)

# subset -- considera duplicata só olhando algumas colunas, não a linha inteira
# útil quando "pedido_id" repetido já é suficiente para considerar duplicata,
# mesmo que outras colunas (por acaso) sejam diferentes
df_por_pedido_id = df.drop_duplicates(subset=["pedido_id"])
print(df_por_pedido_id)

# Sempre reset_index depois de remover linhas, se a ordem/índice sequencial importar
df_limpo = df.drop_duplicates().reset_index(drop=True)
print(df_limpo)
```

Um ponto sutil: `duplicated()` (sem `subset`) considera duas linhas iguais
somente se **todas as colunas** baterem. Isso significa que duas linhas
podem representar o mesmo evento do mundo real (o mesmo pedido, por exemplo)
sem serem detectadas como duplicatas, se algum campo (como um timestamp de
processamento) for ligeiramente diferente. Por isso é importante pensar em
qual é a **chave de identidade** real dos seus dados — normalmente um ID —
e usar `subset` para refletir isso.

## Erros comuns de quem está começando

- Rodar `drop_duplicates()` sem `subset` acreditando que remove duplicatas
  "de negócio" (ex: o mesmo pedido registrado duas vezes), quando na
  verdade só remove linhas 100% idênticas em todas as colunas — se houver
  qualquer diferença mínima entre elas (mesmo um espaço extra no texto),
  não são detectadas.
- Não verificar `duplicated().sum()` antes de agregar ou somar dados,
  chegando a totais inflados sem perceber a causa.
- Usar `keep=False` (remove todas as ocorrências) quando o objetivo era só
  "manter uma cópia" (`keep="first"`, o padrão) — isso descarta até a
  primeira ocorrência legítima do dado, que não deveria ser removida.

## Exercício prático

```python
df = pd.DataFrame({
    "cliente_id": [1, 2, 3, 1, 4, 2],
    "email": ["a@x.com", "b@x.com", "c@x.com", "a@x.com", "d@x.com", "b@x.com"],
    "cadastro": ["2024-01-10", "2024-01-11", "2024-01-12", "2024-02-01", "2024-01-15", "2024-03-01"],
})
```

1. Descubra quantas linhas são duplicatas exatas (considerando todas as
   colunas).
2. Descubra quantos `cliente_id` aparecem mais de uma vez, mesmo que a data
   de `cadastro` seja diferente (use `subset=["cliente_id"]`).
3. Remova duplicatas por `cliente_id`, mantendo a ocorrência com a data de
   cadastro **mais antiga** (dica: ordene por `cadastro` antes de usar
   `drop_duplicates(subset=..., keep="first")`).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

df = pd.DataFrame({
    "cliente_id": [1, 2, 3, 1, 4, 2],
    "email": ["a@x.com", "b@x.com", "c@x.com", "a@x.com", "d@x.com", "b@x.com"],
    "cadastro": ["2024-01-10", "2024-01-11", "2024-01-12", "2024-02-01", "2024-01-15", "2024-03-01"],
})

print(df.duplicated().sum())  # 0 -- nenhuma linha é 100% idêntica (cadastro difere)

duplicados_por_cliente = df.duplicated(subset=["cliente_id"]).sum()
print(duplicados_por_cliente)  # 2 (cliente_id 1 e 2 aparecem duas vezes)

df_ordenado = df.sort_values("cadastro")
df_mais_antigo = df_ordenado.drop_duplicates(subset=["cliente_id"], keep="first")
print(df_mais_antigo.sort_values("cliente_id"))
```

</details>

## Checklist antes de avançar

- [ ] Sei identificar duplicatas exatas e contar quantas existem
- [ ] Sei usar `subset` para detectar duplicatas por uma chave de negócio específica
- [ ] Sei escolher entre `keep="first"`, `"last"` e `False` de acordo com o objetivo
- [ ] Resolvi o exercício sem olhar a solução
