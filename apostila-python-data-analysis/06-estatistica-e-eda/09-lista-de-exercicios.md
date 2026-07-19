# Lista de exercícios — Módulo 6

> Módulo 6 — Estatística e EDA · Lista de exercícios de revisão

Esta lista reúne 10 exercícios práticos para cada tópico do módulo, para
consolidar o que foi aprendido antes de avançar. Tente resolver cada
exercício sem consultar o tópico original primeiro — as soluções vêm logo
depois de cada bloco, dentro de um "clique para ver".

## 1. Medidas de tendência central

1. Dada `notas = pd.Series([6.0, 6.5, 7.0, 6.8, 7.2])`, calcule a média e a
   mediana.
2. Dada `precos = pd.Series([10, 12, 11, 13, 12])`, calcule a moda.
3. Dada `aluguel = pd.Series([1200, 1300, 1250, 1280, 1220])`, calcule média
   e mediana e diga (em comentário) se elas estão próximas.
4. Dada `salarios = pd.Series([2500, 2600, 2550, 2700, 2650, 40000])`,
   calcule média e mediana e explique em comentário por que são tão
   diferentes.
5. Dada `categorias = pd.Series(["Livro", "Caderno", "Livro", "Caneta", "Livro"])`,
   calcule a moda.
6. Dada `avaliacoes = pd.Series([5, 5, 4, 4, 3, 3])`, calcule a moda e
   verifique se há empate.
7. Dada `vendas = pd.Series([300, 320, 310, 295, 305, 2000])`, calcule a
   média com e sem o valor 2000, e compare com a mediana original.
8. Dado o DataFrame
   `df = pd.DataFrame({"produto": ["A","B","C","D"], "preco": [50, 55, 48, 300], "estoque": [10, 12, 9, 11]})`,
   calcule média e mediana de `preco` e `estoque`.
9. Usando o `df` do exercício 8, calcule a diferença entre média e mediana
   de `preco` e diga em comentário se isso indica outlier.
10. Dada `tempo_entrega = pd.Series([2, 3, 2, 3, 2, 3, 2, 20])` (dias),
    calcule média, mediana e moda, e escreva em comentário qual medida
    melhor representa o "tempo típico" de entrega.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd

notas = pd.Series([6.0, 6.5, 7.0, 6.8, 7.2])
print(notas.mean())    # 6.7
print(notas.median())  # 6.8
```

**2.**
```python
precos = pd.Series([10, 12, 11, 13, 12])
print(precos.mode())  # 12
```

**3.**
```python
aluguel = pd.Series([1200, 1300, 1250, 1280, 1220])
print(aluguel.mean())    # 1250.0
print(aluguel.median())  # 1250.0
# valores praticamente iguais -- distribuição equilibrada, sem outliers aparentes
```

**4.**
```python
salarios = pd.Series([2500, 2600, 2550, 2700, 2650, 40000])
print(salarios.mean())    # ~8666.7 -- fortemente puxada pelo valor 40000
print(salarios.median())  # 2625.0 -- representa melhor o salário "típico"
# a média é bem maior que a mediana porque o valor 40000 é um outlier que
# puxa a média para cima, enquanto a mediana não é afetada da mesma forma
```

**5.**
```python
categorias = pd.Series(["Livro", "Caderno", "Livro", "Caneta", "Livro"])
print(categorias.mode())  # 0    Livro
```

**6.**
```python
avaliacoes = pd.Series([5, 5, 4, 4, 3, 3])
print(avaliacoes.mode())  # 0    3 \n 1    4 \n 2    5 -- três valores empatados
```

**7.**
```python
vendas = pd.Series([300, 320, 310, 295, 305, 2000])
print(vendas.mean())                       # ~588.3 -- puxada pelo 2000
sem_outlier = vendas[vendas != 2000]
print(sem_outlier.mean())                  # ~306.0
print(vendas.median())                     # 307.5
# a média sem o outlier fica bem mais próxima da mediana original
```

**8.**
```python
df = pd.DataFrame({"produto": ["A","B","C","D"], "preco": [50, 55, 48, 300], "estoque": [10, 12, 9, 11]})
print(df[["preco", "estoque"]].mean())
print(df[["preco", "estoque"]].median())
```

**9.**
```python
diferenca = df["preco"].mean() - df["preco"].median()
print(diferenca)
# diferença grande -- indica que o valor 300 é um outlier puxando a média para cima
```

**10.**
```python
tempo_entrega = pd.Series([2, 3, 2, 3, 2, 3, 2, 20])
print(tempo_entrega.mean())    # ~4.625 -- puxada pelo valor 20
print(tempo_entrega.median())  # 2.5
print(tempo_entrega.mode())    # 0    2
# a mediana (ou a moda) representa melhor o tempo "típico" de entrega,
# já que a média é distorcida pelo valor 20, que é um caso atípico
```

</details>

## 2. Medidas de dispersão

1. Dada `turma = pd.Series([7.0, 7.2, 6.9, 7.1, 6.8])`, calcule a amplitude
   (max - min).
2. Dada `turma`, calcule a variância e o desvio padrão.
3. Dadas `equipe_a = pd.Series([100, 102, 98, 101, 99])` e
   `equipe_b = pd.Series([50, 150, 80, 120, 100])`, compare as médias e os
   desvios padrão.
4. Dada `precos = pd.Series([20, 22, 21, 23, 19, 100])`, calcule o IQR
   (Q3 - Q1).
5. Usando `precos` do exercício 4, calcule a amplitude e compare com o IQR —
   qual é mais afetada pelo valor 100?
6. Dadas `loja_x = pd.Series([500, 510, 495, 505, 500])` e
   `loja_y = pd.Series([300, 700, 400, 600, 500])`, calcule o coeficiente de
   variação (`std / mean`) de cada uma e diga qual é mais dispersa
   relativamente.
7. Dado o DataFrame
   `df = pd.DataFrame({"regiao": ["Norte","Norte","Sul","Sul"], "venda": [1000, 1100, 400, 1600]})`,
   calcule média e desvio padrão de `venda` agrupado por `regiao`.
8. Dada `atendimentos = pd.Series([5, 6, 5, 7, 6, 5, 40])`, calcule
   `.describe()` e identifique visualmente onde o desvio padrão fica alto
   por causa de um único valor.
9. Dadas duas séries com a mesma média
   `serie_a = pd.Series([10, 10, 10, 10, 10])` e
   `serie_b = pd.Series([5, 8, 10, 12, 15])`, calcule o desvio padrão de
   cada uma e explique em comentário o que isso revela sobre a consistência
   dos dados.
10. Dado `df = pd.DataFrame({"vendedor": ["X","X","X","Y","Y","Y"], "venda": [200, 210, 195, 50, 400, 150]})`,
    calcule média, desvio padrão e IQR de `venda` por `vendedor`, e decida
    (em comentário) qual vendedor é mais previsível.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd

turma = pd.Series([7.0, 7.2, 6.9, 7.1, 6.8])
print(turma.max() - turma.min())  # 0.4
```

**2.**
```python
print(turma.var())  # bem pequena
print(turma.std())  # ~0.16
```

**3.**
```python
equipe_a = pd.Series([100, 102, 98, 101, 99])
equipe_b = pd.Series([50, 150, 80, 120, 100])
print(equipe_a.mean(), equipe_b.mean())  # 100.0, 100.0 -- mesma média
print(equipe_a.std(), equipe_b.std())    # ~1.58 vs ~40.3 -- equipe B muito mais dispersa
```

**4.**
```python
precos = pd.Series([20, 22, 21, 23, 19, 100])
q1 = precos.quantile(0.25)
q3 = precos.quantile(0.75)
iqr = q3 - q1
print(iqr)
```

**5.**
```python
amplitude = precos.max() - precos.min()
print(amplitude, iqr)
# amplitude é muito maior porque considera o valor extremo 100 diretamente;
# o IQR é mais robusto pois olha só a metade central dos dados
```

**6.**
```python
loja_x = pd.Series([500, 510, 495, 505, 500])
loja_y = pd.Series([300, 700, 400, 600, 500])
cv_x = loja_x.std() / loja_x.mean()
cv_y = loja_y.std() / loja_y.mean()
print(cv_x, cv_y)  # cv_y bem maior -- loja Y proporcionalmente mais dispersa
```

**7.**
```python
df = pd.DataFrame({"regiao": ["Norte","Norte","Sul","Sul"], "venda": [1000, 1100, 400, 1600]})
print(df.groupby("regiao")["venda"].agg(["mean", "std"]))
```

**8.**
```python
atendimentos = pd.Series([5, 6, 5, 7, 6, 5, 40])
print(atendimentos.describe())
# std alto em relação à mean, mesmo com a maioria dos valores entre 5 e 7,
# porque o valor 40 é um outlier que infla bastante a variância
```

**9.**
```python
serie_a = pd.Series([10, 10, 10, 10, 10])
serie_b = pd.Series([5, 8, 10, 12, 15])
print(serie_a.mean(), serie_b.mean())  # 10.0, 10.0
print(serie_a.std())  # 0.0 -- totalmente consistente, sem variação
print(serie_b.std())  # bem maior -- valores espalhados mesmo com a mesma média
```

**10.**
```python
df = pd.DataFrame({"vendedor": ["X","X","X","Y","Y","Y"], "venda": [200, 210, 195, 50, 400, 150]})
resumo = df.groupby("vendedor")["venda"].agg(["mean", "std"])
print(resumo)
iqr_por_vendedor = df.groupby("vendedor")["venda"].quantile(0.75) - df.groupby("vendedor")["venda"].quantile(0.25)
print(iqr_por_vendedor)
# vendedor X tem desvio padrão e IQR bem menores -- é o mais previsível,
# mesmo que a média de vendas dos dois seja parecida
```

</details>

## 3. Distribuições e histogramas

1. Dada `idades = pd.Series([22, 25, 23, 24, 26, 23, 25])`, use `pd.cut`
   com 3 faixas e conte quantos valores caem em cada uma.
2. Dada `idades`, calcule `.skew()` e diga se a distribuição parece
   simétrica.
3. Dada `salarios = pd.Series([2000, 2100, 2200, 2050, 2150, 15000])`,
   calcule média, mediana e `.skew()`.
4. Com base no resultado do exercício 3, classifique a assimetria (à
   direita, à esquerda ou simétrica) em um comentário.
5. Dada `notas = pd.Series([9, 8.5, 9.2, 8.8, 1.0, 9.1, 8.7])`, calcule
   `.skew()` e explique o sinal em comentário.
6. Dada `vendas_por_hora = pd.Series([5, 6, 20, 21, 5, 6, 20, 22, 5])`, use
   `pd.cut` com 4 faixas e `.value_counts()` para verificar se há indício de
   bimodalidade.
7. Dada `tempo_resposta = pd.Series([1, 2, 1, 2, 1, 2, 30, 32])` (em
   minutos), calcule média, mediana e `.skew()`, e diga se há assimetria.
8. Compare as distribuições de `grupo_1 = pd.Series([10, 11, 9, 10, 12, 11])`
   e `grupo_2 = pd.Series([5, 5, 5, 25, 25, 25])` usando `.skew()` e
   `pd.cut` com 3 faixas cada.
9. Dada `precos_imoveis = pd.Series([200, 220, 210, 230, 215, 205, 900, 950])`
   (em milhares), use `pd.cut` com 5 faixas, calcule `.skew()`, e escreva em
   comentário uma interpretação completa da distribuição.
10. Teste diferentes valores de `bins` (3, 5 e 8) com `pd.cut` na série
    `dados = pd.Series([1,2,2,3,3,3,4,4,5,5,5,5,6,6,7,20])` e comente qual
    número de faixas revela melhor o padrão sem esconder nem exagerar
    detalhes.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd

idades = pd.Series([22, 25, 23, 24, 26, 23, 25])
print(pd.cut(idades, bins=3).value_counts().sort_index())
```

**2.**
```python
print(idades.skew())
# valor próximo de 0 -- distribuição aproximadamente simétrica
```

**3.**
```python
salarios = pd.Series([2000, 2100, 2200, 2050, 2150, 15000])
print(salarios.mean())    # bem puxada para cima
print(salarios.median())  # bem menor
print(salarios.skew())    # positivo
```

**4.**
```python
# skew positivo e média >> mediana -- assimetria à direita (cauda de valores altos)
```

**5.**
```python
notas = pd.Series([9, 8.5, 9.2, 8.8, 1.0, 9.1, 8.7])
print(notas.skew())
# skew negativo -- assimetria à esquerda, causada pelo valor baixo (1.0)
# puxando a cauda para valores menores
```

**6.**
```python
vendas_por_hora = pd.Series([5, 6, 20, 21, 5, 6, 20, 22, 5])
print(pd.cut(vendas_por_hora, bins=4).value_counts().sort_index())
# concentração em duas faixas separadas (baixa e alta) -- indício de bimodalidade
```

**7.**
```python
tempo_resposta = pd.Series([1, 2, 1, 2, 1, 2, 30, 32])
print(tempo_resposta.mean())    # puxada para cima
print(tempo_resposta.median())  # bem menor
print(tempo_resposta.skew())    # positivo -- assimetria à direita
```

**8.**
```python
grupo_1 = pd.Series([10, 11, 9, 10, 12, 11])
grupo_2 = pd.Series([5, 5, 5, 25, 25, 25])
print(grupo_1.skew(), grupo_2.skew())
print(pd.cut(grupo_1, bins=3).value_counts().sort_index())
print(pd.cut(grupo_2, bins=3).value_counts().sort_index())
# grupo_1 tem skew perto de 0 (concentrado); grupo_2 tem valores concentrados
# em duas faixas extremas -- padrão bimodal, não assimetria simples
```

**9.**
```python
precos_imoveis = pd.Series([200, 220, 210, 230, 215, 205, 900, 950])
print(pd.cut(precos_imoveis, bins=5).value_counts().sort_index())
print(precos_imoveis.skew())
# skew fortemente positivo -- a maioria dos imóveis está na faixa de 200-230,
# com um pequeno grupo de imóveis muito mais caros (perto de 900-950) puxando
# a cauda para a direita; pode indicar dois segmentos de mercado misturados
```

**10.**
```python
dados = pd.Series([1,2,2,3,3,3,4,4,5,5,5,5,6,6,7,20])
print(pd.cut(dados, bins=3).value_counts().sort_index())
print(pd.cut(dados, bins=5).value_counts().sort_index())
print(pd.cut(dados, bins=8).value_counts().sort_index())
# com 3 bins, o padrão central fica escondido dentro de uma faixa larga;
# com 8 bins, aparecem faixas vazias que fragmentam demais os dados;
# 5 bins equilibra bem, mostrando a concentração central e o outlier (20) separado
```

</details>

## 4. Correlação entre variáveis

1. Dado `df = pd.DataFrame({"horas_treino": [1,2,3,4,5], "desempenho": [50,55,62,68,75]})`,
   calcule a correlação entre `horas_treino` e `desempenho`.
2. Dado `df = pd.DataFrame({"idade_carro": [1,2,3,4,5], "valor_revenda": [50000,45000,40000,35000,30000]})`,
   calcule a correlação entre `idade_carro` e `valor_revenda`.
3. Dado `df = pd.DataFrame({"altura": [160,165,170,175,180], "nota_prova": [7,6,8,5,9]})`,
   calcule a correlação e diga em comentário se faz sentido interpretá-la.
4. Dado
   `df = pd.DataFrame({"gasto_marketing": [1000,2000,3000,4000,5000], "vendas": [10,25,28,45,52], "reclamacoes": [5,4,4,3,2]})`,
   gere a matriz de correlação completa.
5. Usando o `df` do exercício 4, identifique (em comentário) qual par de
   variáveis tem a correlação mais forte e qual sinal ela tem.
6. Dado
   `df = pd.DataFrame({"temperatura": [10,15,20,25,30,35], "vendas_chocolate_quente": [100,80,50,30,10,5]})`,
   calcule a correlação e interprete o sinal.
7. Dado `df = pd.DataFrame({"x": [1,2,3,4,5], "y": [3,3,3,3,3]})`, calcule a
   correlação entre `x` e `y` e explique em comentário o resultado (`y`
   constante).
8. Dado
   `df = pd.DataFrame({"preco": [10,20,30,40,50], "avaliacao": [4.8,4.5,4.0,3.5,3.0], "categoria": ["A","B","A","B","A"]})`,
   calcule `.corr(numeric_only=True)` e explique por que `categoria` não
   aparece na matriz.
9. Dado
   `df = pd.DataFrame({"experiencia_anos": [1,3,5,7,10,2,6], "salario": [3000,4200,5500,7000,9500,3500,6200]})`,
   calcule a correlação e escreva uma frase de interpretação sem afirmar
   causalidade.
10. Dado
    `df = pd.DataFrame({"horas_sono": [4,5,6,7,8,9], "produtividade": [40,55,70,85,90,60]})`,
    calcule a correlação de Pearson e discuta em comentário por que ela pode
    não capturar bem essa relação (dica: produtividade cai depois de 8h de
    sono, sugerindo uma relação não-linear).

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd

df = pd.DataFrame({"horas_treino": [1,2,3,4,5], "desempenho": [50,55,62,68,75]})
print(df["horas_treino"].corr(df["desempenho"]))  # perto de 1 -- forte positiva
```

**2.**
```python
df = pd.DataFrame({"idade_carro": [1,2,3,4,5], "valor_revenda": [50000,45000,40000,35000,30000]})
print(df["idade_carro"].corr(df["valor_revenda"]))  # -1 -- correlação negativa perfeita
```

**3.**
```python
df = pd.DataFrame({"altura": [160,165,170,175,180], "nota_prova": [7,6,8,5,9]})
print(df["altura"].corr(df["nota_prova"]))
# correlação fraca/próxima de zero é esperada -- não há razão teórica para
# altura estar relacionada com nota de prova; calcular não implica que faça sentido
```

**4.**
```python
df = pd.DataFrame({"gasto_marketing": [1000,2000,3000,4000,5000], "vendas": [10,25,28,45,52], "reclamacoes": [5,4,4,3,2]})
print(df.corr(numeric_only=True))
```

**5.**
```python
# gasto_marketing e vendas têm a correlação mais forte e positiva;
# gasto_marketing e reclamacoes têm correlação forte e negativa
```

**6.**
```python
df = pd.DataFrame({"temperatura": [10,15,20,25,30,35], "vendas_chocolate_quente": [100,80,50,30,10,5]})
print(df["temperatura"].corr(df["vendas_chocolate_quente"]))
# correlação forte e negativa -- conforme a temperatura sobe, as vendas de
# chocolate quente caem
```

**7.**
```python
df = pd.DataFrame({"x": [1,2,3,4,5], "y": [3,3,3,3,3]})
print(df["x"].corr(df["y"]))
# resultado é NaN -- não é possível calcular correlação quando uma das
# variáveis não tem variância (todos os valores iguais)
```

**8.**
```python
df = pd.DataFrame({"preco": [10,20,30,40,50], "avaliacao": [4.8,4.5,4.0,3.5,3.0], "categoria": ["A","B","A","B","A"]})
print(df.corr(numeric_only=True))
# "categoria" é texto (não numérica), então numeric_only=True a exclui
# automaticamente da matriz de correlação
```

**9.**
```python
df = pd.DataFrame({"experiencia_anos": [1,3,5,7,10,2,6], "salario": [3000,4200,5500,7000,9500,3500,6200]})
print(df["experiencia_anos"].corr(df["salario"]))
# correlação forte e positiva entre experiência e salário nesses dados;
# isso não prova que a experiência causa o salário maior, apenas que estão associados
```

**10.**
```python
df = pd.DataFrame({"horas_sono": [4,5,6,7,8,9], "produtividade": [40,55,70,85,90,60]})
print(df["horas_sono"].corr(df["produtividade"]))
# a correlação de Pearson mede relação LINEAR; aqui a produtividade sobe até
# 8h de sono e depois cai -- uma relação em forma de curva (não-linear) --
# o coeficiente de Pearson tende a subestimar essa relação, pois não captura
# a mudança de direção; vale visualizar os dados além de calcular o número
```

</details>

## 5. Análise univariada com Pandas

1. Dado `df = pd.DataFrame({"idade": [23, 31, 45, 29, 38], "cidade": ["SP","RJ","SP","MG","SP"]})`,
   faça a análise univariada completa (`.describe()`) da coluna `idade`.
2. Usando o mesmo `df`, faça a análise univariada da coluna `cidade` com
   `value_counts()` (absoluto e percentual).
3. Dado `df = pd.DataFrame({"nota": [7,8,6,9,7,8,10,5]})`, calcule
   `.skew()` e `.nunique()` da coluna `nota`.
4. Dado `df = pd.DataFrame({"produto": ["A","B","C","D"], "preco": [10,20,15,1000], "categoria": ["X","Y","X","Y"]})`,
   use `.select_dtypes()` para separar colunas numéricas e categóricas.
5. Usando o `df` do exercício 4, escreva uma função `resumo_numerico(serie)`
   que retorne média, mediana, desvio padrão, mínimo e máximo, e aplique-a
   à coluna `preco`.
6. Dado `df = pd.DataFrame({"avaliacao": [5,5,5,5,4,3,5,5]})`, calcule
   `value_counts(normalize=True)` da coluna `avaliacao` e diga em comentário
   se ela deveria ser tratada como numérica ou categórica.
7. Dado
   `df = pd.DataFrame({"funcionario": ["A","B","C","D","E"], "salario": [3000,3200,15000,3100,3300], "cargo": ["Jr","Jr","Diretor","Jr","Pleno"]})`,
   faça a análise univariada de `salario` (incluindo skew) e de `cargo`.
8. Usando o `df` do exercício 7, aplique `.select_dtypes(include="number")`
   e depois use `.apply()` com a função `resumo_numerico` do exercício 5
   nas colunas numéricas resultantes.
9. Dado
   `df = pd.DataFrame({"cliente": ["A","B","C","D","E","F"], "idade": [22,45,33,29,60,38], "plano": ["Basico","Premium","Basico","Basico","Premium","Basico"], "gasto": [40,180,55,60,220,50]})`,
   faça a análise univariada de todas as colunas (numéricas e categóricas)
   separadamente.
10. Usando o `df` do exercício 9, identifique (usando `.nunique()`) se a
    coluna `idade` deveria ser tratada como numérica contínua ou se tem
    poucos valores distintos que sugeririam tratá-la como categórica, e
    justifique em comentário.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd

df = pd.DataFrame({"idade": [23, 31, 45, 29, 38], "cidade": ["SP","RJ","SP","MG","SP"]})
print(df["idade"].describe())
```

**2.**
```python
print(df["cidade"].value_counts())
print(df["cidade"].value_counts(normalize=True) * 100)
```

**3.**
```python
df = pd.DataFrame({"nota": [7,8,6,9,7,8,10,5]})
print(df["nota"].skew())
print(df["nota"].nunique())
```

**4.**
```python
df = pd.DataFrame({"produto": ["A","B","C","D"], "preco": [10,20,15,1000], "categoria": ["X","Y","X","Y"]})
numericas = df.select_dtypes(include="number")
categoricas = df.select_dtypes(include="object")
print(numericas.columns.tolist())
print(categoricas.columns.tolist())
```

**5.**
```python
def resumo_numerico(serie):
    return pd.Series({
        "media": serie.mean(),
        "mediana": serie.median(),
        "desvio_padrao": serie.std(),
        "minimo": serie.min(),
        "maximo": serie.max(),
    })

print(resumo_numerico(df["preco"]))
```

**6.**
```python
df = pd.DataFrame({"avaliacao": [5,5,5,5,4,3,5,5]})
print(df["avaliacao"].value_counts(normalize=True))
# poucos valores distintos (3, 4, 5) -- faz mais sentido tratar como
# categórica/ordinal (com value_counts) do que calcular média/desvio padrão
```

**7.**
```python
df = pd.DataFrame({"funcionario": ["A","B","C","D","E"], "salario": [3000,3200,15000,3100,3300], "cargo": ["Jr","Jr","Diretor","Jr","Pleno"]})
print(df["salario"].describe())
print(df["salario"].skew())
print(df["cargo"].value_counts())
print(df["cargo"].value_counts(normalize=True) * 100)
```

**8.**
```python
numericas = df.select_dtypes(include="number")
print(numericas.apply(resumo_numerico))
```

**9.**
```python
df = pd.DataFrame({"cliente": ["A","B","C","D","E","F"], "idade": [22,45,33,29,60,38], "plano": ["Basico","Premium","Basico","Basico","Premium","Basico"], "gasto": [40,180,55,60,220,50]})
numericas = df.select_dtypes(include="number")
categoricas = df.select_dtypes(include="object")
print(numericas.apply(resumo_numerico))
print(df["plano"].value_counts(normalize=True) * 100)
```

**10.**
```python
print(df["idade"].nunique())
# 6 valores distintos para 6 linhas -- todos únicos, é uma variável
# contínua de fato, faz sentido tratá-la como numérica (média, desvio padrão)
# e não como categórica
```

</details>

## 6. Análise bivariada e segmentação

1. Dado
   `df = pd.DataFrame({"plano": ["Basico","Premium","Basico","Premium"], "gasto": [50,180,55,200]})`,
   calcule a média de `gasto` por `plano` usando `groupby`.
2. Usando o `df` do exercício 1, calcule também o desvio padrão e a
   contagem de cada grupo.
3. Dado
   `df = pd.DataFrame({"regiao": ["Sul","Norte","Sul","Norte"], "canal": ["Online","Loja","Loja","Online"]})`,
   gere uma tabela cruzada (`crosstab`) entre `regiao` e `canal`.
4. Usando o `df` do exercício 3, gere a mesma tabela cruzada normalizada por
   linha (`normalize="index"`).
5. Dado
   `df = pd.DataFrame({"anos_empresa": [1,3,5,8,12,2,6,15], "salario": [3000,4000,5500,7500,11000,3500,6200,15000]})`,
   calcule a correlação entre `anos_empresa` e `salario`.
6. Usando o `df` do exercício 5, segmente `anos_empresa` em 3 faixas com
   `pd.cut` (bins `[0, 5, 10, 16]`) e calcule a média de `salario` por
   faixa.
7. Dado
   `df = pd.DataFrame({"departamento": ["Vendas","TI","Vendas","TI","Vendas","TI"], "nivel": ["Jr","Sr","Pleno","Jr","Sr","Pleno"], "salario": [3000,9000,5000,3200,8500,5300]})`,
   crie uma `pivot_table` com a média salarial por `departamento` e `nivel`.
8. Usando o `df` do exercício 7, crie um `crosstab` entre `departamento` e
   `nivel`.
9. Dado
   `df = pd.DataFrame({"cidade": ["SP","SP","RJ","RJ","SP","RJ"], "satisfacao": [8,9,5,6,7,4]})`,
   calcule média e desvio padrão de `satisfacao` por `cidade`, e escreva em
   comentário qual cidade tem clientes mais satisfeitos e mais consistentes.
10. Dado
    `df = pd.DataFrame({"loja": ["A","A","A","B","B","B"], "vendedor": ["X","Y","X","Y","X","Y"], "venda": [500,700,550,650,600,720]})`,
    crie uma `pivot_table` com a média de `venda` por `loja` e `vendedor`, e
    segmente `venda` em 2 faixas com `pd.cut` cruzando com `loja` via
    `crosstab`.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd

df = pd.DataFrame({"plano": ["Basico","Premium","Basico","Premium"], "gasto": [50,180,55,200]})
print(df.groupby("plano")["gasto"].mean())
```

**2.**
```python
print(df.groupby("plano")["gasto"].agg(["mean", "std", "count"]))
```

**3.**
```python
df = pd.DataFrame({"regiao": ["Sul","Norte","Sul","Norte"], "canal": ["Online","Loja","Loja","Online"]})
print(pd.crosstab(df["regiao"], df["canal"]))
```

**4.**
```python
print(pd.crosstab(df["regiao"], df["canal"], normalize="index") * 100)
```

**5.**
```python
df = pd.DataFrame({"anos_empresa": [1,3,5,8,12,2,6,15], "salario": [3000,4000,5500,7500,11000,3500,6200,15000]})
print(df["anos_empresa"].corr(df["salario"]))  # forte positiva
```

**6.**
```python
df["faixa_anos"] = pd.cut(df["anos_empresa"], bins=[0, 5, 10, 16], labels=["0-5", "6-10", "11-16"])
print(df.groupby("faixa_anos", observed=True)["salario"].mean())
```

**7.**
```python
df = pd.DataFrame({"departamento": ["Vendas","TI","Vendas","TI","Vendas","TI"], "nivel": ["Jr","Sr","Pleno","Jr","Sr","Pleno"], "salario": [3000,9000,5000,3200,8500,5300]})
print(df.pivot_table(index="departamento", columns="nivel", values="salario", aggfunc="mean"))
```

**8.**
```python
print(pd.crosstab(df["departamento"], df["nivel"]))
```

**9.**
```python
df = pd.DataFrame({"cidade": ["SP","SP","RJ","RJ","SP","RJ"], "satisfacao": [8,9,5,6,7,4]})
print(df.groupby("cidade")["satisfacao"].agg(["mean", "std"]))
# SP tem satisfação média mais alta; comparar o desvio padrão de cada
# cidade indica qual delas é mais consistente (menor variação entre clientes)
```

**10.**
```python
df = pd.DataFrame({"loja": ["A","A","A","B","B","B"], "vendedor": ["X","Y","X","Y","X","Y"], "venda": [500,700,550,650,600,720]})
print(df.pivot_table(index="loja", columns="vendedor", values="venda", aggfunc="mean"))

df["faixa_venda"] = pd.cut(df["venda"], bins=2)
print(pd.crosstab(df["faixa_venda"], df["loja"]))
```

</details>

## 7. Amostragem e introdução à inferência

1. Dado (com `np.random.seed(1)`)
   `populacao = pd.Series(np.random.normal(loc=100, scale=15, size=5000))`,
   calcule a média real da população.
2. Usando a mesma `populacao`, retire uma amostra de 50 valores
   (`random_state=1`) e calcule sua média.
3. Calcule o erro padrão da amostra do exercício 2.
4. Calcule o intervalo de confiança aproximado de 95% da amostra do
   exercício 2.
5. Repita os exercícios 2 a 4 com uma amostra de 500 valores
   (`random_state=1`) e compare a largura do intervalo de confiança com o
   da amostra de 50.
6. Dado
   `df = pd.DataFrame({"cliente": range(1, 21), "plano": ["Basico"]*15 + ["Premium"]*5, "gasto": list(range(40, 55)) + [200,210,190,220,205]})`,
   retire uma amostra aleatória simples de 6 linhas (`random_state=2`) e
   verifique quantos clientes Premium ela capturou.
7. Usando o mesmo `df`, faça uma amostragem estratificada por `plano` com
   `frac=0.4` e `random_state=2`, e compare a proporção de Premium na
   amostra com a proporção na população original.
8. Dado (com `np.random.seed(10)`)
   `populacao_precos = pd.Series(np.random.normal(loc=50, scale=10, size=8000))`,
   compare a média de amostras de tamanho 20, 200 e 2000
   (todas com `random_state=5`) com a média real da população.
9. Usando `populacao_precos`, calcule o erro padrão para amostras de tamanho
   20 e 2000, e explique em comentário por que ele diminui com `n` maior.
10. Explique, com um exemplo de código usando `populacao_precos`, por que
    tratar uma amostra pequena (`n=10`, `random_state=3`) como se fosse a
    população inteira pode levar a conclusões erradas sobre a média real.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd
import numpy as np

np.random.seed(1)
populacao = pd.Series(np.random.normal(loc=100, scale=15, size=5000))
print(populacao.mean())  # próxima de 100
```

**2.**
```python
amostra_50 = populacao.sample(n=50, random_state=1)
print(amostra_50.mean())
```

**3.**
```python
erro_padrao_50 = amostra_50.std() / np.sqrt(50)
print(erro_padrao_50)
```

**4.**
```python
margem_50 = 1.96 * erro_padrao_50
media_50 = amostra_50.mean()
print(media_50 - margem_50, media_50 + margem_50)
```

**5.**
```python
amostra_500 = populacao.sample(n=500, random_state=1)
media_500 = amostra_500.mean()
erro_padrao_500 = amostra_500.std() / np.sqrt(500)
margem_500 = 1.96 * erro_padrao_500
print(media_500 - margem_500, media_500 + margem_500)
# o intervalo com n=500 é bem mais estreito que com n=50 -- amostra maior,
# estimativa mais precisa
```

**6.**
```python
df = pd.DataFrame({"cliente": range(1, 21), "plano": ["Basico"]*15 + ["Premium"]*5, "gasto": list(range(40, 55)) + [200,210,190,220,205]})
amostra_simples = df.sample(n=6, random_state=2)
print(amostra_simples)
print((amostra_simples["plano"] == "Premium").sum())
# a amostragem aleatória simples pode capturar poucos ou nenhum Premium por acaso
```

**7.**
```python
amostra_estratificada = df.groupby("plano", group_keys=False).apply(
    lambda grupo: grupo.sample(frac=0.4, random_state=2)
)
print(amostra_estratificada["plano"].value_counts(normalize=True))
print(df["plano"].value_counts(normalize=True))
# a proporção de Premium na amostra estratificada fica igual (ou muito
# próxima) à proporção da população original
```

**8.**
```python
np.random.seed(10)
populacao_precos = pd.Series(np.random.normal(loc=50, scale=10, size=8000))
for n in [20, 200, 2000]:
    amostra = populacao_precos.sample(n=n, random_state=5)
    print(f"n={n}: media={amostra.mean():.2f} (populacao={populacao_precos.mean():.2f})")
```

**9.**
```python
amostra_20 = populacao_precos.sample(n=20, random_state=5)
amostra_2000 = populacao_precos.sample(n=2000, random_state=5)
print(amostra_20.std() / np.sqrt(20))
print(amostra_2000.std() / np.sqrt(2000))
# o erro padrão diminui porque divide o desvio padrão por sqrt(n) -- quanto
# maior a amostra, menor a incerteza sobre onde está a média real
```

**10.**
```python
amostra_10 = populacao_precos.sample(n=10, random_state=3)
print(amostra_10.mean(), populacao_precos.mean())
# com apenas 10 valores, a média da amostra pode se afastar bastante da
# média real da população por puro acaso; tratar essa amostra pequena como
# "a verdade" levaria a uma conclusão sem margem de erro reconhecida,
# quando na prática o erro padrão dela é grande
```

</details>

## 8. Estruturando uma EDA completa

1. Dado
   `df = pd.DataFrame({"pedido": range(1,7), "canal": ["Online","Loja","Online","Loja","Online","Loja"], "valor": [120, 80, 200, 95, 150, 60], "itens": [2, 1, 4, 2, 3, 1]})`,
   faça a visão geral (`shape`, `info`) e a análise univariada de `valor` e
   `itens`.
2. Usando o mesmo `df`, faça a análise univariada de `canal` e calcule a
   correlação entre `valor` e `itens`.
3. Ainda com o mesmo `df`, calcule o valor médio de pedido por `canal` e
   escreva 2 frases de síntese.
4. Dado um novo dataset
   `df = pd.DataFrame({"paciente": range(1,9), "idade": [25,40,60,35,50,29,45,70], "pressao": [12,13,15,12,14,11,13,16], "fumante": ["Nao","Sim","Sim","Nao","Sim","Nao","Nao","Sim"]})`,
   faça a visão geral e a análise univariada de todas as colunas relevantes
   (ignorando `paciente` como ID).
5. Usando o `df` do exercício 4, calcule a correlação entre `idade` e
   `pressao`, e compare a `pressao` média entre fumantes e não fumantes com
   `groupby`.
6. Ainda com o `df` do exercício 4, escreva a síntese completa da EDA (3-4
   frases) juntando os achados dos exercícios 4 e 5.
7. Dado o dataset
   `df = pd.DataFrame({"filme": ["A","B","C","D","E","F","G","H"], "genero": ["Acao","Comedia","Drama","Acao","Comedia","Drama","Acao","Drama"], "nota": [7.5, 6.0, 8.2, 6.8, 5.5, 8.9, 7.0, 7.8], "bilheteria_milhoes": [300, 90, 40, 250, 60, 35, 220, 50]})`,
   execute o roteiro completo de EDA (visão geral, univariada de `nota` e
   `bilheteria_milhoes`, univariada de `genero`, correlação entre `nota` e
   `bilheteria_milhoes`).
8. Usando o `df` do exercício 7, calcule a bilheteria e a nota médias por
   `genero`, e escreva uma síntese respondendo: "filmes de ação faturam mais
   que os outros gêneros, mesmo com notas parecidas?".
9. Dado o dataset
   `df = pd.DataFrame({"funcionario": range(1,11), "area": ["Vendas","TI","Vendas","RH","TI","Vendas","RH","TI","Vendas","RH"], "anos_empresa": [1,5,2,8,3,1,10,4,2,6], "satisfacao": [6,8,5,9,7,4,9,8,5,8]})`,
   execute o roteiro completo de EDA (visão geral, univariada de todas as
   colunas numéricas e categóricas, correlação entre `anos_empresa` e
   `satisfacao`, satisfação média por `area`).
10. Usando o `df` do exercício 9, escreva uma síntese final de 3-4 frases
    que aponte: o principal padrão numérico encontrado, o padrão por grupo
    (`area`) mais relevante, e uma ressalva sobre o tamanho pequeno da
    amostra (10 funcionários).

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import pandas as pd

df = pd.DataFrame({"pedido": range(1,7), "canal": ["Online","Loja","Online","Loja","Online","Loja"], "valor": [120, 80, 200, 95, 150, 60], "itens": [2, 1, 4, 2, 3, 1]})
print(df.shape)
df.info()
print(df["valor"].describe())
print(df["itens"].describe())
```

**2.**
```python
print(df["canal"].value_counts(normalize=True) * 100)
print(df["valor"].corr(df["itens"]))
```

**3.**
```python
print(df.groupby("canal")["valor"].mean())
sintese = """
- Pedidos Online têm valor médio maior que pedidos feitos na Loja física.
- Valor do pedido e quantidade de itens têm correlação positiva forte,
  como esperado (mais itens, maior o valor total).
"""
print(sintese)
```

**4.**
```python
df = pd.DataFrame({"paciente": range(1,9), "idade": [25,40,60,35,50,29,45,70], "pressao": [12,13,15,12,14,11,13,16], "fumante": ["Nao","Sim","Sim","Nao","Sim","Nao","Nao","Sim"]})
print(df.shape)
df.info()
print(df["idade"].describe())
print(df["pressao"].describe())
print(df["fumante"].value_counts(normalize=True) * 100)
```

**5.**
```python
print(df["idade"].corr(df["pressao"]))  # correlação positiva
print(df.groupby("fumante")["pressao"].mean())
```

**6.**
```python
sintese = """
- Idade e pressão têm correlação positiva forte -- pacientes mais velhos
  tendem a ter pressão mais alta nesta amostra.
- Pacientes fumantes apresentam pressão média mais alta que não fumantes.
- Amostra pequena (8 pacientes), então esses padrões são indícios, não
  conclusões definitivas sobre causa e efeito.
"""
print(sintese)
```

**7.**
```python
df = pd.DataFrame({"filme": ["A","B","C","D","E","F","G","H"], "genero": ["Acao","Comedia","Drama","Acao","Comedia","Drama","Acao","Drama"], "nota": [7.5, 6.0, 8.2, 6.8, 5.5, 8.9, 7.0, 7.8], "bilheteria_milhoes": [300, 90, 40, 250, 60, 35, 220, 50]})
print(df.shape)
df.info()
print(df["nota"].describe())
print(df["bilheteria_milhoes"].describe())
print(df["genero"].value_counts(normalize=True) * 100)
print(df["nota"].corr(df["bilheteria_milhoes"]))
```

**8.**
```python
print(df.groupby("genero")[["nota", "bilheteria_milhoes"]].mean())
sintese = """
- Filmes de Ação têm a maior bilheteria média, bem acima de Comédia e
  Drama, mesmo com notas médias competitivas.
- Filmes de Drama têm as notas mais altas em média, mas bilheteria bem
  menor -- sugere que crítica/avaliação não é o principal fator de bilheteria.
"""
print(sintese)
```

**9.**
```python
df = pd.DataFrame({"funcionario": range(1,11), "area": ["Vendas","TI","Vendas","RH","TI","Vendas","RH","TI","Vendas","RH"], "anos_empresa": [1,5,2,8,3,1,10,4,2,6], "satisfacao": [6,8,5,9,7,4,9,8,5,8]})
print(df.shape)
df.info()
print(df["anos_empresa"].describe())
print(df["satisfacao"].describe())
print(df["area"].value_counts(normalize=True) * 100)
print(df["anos_empresa"].corr(df["satisfacao"]))
print(df.groupby("area")["satisfacao"].mean())
```

**10.**
```python
sintese = """
- Anos de empresa e satisfação têm correlação positiva forte -- funcionários
  mais antigos tendem a estar mais satisfeitos nesta amostra.
- A área de RH apresenta a maior satisfação média entre as três áreas,
  enquanto Vendas apresenta a menor.
- Com apenas 10 funcionários na amostra, esses padrões servem como indícios
  iniciais, não como conclusões estatisticamente robustas -- vale coletar
  mais dados antes de embasar decisões importantes neles.
"""
print(sintese)
```

</details>
