# Tabelas dinâmicas (pivot_table)

> Módulo 4 — Pandas Essencial · Tópico 12 de 12 (último do módulo)

## O que é e por que importa

Se você já usou tabela dinâmica no Excel ou Google Sheets, `pivot_table` do
Pandas é exatamente essa ideia em código: reorganizar dados "compridos"
(uma linha por registro) numa tabela "larga" que cruza duas dimensões — por
exemplo, produtos nas linhas e meses nas colunas, com o faturamento em cada
célula. É extremamente útil para criar resumos que ficam fáceis de ler e
comparar visualmente.

`pivot_table` é, na prática, um `groupby` (Tópico 8) que organiza o resultado
de um jeito diferente: em vez de uma coluna por categoria de agrupamento, ele
espalha uma das dimensões pelas **colunas** da tabela.

## Como funciona (com exemplo comentado)

```python
import pandas as pd

vendas = pd.DataFrame({
    "produto": ["Caneta", "Caneta", "Caderno", "Caderno", "Mochila", "Mochila"],
    "mes": ["Jan", "Fev", "Jan", "Fev", "Jan", "Fev"],
    "quantidade": [10, 15, 5, 8, 2, 3],
    "faturamento": [25.0, 37.5, 79.5, 127.2, 179.8, 269.7],
})
print(vendas)

# pivot_table: index = vai virar linha, columns = vai virar coluna,
# values = o que preencher nas células, aggfunc = como agregar (padrão: mean)
tabela = vendas.pivot_table(
    index="produto",
    columns="mes",
    values="faturamento",
    aggfunc="sum",
)
print(tabela)
# mes         Fev    Jan
# produto
# Caderno   127.2   79.5
# Caneta     37.5   25.0
# Mochila   269.7  179.8

# Comparando com o groupby equivalente (Tópico 8) -- o resultado tem os mesmos
# números, só que "compridos" em vez de "largos":
equivalente_groupby = vendas.groupby(["produto", "mes"])["faturamento"].sum()
print(equivalente_groupby)
# produto  mes
# Caderno  Fev    127.2
#          Jan     79.5
# Caneta   Fev     37.5
#          Jan     25.0
# Mochila  Fev    269.7
#          Jan    179.8

# fill_value -- preenche combinações que não existem nos dados com um valor
# (por padrão ficariam como NaN)
tabela_preenchida = vendas.pivot_table(
    index="produto", columns="mes", values="faturamento",
    aggfunc="sum", fill_value=0,
)

# margins=True -- adiciona uma linha e coluna de totais gerais
tabela_com_totais = vendas.pivot_table(
    index="produto", columns="mes", values="faturamento",
    aggfunc="sum", margins=True, margins_name="Total",
)
print(tabela_com_totais)
#             Fev    Jan   Total
# produto
# Caderno   127.2   79.5   206.7
# Caneta     37.5   25.0    62.5
# Mochila   269.7  179.8   449.5
# Total     434.4  284.3   718.7

# Múltiplos valores agregados de uma vez
tabela_multipla = vendas.pivot_table(
    index="produto", columns="mes",
    values=["faturamento", "quantidade"],
    aggfunc="sum",
)
print(tabela_multipla)

# Voltando de "larga" para "comprida" com melt (operação inversa ao pivot)
comprida = tabela.reset_index().melt(id_vars="produto", var_name="mes", value_name="faturamento")
print(comprida)
```

## Erros comuns de quem está começando

- Esquecer `aggfunc` quando há mais de um valor para a mesma combinação de
  `index`/`columns` — o padrão é `"mean"` (média), o que pode não ser o que
  você quer (frequentemente é `"sum"` para totais de vendas, por exemplo).
- Não usar `fill_value=0` quando faz sentido, e depois se confundir com
  `NaN` aparecendo em células cuja combinação simplesmente não tem dados
  (por exemplo, um produto que só foi vendido num mês).
- Achar que `pivot_table` é uma ferramenta completamente diferente de
  `groupby`, quando na prática resolve o mesmo tipo de pergunta — vale a
  pena pensar em qual formato de resultado (comprido, do `groupby`, ou
  largo, do `pivot_table`) é mais útil para o próximo passo da análise.

## Exercício prático

```python
notas = pd.DataFrame({
    "aluno": ["Marcos", "Marcos", "Julia", "Julia", "Pedro", "Pedro"],
    "materia": ["Matemática", "Português", "Matemática", "Português", "Matemática", "Português"],
    "nota": [7.5, 8.0, 9.0, 6.5, 5.5, 7.0],
})
```

1. Crie uma tabela dinâmica com alunos nas linhas, matérias nas colunas e a
   nota como valor (use `aggfunc="mean"`, já que cada combinação aluno/matéria
   tem só um valor).
2. Adicione `margins=True` para ver a média geral por aluno e por matéria.
3. Descubra, olhando a tabela, qual aluno teve a maior média geral.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

notas = pd.DataFrame({
    "aluno": ["Marcos", "Marcos", "Julia", "Julia", "Pedro", "Pedro"],
    "materia": ["Matemática", "Português", "Matemática", "Português", "Matemática", "Português"],
    "nota": [7.5, 8.0, 9.0, 6.5, 5.5, 7.0],
})

tabela = notas.pivot_table(index="aluno", columns="materia", values="nota", aggfunc="mean")
print(tabela)

tabela_com_totais = notas.pivot_table(
    index="aluno", columns="materia", values="nota",
    aggfunc="mean", margins=True, margins_name="Média",
)
print(tabela_com_totais)
# Julia tem a maior média geral (coluna "Média", linha "Julia")
```

</details>

## Checklist antes de avançar

- [ ] Sei criar uma tabela dinâmica com `index`, `columns`, `values` e `aggfunc`
- [ ] Entendo a relação entre `pivot_table` e `groupby` (mesma informação, formatos diferentes)
- [ ] Sei usar `fill_value` e `margins` quando fazem sentido
- [ ] Resolvi o exercício sem olhar a solução

## Checklist do Módulo 4

Antes de seguir para o Módulo 5 (Limpeza de Dados), confirme que você
consegue, sem consultar a apostila:

- [ ] Explicar a diferença entre Series e DataFrame
- [ ] Ler e salvar dados em CSV (e saber que Excel/JSON seguem padrão parecido)
- [ ] Explorar um dataset novo com `.head()`, `.info()`, `.describe()`, `.value_counts()`
- [ ] Selecionar dados com `.loc` e `.iloc`, sabendo a diferença entre eles
- [ ] Filtrar linhas com condições simples e combinadas (`&`, `|`, `.isin()`)
- [ ] Criar e modificar colunas, inclusive com `.apply()` quando necessário
- [ ] Ordenar um DataFrame por uma ou mais colunas
- [ ] Agrupar dados com `groupby` e agregar com `.agg()`
- [ ] Combinar tabelas com `concat` e `merge`, escolhendo o `how` certo
- [ ] Identificar e tratar valores ausentes básicos com `dropna`/`fillna`
- [ ] Criar uma tabela dinâmica com `pivot_table`

Pronto? Siga para o [Módulo 5 — Limpeza de Dados](../05-limpeza-de-dados/00-indice.md).
