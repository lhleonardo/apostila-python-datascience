# Medidas de tendência central

> Módulo 6 — Estatística e EDA · Tópico 1 de 8

## O que é e por que importa

Medidas de tendência central respondem "qual é o valor típico desses
dados?" — um único número que resume o "centro" de uma coluna inteira. Você
já usou algumas delas (`mean()`, `median()`) nos módulos anteriores; aqui o
foco é entender **quando cada uma é apropriada**, porque escolher a errada
pode levar a conclusões enganosas.

As três principais são:

- **Média (mean)**: soma de todos os valores dividida pela quantidade.
  Sensível a outliers — um único valor muito alto ou baixo puxa a média na
  sua direção (visto no Módulo 5, Tópico 6).
- **Mediana (median)**: o valor do meio quando os dados são ordenados
  (ou a média dos dois valores centrais, se a quantidade for par). Não é
  afetada por outliers da mesma forma que a média.
- **Moda (mode)**: o valor que mais se repete. É a única das três que
  também funciona bem para dados categóricos (texto), não só números.

## Como funciona (com exemplo comentado)

```python
import pandas as pd

salarios = pd.Series([3200, 3500, 3800, 3900, 4100, 4200, 50000])

print(salarios.mean())    # 10385.71... -- fortemente puxada pelo valor 50000
print(salarios.median())  # 3900.0 -- representa melhor o "salário típico" aqui
print(salarios.mode())    # sem moda clara neste caso (todos os valores são únicos)

# Quando os dados NÃO têm outliers extremos, média e mediana ficam próximas
notas = pd.Series([7.0, 7.5, 8.0, 6.5, 7.2])
print(notas.mean())    # 7.24
print(notas.median())  # 7.2
# valores próximos -- sinal de que a distribuição é razoavelmente "equilibrada"

# Moda em dados categóricos (texto) -- a média/mediana não fazem sentido aqui
categorias = pd.Series(["Papelaria", "Papelaria", "Acessorios", "Papelaria", "Eletronicos"])
print(categorias.mode())  # 0    Papelaria -- a categoria mais frequente

# .mode() pode retornar mais de um valor em caso de empate
empatado = pd.Series([1, 1, 2, 2, 3])
print(empatado.mode())  # 0    1 \n 1    2 -- dois valores empatados como mais frequentes

# Aplicando a um DataFrame inteiro (colunas numéricas)
df = pd.DataFrame({
    "produto": ["A", "B", "C", "D", "E"],
    "preco": [25.0, 30.0, 28.0, 32.0, 27.0],
    "avaliacao": [4.5, 3.0, 4.8, 4.2, 4.0],
})
print(df[["preco", "avaliacao"]].mean())
print(df[["preco", "avaliacao"]].median())

# .describe() (Módulo 4, Tópico 3) já traz mean e median (como "50%") juntos
print(df["preco"].describe())

# Comparar mean e median é uma forma rápida de suspeitar de outliers ou
# assimetria na distribuição, mesmo antes de visualizar (Tópico 3)
diferenca = df["preco"].mean() - df["preco"].median()
print(diferenca)  # perto de 0 -> distribuição razoavelmente simétrica
```

Uma regra prática: sempre que `mean()` e `median()` estiverem bem diferentes
uma da outra, é sinal de que a distribuição tem assimetria (mais valores
concentrados de um lado) ou outliers puxando a média — vale investigar antes
de reportar só a média como "o valor típico".

## Erros comuns de quem está começando

- Reportar só a média em dados que têm outliers (como salários, preços de
  imóveis, faturamento de empresas), sem perceber que ela não representa bem
  o "típico" nesses casos — a mediana costuma ser mais informativa quando a
  distribuição é bem assimétrica.
- Calcular média ou mediana de uma coluna categórica (texto) por engano —
  essas medidas só fazem sentido para números; para texto, a medida
  equivalente é a moda.
- Ignorar `.mode()` quando ela retorna mais de um valor (empate) e assumir
  erroneamente que só existe uma moda — sempre checar quantos valores
  `.mode()` retornou antes de usar `.mode()[0]` diretamente.

## Exercício prático

```python
vendas_diarias = pd.Series([1200, 1350, 1100, 1280, 1400, 1150, 15000])
categoria_mais_vendida = pd.Series(["Papelaria", "Eletronicos", "Papelaria", "Papelaria", "Acessorios"])
```

1. Calcule média e mediana de `vendas_diarias` e compare os dois valores.
2. Explique (em um comentário) por que eles são tão diferentes.
3. Calcule a moda de `categoria_mais_vendida`.
4. Recalcule a média de `vendas_diarias` **excluindo** o valor 15000 e
   compare com a mediana calculada no item 1 — elas deveriam ficar bem mais
   próximas.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

vendas_diarias = pd.Series([1200, 1350, 1100, 1280, 1400, 1150, 15000])

print(vendas_diarias.mean())    # ~3068.6 -- puxada pelo valor 15000
print(vendas_diarias.median())  # 1280.0 -- mais próxima do dia "típico"
# a diferença grande entre média e mediana indica um outlier (15000)
# puxando a média para cima

categoria_mais_vendida = pd.Series(["Papelaria", "Eletronicos", "Papelaria", "Papelaria", "Acessorios"])
print(categoria_mais_vendida.mode())  # Papelaria

sem_outlier = vendas_diarias[vendas_diarias != 15000]
print(sem_outlier.mean())  # ~1246.7 -- agora bem próxima da mediana original (1280)
```

</details>

## Checklist antes de avançar

- [ ] Sei calcular média, mediana e moda com Pandas
- [ ] Sei explicar quando a mediana é mais apropriada que a média
- [ ] Sei que moda funciona tanto para números quanto para texto
- [ ] Resolvi o exercício sem olhar a solução
