# Ordenação

> Módulo 4 — Pandas Essencial · Tópico 7 de 12

## O que é e por que importa

Ordenar dados é uma das tarefas mais simples e mais usadas em análise: "quais
os 10 produtos mais vendidos", "quem são os clientes que mais compraram",
"do dia com mais faturamento para o com menos". Pandas faz isso com
`.sort_values()` (ordenar pelos valores de uma ou mais colunas) e
`.sort_index()` (ordenar pelo índice).

## Como funciona (com exemplo comentado)

```python
import pandas as pd

df = pd.DataFrame({
    "produto": ["Caneta Azul", "Caderno", "Mochila", "Lapis HB", "Estojo"],
    "categoria": ["Papelaria", "Papelaria", "Acessorios", "Papelaria", "Acessorios"],
    "quantidade": [3, 1, 2, 5, 4],
    "preco_unitario": [2.50, 15.90, 89.90, 1.20, 25.00],
})

# sort_values -- ordena pelos valores de uma coluna, do menor para o maior (padrão)
por_preco = df.sort_values("preco_unitario")
print(por_preco)

# ascending=False -- do maior para o menor
por_preco_desc = df.sort_values("preco_unitario", ascending=False)
print(por_preco_desc)

# Ordenando por múltiplas colunas -- lista de colunas, na ordem de prioridade
# primeiro por categoria (A-Z), dentro de cada categoria por preço (maior pro menor)
multi = df.sort_values(["categoria", "preco_unitario"], ascending=[True, False])
print(multi)

# Depois de ordenar, o índice original "vem junto" (fica fora de ordem) --
# use reset_index(drop=True) se quiser um índice novo, sequencial
top_precos = df.sort_values("preco_unitario", ascending=False).reset_index(drop=True)
print(top_precos)
# drop=True descarta o índice antigo; sem isso, ele viraria uma coluna nova chamada "index"

# .head(n) depois de ordenar -- padrão clássico para "top N"
top_3_mais_caros = df.sort_values("preco_unitario", ascending=False).head(3)
print(top_3_mais_caros)

# .nlargest() / .nsmallest() -- atalho para o mesmo resultado, geralmente mais rápido
top_3_v2 = df.nlargest(3, "preco_unitario")
print(top_3_v2)

mais_baratos = df.nsmallest(2, "preco_unitario")
print(mais_baratos)

# sort_index -- ordena pelo índice (linhas), útil depois de filtros/concatenações
# que deixam o índice fora de ordem
embaralhado = df.sample(frac=1)  # embaralha as linhas aleatoriamente (útil para testar)
print(embaralhado.sort_index())  # volta para a ordem original 0, 1, 2, 3, 4
```

## Erros comuns de quem está começando

- Esquecer `ascending=False` e se confundir achando que o `.sort_values()`
  "não funcionou" quando na verdade ordenou do menor para o maior (o
  padrão), e não do maior para o menor como esperado.
- Esquecer `reset_index(drop=True)` depois de ordenar e ficar com um índice
  fora de ordem (`3, 0, 4, 1, 2` em vez de `0, 1, 2, 3, 4`) — não é um erro
  em si (o DataFrame continua funcionando normalmente), mas pode confundir
  em análises seguintes que dependem de posição.
- Passar uma lista de colunas para `sort_values` mas só um valor (não-lista)
  para `ascending`, esperando que ele se aplique a todas — quando são várias
  colunas com ordens diferentes, `ascending` também precisa ser uma lista do
  mesmo tamanho, na mesma ordem das colunas.

## Exercício prático

```python
df = pd.DataFrame({
    "aluno": ["Marcos", "Julia", "Pedro", "Ana", "Carlos"],
    "nota": [7.5, 9.0, 5.5, 9.0, 6.0],
    "turma": ["A", "B", "A", "B", "A"],
})
```

1. Ordene o DataFrame pela nota, da maior para a menor.
2. Descubra os 2 alunos com as maiores notas usando `.nlargest()`.
3. Ordene por `turma` (A-Z) e, dentro de cada turma, por `nota` (maior para
   menor).
4. Depois de ordenar por nota (item 1), resete o índice para ficar
   sequencial de novo (0, 1, 2, 3, 4), sem manter o índice antigo como
   coluna.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

df = pd.DataFrame({
    "aluno": ["Marcos", "Julia", "Pedro", "Ana", "Carlos"],
    "nota": [7.5, 9.0, 5.5, 9.0, 6.0],
    "turma": ["A", "B", "A", "B", "A"],
})

por_nota_desc = df.sort_values("nota", ascending=False)
print(por_nota_desc)

top_2 = df.nlargest(2, "nota")
print(top_2)

por_turma_e_nota = df.sort_values(["turma", "nota"], ascending=[True, False])
print(por_turma_e_nota)

resetado = por_nota_desc.reset_index(drop=True)
print(resetado)
```

</details>

## Checklist antes de avançar

- [ ] Sei ordenar por uma coluna, ascendente e descendente
- [ ] Sei ordenar por múltiplas colunas com prioridades diferentes
- [ ] Sei usar `.nlargest()`/`.nsmallest()` e `reset_index(drop=True)`
- [ ] Resolvi o exercício sem olhar a solução
