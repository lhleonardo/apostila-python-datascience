# Estratégias para valores ausentes

> Módulo 5 — Limpeza de Dados · Tópico 1 de 7

## O que é e por que importa

No Módulo 4 (Tópico 11) você aprendeu a **identificar** e fazer operações
básicas (`dropna`, `fillna`) com valores ausentes. Aqui o foco muda: como
**decidir** o que fazer com eles. Essa decisão não é mecânica — depende do
que os dados significam e de quanto cada abordagem pode distorcer a análise.

Existem, na prática, quatro caminhos principais:

1. **Remover a linha** — quando o dado ausente é raro e a linha inteira
   perde sentido sem ele.
2. **Remover a coluna** — quando a maior parte dos valores da coluna está
   ausente (ela adiciona pouca informação).
3. **Preencher com um valor fixo ou estatística** (média, mediana, moda,
   "desconhecido") — quando remover perderia dados bons demais.
4. **Preencher usando outras colunas ou linhas próximas** (interpolação,
   preenchimento por grupo) — quando existe uma forma mais informada de
   estimar o valor que faltou.

## Como funciona (com exemplo comentado)

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "produto": ["Caneta", "Caderno", "Mochila", "Lapis", "Estojo", "Borracha"],
    "categoria": ["Papelaria", "Papelaria", "Acessorios", None, "Acessorios", "Papelaria"],
    "preco": [2.5, 15.9, 89.9, 1.2, np.nan, 0.9],
    "avaliacao": [4.5, np.nan, np.nan, np.nan, np.nan, 3.8],
})

# Passo 1: sempre visualizar a extensão do problema, coluna a coluna
print(df.isnull().sum())
print((df.isnull().sum() / len(df) * 100).round(1))
# categoria: 1 de 6 (16.7%)  -- razoável preencher
# preco:     1 de 6 (16.7%)  -- razoável preencher
# avaliacao: 4 de 6 (66.7%)  -- muito ausente, considerar remover a coluna

# Estratégia 1: remover coluna com ausência muito alta
df_sem_avaliacao = df.drop(columns=["avaliacao"])

# Estratégia 2: remover linhas específicas (quando o dado é essencial e raro de faltar)
df_sem_preco_ausente = df.dropna(subset=["preco"])

# Estratégia 3: preencher com estatística -- média/mediana para números
mediana_preco = df["preco"].median()
df["preco"] = df["preco"].fillna(mediana_preco)
# mediana costuma ser preferível à média quando há valores muito extremos
# (outliers) puxando a média para longe do "típico" -- mais no Tópico 6

# Estratégia 3b: preencher categórico com a moda (valor mais frequente) ou um rótulo fixo
moda_categoria = df["categoria"].mode()[0]  # .mode() retorna uma Series (pode ter empate)
df["categoria"] = df["categoria"].fillna(moda_categoria)
# alternativa, muitas vezes mais honesta que "inventar" uma categoria:
# df["categoria"] = df["categoria"].fillna("Não informado")

# Estratégia 4: preencher por grupo -- usa a média/mediana DENTRO de cada categoria,
# mais preciso do que usar uma média geral que ignora o contexto
df2 = pd.DataFrame({
    "produto": ["A", "B", "C", "D", "E"],
    "categoria": ["X", "X", "Y", "Y", "Y"],
    "preco": [10.0, np.nan, 50.0, 55.0, np.nan],
})
df2["preco"] = df2.groupby("categoria")["preco"].transform(lambda s: s.fillna(s.mean()))
print(df2)
#   produto categoria  preco
# 0       A         X   10.0
# 1       B         X   10.0   <- preenchido com a média do grupo X (só tinha 10.0)
# 2       C         Y   50.0
# 3       D         Y   55.0
# 4       E         Y   52.5   <- preenchido com a média do grupo Y (50 e 55)

# Estratégia 4b: interpolação -- estima valores ausentes com base na tendência
# dos vizinhos, útil sobretudo em séries temporais (mais sobre datas no Tópico 5)
serie_temporal = pd.Series([10, 12, np.nan, 16, 18])
print(serie_temporal.interpolate())  # [10. 12. 14. 16. 18.] -- preencheu com a média linear
```

## Erros comuns de quem está começando

- Preencher todos os valores ausentes com a **média geral** sem considerar
  contexto (grupos, categorias), gerando estimativas piores do que preencher
  por grupo — como no exemplo do `df2` acima, a média geral ignoraria que os
  produtos da categoria "Y" custam bem mais que os da "X".
- Remover linhas com qualquer valor ausente (`dropna()` sem `subset`) de
  forma automática, sem checar antes se isso descarta uma fatia grande e
  possivelmente enviesada dos dados (por exemplo, se só clientes de uma
  região específica não preenchem um campo).
- Preencher valores ausentes numéricos com `0` "porque é neutro", quando
  `0` na verdade tem um significado real diferente de "não sei" (por
  exemplo, preço `0` parece uma promoção, não um dado ausente) — nesses
  casos, `NaN` é mais honesto do que um `0` inventado.

## Exercício prático

```python
df = pd.DataFrame({
    "cidade": ["São Paulo", "São Paulo", "Rio de Janeiro", "Rio de Janeiro", "Salvador"],
    "aluguel_medio": [3500, np.nan, 2200, 2400, np.nan],
    "corretor": ["Marcos", "Julia", "Marcos", None, "Pedro"],
})
```

1. Calcule a porcentagem de valores ausentes em cada coluna.
2. Preencha `aluguel_medio` usando a média **por cidade** (com `groupby` +
   `transform`, como no exemplo).
3. Preencha `corretor` ausente com o texto `"Não atribuído"`.
4. Confirme, ao final, que não sobrou nenhum valor ausente no DataFrame.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "cidade": ["São Paulo", "São Paulo", "Rio de Janeiro", "Rio de Janeiro", "Salvador"],
    "aluguel_medio": [3500, np.nan, 2200, 2400, np.nan],
    "corretor": ["Marcos", "Julia", "Marcos", None, "Pedro"],
})

print((df.isnull().sum() / len(df) * 100).round(1))

df["aluguel_medio"] = df.groupby("cidade")["aluguel_medio"].transform(lambda s: s.fillna(s.mean()))
# Salvador só tem 1 linha e ela está ausente -> continua NaN (não há outro
# valor no grupo para calcular a média) -- essa é uma limitação real da
# técnica que vale reconhecer

df["corretor"] = df["corretor"].fillna("Não atribuído")

print(df.isnull().sum())
# aluguel_medio ainda tem 1 ausente (Salvador) -- precisaria de outra estratégia
# (ex: média geral como fallback) para esse caso específico
```

</details>

## Checklist antes de avançar

- [ ] Sei calcular a porcentagem de valores ausentes por coluna antes de decidir o que fazer
- [ ] Sei escolher entre remover, preencher com estatística geral ou preencher por grupo
- [ ] Entendo por que preencher com `0` nem sempre é uma boa ideia
- [ ] Resolvi o exercício sem olhar a solução
