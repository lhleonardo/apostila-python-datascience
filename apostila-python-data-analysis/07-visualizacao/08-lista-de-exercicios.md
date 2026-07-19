# Lista de exercícios — Módulo 7

> Módulo 7 — Visualização · Lista de exercícios de revisão

Esta lista reúne 10 exercícios práticos para cada tópico do módulo, para
consolidar o que foi aprendido antes de avançar. Tente resolver cada
exercício sem consultar o tópico original primeiro — as soluções vêm logo
depois de cada bloco, dentro de um "clique para ver".

## 1. Introdução ao Matplotlib

1. Crie uma figura com `fig, ax = plt.subplots()` e desenhe uma linha com
   `x = [1, 2, 3, 4, 5]` e `y = [2, 4, 3, 5, 6]`.
2. No gráfico do item 1, adicione título `"Meu gráfico"`, rótulo `"Dia"` no
   eixo X e `"Valor"` no eixo Y.
3. Desenhe o mesmo gráfico do item 1 usando a forma direta (`plt.plot`, sem
   `ax`) e compare o resultado visual — ele deve ser idêntico.
4. Crie uma figura com `figsize=(10, 4)` e desenhe um gráfico de barras com
   `categorias = ["A", "B", "C"]` e `valores = [10, 25, 15]`.
5. Salve o gráfico do item 4 em um arquivo chamado `grafico_categorias.png`
   com `dpi=150` e `bbox_inches="tight"`.
6. Crie uma figura com `plt.subplots(1, 2, figsize=(10, 4))`: no primeiro
   eixo desenhe uma linha com `y1 = [1, 3, 2, 5, 4]`, no segundo desenhe uma
   barra com `y2 = [4, 2, 6, 3, 5]`, ambos usando `x = [1, 2, 3, 4, 5]`.
7. Adicione `plt.tight_layout()` ao gráfico do item 6 e explique (em
   comentário) por que ela evita sobreposição de títulos.
8. Crie uma figura com `plt.subplots(2, 2, figsize=(8, 6))` (2 linhas, 2
   colunas) e desenhe quatro gráficos de linha diferentes, um em cada eixo,
   usando `dados = [[1, 2, 3], [3, 1, 2], [2, 3, 1], [1, 1, 1]]` (dica: os
   eixos vêm como uma matriz 2x2, acesse com `eixos[0, 0]`, `eixos[0, 1]`
   etc).
9. Crie um gráfico de linha com `x = [0, 1, 2, 3, 4]` e
   `y = [0, 1, 4, 9, 16]`, título `"Quadrados"`, e salve em
   `quadrados.png`, sem chamar `plt.show()` antes de salvar.
10. Explique, em um comentário no código, a diferença entre `fig` e `ax` na
    dupla `fig, ax = plt.subplots()`, e reescreva um gráfico simples de
    barras (`categorias = ["X", "Y"]`, `valores = [7, 3]`) usando a
    abordagem orientada a objetos, com título e rótulos nos dois eixos.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [2, 4, 3, 5, 6]

fig, ax = plt.subplots()
ax.plot(x, y)
plt.show()
```

**2.**
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [2, 4, 3, 5, 6]

fig, ax = plt.subplots()
ax.plot(x, y)
ax.set_title("Meu gráfico")
ax.set_xlabel("Dia")
ax.set_ylabel("Valor")
plt.show()
```

**3.**
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [2, 4, 3, 5, 6]

plt.plot(x, y)
plt.show()
# resultado visual idêntico ao da abordagem orientada a objetos
```

**4.**
```python
import matplotlib.pyplot as plt

categorias = ["A", "B", "C"]
valores = [10, 25, 15]

fig, ax = plt.subplots(figsize=(10, 4))
ax.bar(categorias, valores)
plt.show()
```

**5.**
```python
import matplotlib.pyplot as plt

categorias = ["A", "B", "C"]
valores = [10, 25, 15]

fig, ax = plt.subplots(figsize=(10, 4))
ax.bar(categorias, valores)
fig.savefig("grafico_categorias.png", dpi=150, bbox_inches="tight")
```

**6.**
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y1 = [1, 3, 2, 5, 4]
y2 = [4, 2, 6, 3, 5]

fig, eixos = plt.subplots(1, 2, figsize=(10, 4))
eixos[0].plot(x, y1)
eixos[1].bar(x, y2)
plt.show()
```

**7.**
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y1 = [1, 3, 2, 5, 4]
y2 = [4, 2, 6, 3, 5]

fig, eixos = plt.subplots(1, 2, figsize=(10, 4))
eixos[0].plot(x, y1)
eixos[0].set_title("Linha")
eixos[1].bar(x, y2)
eixos[1].set_title("Barra")
plt.tight_layout()
# tight_layout ajusta o espaçamento entre subplots automaticamente,
# evitando que títulos e rótulos de um eixo se sobreponham ao eixo vizinho
plt.show()
```

**8.**
```python
import matplotlib.pyplot as plt

dados = [[1, 2, 3], [3, 1, 2], [2, 3, 1], [1, 1, 1]]

fig, eixos = plt.subplots(2, 2, figsize=(8, 6))
eixos[0, 0].plot(dados[0])
eixos[0, 1].plot(dados[1])
eixos[1, 0].plot(dados[2])
eixos[1, 1].plot(dados[3])
plt.tight_layout()
plt.show()
```

**9.**
```python
import matplotlib.pyplot as plt

x = [0, 1, 2, 3, 4]
y = [0, 1, 4, 9, 16]

fig, ax = plt.subplots()
ax.plot(x, y)
ax.set_title("Quadrados")
fig.savefig("quadrados.png", dpi=150, bbox_inches="tight")
```

**10.**
```python
import matplotlib.pyplot as plt

# fig controla propriedades da figura inteira (tamanho, salvar em arquivo);
# ax controla o conteúdo do gráfico em si (dados, título, rótulos dos eixos)

categorias = ["X", "Y"]
valores = [7, 3]

fig, ax = plt.subplots()
ax.bar(categorias, valores)
ax.set_title("Comparação X vs Y")
ax.set_xlabel("Categoria")
ax.set_ylabel("Valor")
plt.show()
```

</details>

## 2. Gráficos de linha e barra

1. Com `dias = ["Seg", "Ter", "Qua", "Qui", "Sex"]` e
   `visitantes = [120, 135, 98, 150, 170]`, crie um gráfico de linha com
   `marker="o"`.
2. Com `lojas = ["Norte", "Sul", "Leste", "Oeste"]` e
   `faturamento = [8000, 6500, 9200, 5400]`, crie um gráfico de barra
   vertical com `color="steelblue"`.
3. Refaça o gráfico do item 2 como barra horizontal (`ax.barh`).
4. Com `receita_2024 = [4000, 4500, 4300, 5000]` e
   `receita_2023 = [3800, 4000, 4100, 4600]` para os trimestres
   `["T1", "T2", "T3", "T4"]`, crie um gráfico de linha com as duas séries,
   usando `marker` diferente para cada uma e `ax.legend()`.
5. Ordene `lojas` e `faturamento` (do item 2) da maior para a menor receita
   usando um `pd.DataFrame` e `.sort_values()`, e desenhe o resultado como
   barra horizontal.
6. Com `produtos = ["Mouse", "Teclado", "Monitor", "Headset", "Webcam"]` e
   `unidades = [230, 180, 90, 140, 60]`, crie um gráfico de barra com as
   barras ordenadas da maior para a menor.
7. Crie um `pd.DataFrame` com colunas `mes` e `vendas` a partir de
   `meses = ["Jan", "Fev", "Mar", "Abr"]` e `vendas = [200, 220, 180, 260]`,
   e gere o gráfico de linha diretamente com `df.plot(x="mes", y="vendas",
   kind="line", marker="o")`.
8. Com `canais = ["Site", "App", "Loja física", "Telefone"]` e
   `pedidos = [500, 620, 310, 90]`, decida (e justifique em um comentário)
   se o gráfico mais adequado é linha ou barra, e implemente-o.
9. Com `semanas = [1, 2, 3, 4, 5, 6]`, `vendas_produto_x = [50, 65, 60, 80,
   75, 90]` e `vendas_produto_y = [40, 42, 55, 50, 60, 58]`, crie um
   gráfico de linha comparando os dois produtos, com título, rótulos nos
   eixos e legenda.
10. Combine em uma única figura com dois subplots lado a lado: à esquerda, o
    gráfico de linha do item 9; à direita, um gráfico de barra comparando o
    total vendido de cada produto (some as listas do item 9 com `sum()`).

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import matplotlib.pyplot as plt

dias = ["Seg", "Ter", "Qua", "Qui", "Sex"]
visitantes = [120, 135, 98, 150, 170]

fig, ax = plt.subplots()
ax.plot(dias, visitantes, marker="o")
ax.set_title("Visitantes por dia")
plt.show()
```

**2.**
```python
import matplotlib.pyplot as plt

lojas = ["Norte", "Sul", "Leste", "Oeste"]
faturamento = [8000, 6500, 9200, 5400]

fig, ax = plt.subplots()
ax.bar(lojas, faturamento, color="steelblue")
ax.set_title("Faturamento por loja")
plt.show()
```

**3.**
```python
import matplotlib.pyplot as plt

lojas = ["Norte", "Sul", "Leste", "Oeste"]
faturamento = [8000, 6500, 9200, 5400]

fig, ax = plt.subplots()
ax.barh(lojas, faturamento, color="steelblue")
ax.set_title("Faturamento por loja (horizontal)")
plt.show()
```

**4.**
```python
import matplotlib.pyplot as plt

trimestres = ["T1", "T2", "T3", "T4"]
receita_2024 = [4000, 4500, 4300, 5000]
receita_2023 = [3800, 4000, 4100, 4600]

fig, ax = plt.subplots()
ax.plot(trimestres, receita_2024, marker="o", label="2024")
ax.plot(trimestres, receita_2023, marker="s", label="2023")
ax.set_title("Receita por trimestre")
ax.legend()
plt.show()
```

**5.**
```python
import matplotlib.pyplot as plt
import pandas as pd

lojas = ["Norte", "Sul", "Leste", "Oeste"]
faturamento = [8000, 6500, 9200, 5400]

df = pd.DataFrame({"loja": lojas, "faturamento": faturamento}).sort_values("faturamento")

fig, ax = plt.subplots()
ax.barh(df["loja"], df["faturamento"], color="steelblue")
ax.set_title("Faturamento por loja (ordenado)")
plt.show()
```

**6.**
```python
import matplotlib.pyplot as plt
import pandas as pd

produtos = ["Mouse", "Teclado", "Monitor", "Headset", "Webcam"]
unidades = [230, 180, 90, 140, 60]

df = pd.DataFrame({"produto": produtos, "unidades": unidades}).sort_values(
    "unidades", ascending=False
)

fig, ax = plt.subplots()
ax.bar(df["produto"], df["unidades"], color="steelblue")
ax.set_title("Unidades vendidas por produto (ordenado)")
plt.show()
```

**7.**
```python
import matplotlib.pyplot as plt
import pandas as pd

meses = ["Jan", "Fev", "Mar", "Abr"]
vendas = [200, 220, 180, 260]

df = pd.DataFrame({"mes": meses, "vendas": vendas})
df.plot(x="mes", y="vendas", kind="line", marker="o", title="Vendas mensais")
plt.show()
```

**8.**
```python
import matplotlib.pyplot as plt

# canais são categorias sem ordem temporal natural -> barra é o mais adequado
canais = ["Site", "App", "Loja física", "Telefone"]
pedidos = [500, 620, 310, 90]

fig, ax = plt.subplots()
ax.bar(canais, pedidos, color="steelblue")
ax.set_title("Pedidos por canal")
plt.show()
```

**9.**
```python
import matplotlib.pyplot as plt

semanas = [1, 2, 3, 4, 5, 6]
vendas_produto_x = [50, 65, 60, 80, 75, 90]
vendas_produto_y = [40, 42, 55, 50, 60, 58]

fig, ax = plt.subplots()
ax.plot(semanas, vendas_produto_x, marker="o", label="Produto X")
ax.plot(semanas, vendas_produto_y, marker="s", label="Produto Y")
ax.set_title("Vendas semanais: Produto X vs Produto Y")
ax.set_xlabel("Semana")
ax.set_ylabel("Unidades vendidas")
ax.legend()
plt.show()
```

**10.**
```python
import matplotlib.pyplot as plt

semanas = [1, 2, 3, 4, 5, 6]
vendas_produto_x = [50, 65, 60, 80, 75, 90]
vendas_produto_y = [40, 42, 55, 50, 60, 58]

fig, eixos = plt.subplots(1, 2, figsize=(10, 4))

eixos[0].plot(semanas, vendas_produto_x, marker="o", label="Produto X")
eixos[0].plot(semanas, vendas_produto_y, marker="s", label="Produto Y")
eixos[0].set_title("Vendas por semana")
eixos[0].legend()

eixos[1].bar(
    ["Produto X", "Produto Y"],
    [sum(vendas_produto_x), sum(vendas_produto_y)],
    color="steelblue",
)
eixos[1].set_title("Total vendido")

plt.tight_layout()
plt.show()
```

</details>

## 3. Histogramas e boxplots

1. Com `np.random.seed(10)` e `dados = np.random.normal(50, 10, 300)`, crie
   um histograma com `bins=20`.
2. Refaça o histograma do item 1 testando três valores de `bins` (`5`, `20`,
   `50`) em subplots lado a lado, usando `plt.subplots(1, 3, figsize=(12,
   4))`.
3. Com `np.random.seed(11)` e `notas = np.random.normal(7, 1.5, 200)`, crie
   um boxplot único com `ax.boxplot(notas)`.
4. Com `np.random.seed(12)`, `salario_ti = np.random.normal(6000, 1500,
   100)` e `salario_rh = np.random.normal(4500, 800, 100)`, crie um boxplot
   comparando as duas distribuições lado a lado, com `labels`.
5. Com `np.random.seed(13)` e
   `precos = np.concatenate([np.random.normal(50, 8, 150),
   np.random.normal(150, 20, 20)])`, crie um histograma com `bins=25` e, em
   um comentário, aponte se a distribuição parece ter uma cauda longa.
6. Usando os mesmos `precos` do item 5, crie um boxplot e verifique
   (comentário) se os valores mais altos aparecem como outliers.
7. Com `np.random.seed(14)`, crie um `pd.DataFrame` com colunas `turno`
   (`["Manhã"] * 80 + ["Tarde"] * 80 + ["Noite"] * 80`) e `producao`
   (`np.random.normal(100, 15, 240)` para todos, mas some `20` aos valores
   de `"Noite"` para simular turno mais produtivo). Crie um boxplot de
   `producao` agrupado por `turno` usando `df.boxplot(column=..., by=...)`.
8. Com `np.random.seed(15)` e `idade_clientes = np.random.normal(35, 12,
   400)`, crie um histograma de `idade_clientes` com `bins=30`,
   `color="seagreen"` e `edgecolor="white"`, título e rótulos nos eixos.
9. Com `np.random.seed(16)`, `tempo_entrega_sp = np.random.normal(3, 0.5,
   120)` e `tempo_entrega_rj = np.random.normal(3, 2, 120)` (dias), crie um
   boxplot comparando as duas cidades e escreva (comentário) qual delas tem
   entrega mais previsível.
10. Com `np.random.seed(17)` e `avaliacoes = np.random.uniform(1, 5, 500)`,
    crie uma figura com dois subplots lado a lado: um histograma com
    `bins=15` à esquerda e um boxplot à direita, ambos usando os mesmos
    dados, e compare (comentário) o que cada um revela sobre a distribuição.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(10)
dados = np.random.normal(50, 10, 300)

fig, ax = plt.subplots()
ax.hist(dados, bins=20, color="steelblue", edgecolor="white")
plt.show()
```

**2.**
```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(10)
dados = np.random.normal(50, 10, 300)

fig, eixos = plt.subplots(1, 3, figsize=(12, 4))
for ax, bins in zip(eixos, [5, 20, 50]):
    ax.hist(dados, bins=bins, color="steelblue", edgecolor="white")
    ax.set_title(f"bins={bins}")
plt.tight_layout()
plt.show()
```

**3.**
```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(11)
notas = np.random.normal(7, 1.5, 200)

fig, ax = plt.subplots()
ax.boxplot(notas)
ax.set_title("Distribuição de notas")
plt.show()
```

**4.**
```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(12)
salario_ti = np.random.normal(6000, 1500, 100)
salario_rh = np.random.normal(4500, 800, 100)

fig, ax = plt.subplots()
ax.boxplot([salario_ti, salario_rh], labels=["TI", "RH"])
ax.set_title("Salário por área")
plt.show()
```

**5.**
```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(13)
precos = np.concatenate([np.random.normal(50, 8, 150), np.random.normal(150, 20, 20)])

fig, ax = plt.subplots()
ax.hist(precos, bins=25, color="steelblue", edgecolor="white")
ax.set_title("Distribuição de preços")
plt.show()
# a distribuição tem uma cauda longa à direita, causada pelo pequeno grupo
# de preços em torno de 150
```

**6.**
```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(13)
precos = np.concatenate([np.random.normal(50, 8, 150), np.random.normal(150, 20, 20)])

fig, ax = plt.subplots()
ax.boxplot(precos)
ax.set_title("Boxplot de preços")
plt.show()
# sim, os valores mais altos aparecem como pontos isolados acima do bigode
# superior, sinalizando outliers estatísticos
```

**7.**
```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

np.random.seed(14)
df = pd.DataFrame({
    "turno": ["Manhã"] * 80 + ["Tarde"] * 80 + ["Noite"] * 80,
    "producao": np.random.normal(100, 15, 240),
})
df.loc[df["turno"] == "Noite", "producao"] += 20

fig, ax = plt.subplots()
df.boxplot(column="producao", by="turno", ax=ax)
ax.set_title("Produção por turno")
plt.suptitle("")
plt.show()
```

**8.**
```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(15)
idade_clientes = np.random.normal(35, 12, 400)

fig, ax = plt.subplots()
ax.hist(idade_clientes, bins=30, color="seagreen", edgecolor="white")
ax.set_title("Distribuição de idade dos clientes")
ax.set_xlabel("Idade")
ax.set_ylabel("Frequência")
plt.show()
```

**9.**
```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(16)
tempo_entrega_sp = np.random.normal(3, 0.5, 120)
tempo_entrega_rj = np.random.normal(3, 2, 120)

fig, ax = plt.subplots()
ax.boxplot([tempo_entrega_sp, tempo_entrega_rj], labels=["São Paulo", "Rio de Janeiro"])
ax.set_title("Tempo de entrega por cidade")
ax.set_ylabel("Dias")
plt.show()
# São Paulo tem entrega mais previsível: caixa e bigodes bem mais estreitos,
# mesmo com média parecida à do Rio de Janeiro
```

**10.**
```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(17)
avaliacoes = np.random.uniform(1, 5, 500)

fig, eixos = plt.subplots(1, 2, figsize=(10, 4))
eixos[0].hist(avaliacoes, bins=15, color="steelblue", edgecolor="white")
eixos[0].set_title("Histograma")
eixos[1].boxplot(avaliacoes)
eixos[1].set_title("Boxplot")
plt.tight_layout()
plt.show()
# o histograma mostra a forma completa da distribuição (achatada, uniforme
# entre 1 e 5); o boxplot resume isso em quartis, sem revelar o formato
# retangular característico da distribuição uniforme
```

</details>

## 4. Scatter plots e relação entre variáveis

1. Com `np.random.seed(20)`, `horas_sono = np.random.uniform(4, 10, 60)` e
   `produtividade = horas_sono * 5 + np.random.normal(0, 5, 60)`, crie um
   scatter plot com `alpha=0.7`.
2. Adicione título e rótulos nos eixos ao gráfico do item 1.
3. Com `np.random.seed(21)`, `idade = np.random.uniform(18, 70, 80)` e
   `gasto_mensal = np.random.uniform(100, 2000, 80)`, mais
   `plano = np.random.choice(["Básico", "Premium"], size=80)`, crie um
   scatter plot de `idade` (x) por `gasto_mensal` (y), colorido por `plano`,
   com legenda.
4. Com os dados do item 1, adicione uma linha de tendência linear com
   `np.polyfit(horas_sono, produtividade, deg=1)`.
5. Com `np.random.seed(22)`, `investimento_ads = np.random.uniform(500,
   5000, 50)`, `conversoes = np.random.uniform(10, 300, 50)` e
   `alcance = np.random.uniform(1000, 50000, 50)`, crie um scatter plot de
   `investimento_ads` (x) por `conversoes` (y) com o tamanho dos pontos
   (`s`) proporcional a `alcance / 200`.
6. Com `np.random.seed(23)`, `x_u = np.linspace(-10, 10, 150)` e
   `y_u = x_u ** 2 + np.random.normal(0, 8, 150)`, crie um scatter plot e
   calcule `np.corrcoef(x_u, y_u)[0, 1]`; comente (no código) por que esse
   número pode enganar apesar do padrão visual em "U" ser claro.
7. Com `np.random.seed(24)`, `preco = np.random.uniform(10, 500, 100)` e
   `quantidade_vendida = 1000 / preco + np.random.normal(0, 3, 100)`, crie
   um scatter plot e avalie visualmente (comentário) se a relação parece
   linear ou não-linear.
8. Usando os dados do item 3, crie a mesma visualização mas separando os
   dois planos em subplots distintos lado a lado (em vez de cor), com o
   mesmo eixo X e Y em ambos para facilitar a comparação.
9. Com `np.random.seed(25)`, `anos_experiencia = np.random.uniform(0, 20,
   90)`, `salario = 3000 + anos_experiencia * 400 + np.random.normal(0, 800,
   90)` e `area = np.random.choice(["Dados", "Backend", "Design"],
   size=90)`, crie um scatter plot colorido por `area` com legenda, mais uma
   linha de tendência calculada sobre todos os pontos (ignorando a
   separação por área).
10. Com os dados do item 9, calcule a correlação entre `anos_experiencia` e
    `salario` com `np.corrcoef`, e escreva (comentário) se o valor obtido é
    coerente com o padrão visual do scatter plot.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(20)
horas_sono = np.random.uniform(4, 10, 60)
produtividade = horas_sono * 5 + np.random.normal(0, 5, 60)

fig, ax = plt.subplots()
ax.scatter(horas_sono, produtividade, alpha=0.7)
plt.show()
```

**2.**
```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(20)
horas_sono = np.random.uniform(4, 10, 60)
produtividade = horas_sono * 5 + np.random.normal(0, 5, 60)

fig, ax = plt.subplots()
ax.scatter(horas_sono, produtividade, alpha=0.7)
ax.set_title("Horas de sono x Produtividade")
ax.set_xlabel("Horas de sono")
ax.set_ylabel("Produtividade")
plt.show()
```

**3.**
```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

np.random.seed(21)
idade = np.random.uniform(18, 70, 80)
gasto_mensal = np.random.uniform(100, 2000, 80)
plano = np.random.choice(["Básico", "Premium"], size=80)

df = pd.DataFrame({"idade": idade, "gasto_mensal": gasto_mensal, "plano": plano})

fig, ax = plt.subplots()
for p, cor in [("Básico", "steelblue"), ("Premium", "orange")]:
    subset = df[df["plano"] == p]
    ax.scatter(subset["idade"], subset["gasto_mensal"], label=p, alpha=0.7, color=cor)
ax.set_title("Idade x Gasto mensal, por plano")
ax.legend()
plt.show()
```

**4.**
```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(20)
horas_sono = np.random.uniform(4, 10, 60)
produtividade = horas_sono * 5 + np.random.normal(0, 5, 60)

coeficientes = np.polyfit(horas_sono, produtividade, deg=1)
linha_tendencia = np.poly1d(coeficientes)
x_ordenado = np.sort(horas_sono)

fig, ax = plt.subplots()
ax.scatter(horas_sono, produtividade, alpha=0.6, color="steelblue")
ax.plot(x_ordenado, linha_tendencia(x_ordenado), color="red", linewidth=2)
plt.show()
```

**5.**
```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(22)
investimento_ads = np.random.uniform(500, 5000, 50)
conversoes = np.random.uniform(10, 300, 50)
alcance = np.random.uniform(1000, 50000, 50)

fig, ax = plt.subplots()
ax.scatter(investimento_ads, conversoes, s=alcance / 200, alpha=0.5, color="steelblue")
ax.set_title("Investimento x Conversões (tamanho = alcance)")
plt.show()
```

**6.**
```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(23)
x_u = np.linspace(-10, 10, 150)
y_u = x_u ** 2 + np.random.normal(0, 8, 150)

fig, ax = plt.subplots()
ax.scatter(x_u, y_u, alpha=0.6, color="steelblue")
plt.show()

print(np.corrcoef(x_u, y_u)[0, 1])
# a correlação de Pearson mede relação LINEAR; como a relação aqui é
# quadrática (em U), o coeficiente fica perto de 0 mesmo com um padrão
# visual claríssimo entre as variáveis
```

**7.**
```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(24)
preco = np.random.uniform(10, 500, 100)
quantidade_vendida = 1000 / preco + np.random.normal(0, 3, 100)

fig, ax = plt.subplots()
ax.scatter(preco, quantidade_vendida, alpha=0.6, color="steelblue")
ax.set_title("Preço x Quantidade vendida")
plt.show()
# a relação parece não-linear: a curva decai rapidamente em preços baixos e
# se achata em preços altos, típico de uma relação do tipo 1/x
```

**8.**
```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

np.random.seed(21)
idade = np.random.uniform(18, 70, 80)
gasto_mensal = np.random.uniform(100, 2000, 80)
plano = np.random.choice(["Básico", "Premium"], size=80)

df = pd.DataFrame({"idade": idade, "gasto_mensal": gasto_mensal, "plano": plano})

fig, eixos = plt.subplots(1, 2, figsize=(10, 4), sharex=True, sharey=True)
for ax, p in zip(eixos, ["Básico", "Premium"]):
    subset = df[df["plano"] == p]
    ax.scatter(subset["idade"], subset["gasto_mensal"], alpha=0.7, color="steelblue")
    ax.set_title(p)
plt.tight_layout()
plt.show()
```

**9.**
```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

np.random.seed(25)
anos_experiencia = np.random.uniform(0, 20, 90)
salario = 3000 + anos_experiencia * 400 + np.random.normal(0, 800, 90)
area = np.random.choice(["Dados", "Backend", "Design"], size=90)

df = pd.DataFrame({"anos_experiencia": anos_experiencia, "salario": salario, "area": area})

fig, ax = plt.subplots()
for a, cor in [("Dados", "steelblue"), ("Backend", "orange"), ("Design", "seagreen")]:
    subset = df[df["area"] == a]
    ax.scatter(subset["anos_experiencia"], subset["salario"], label=a, alpha=0.7, color=cor)

coeficientes = np.polyfit(anos_experiencia, salario, deg=1)
linha_tendencia = np.poly1d(coeficientes)
x_ordenado = np.sort(anos_experiencia)
ax.plot(x_ordenado, linha_tendencia(x_ordenado), color="red", linewidth=2, label="Tendência")

ax.set_title("Experiência x Salário, por área")
ax.legend()
plt.show()
```

**10.**
```python
import numpy as np

np.random.seed(25)
anos_experiencia = np.random.uniform(0, 20, 90)
salario = 3000 + anos_experiencia * 400 + np.random.normal(0, 800, 90)

print(np.corrcoef(anos_experiencia, salario)[0, 1])
# o valor deve ficar forte e positivo (perto de 0.9), coerente com o padrão
# visual ascendente e aproximadamente linear observado no scatter plot
```

</details>

## 5. Customização de gráficos

1. Com `meses = ["Jan", "Fev", "Mar", "Abr", "Mai"]` e
   `custos = [8000, 8500, 7900, 9200, 9800]`, crie um gráfico de linha com
   `figsize=(8, 5)`, `color="#2b6cb0"` e `linewidth=2`.
2. No gráfico do item 1, adicione título em negrito com `fontsize=14`.
3. Adicione uma grade sutil (`ax.grid(True, alpha=0.3)`) ao gráfico do item
   1.
4. Com `regioes = ["Norte", "Sul", "Leste", "Oeste"]` e
   `vendas = [4000, 6200, 5100, 3900]`, crie um gráfico de barra com uma
   lista de 4 cores fixas diferentes, uma para cada barra.
5. No gráfico do item 4, remova as bordas superior e direita
   (`ax.spines["top"]` e `ax.spines["right"]`).
6. No gráfico do item 1, use `ax.annotate()` para destacar o mês de maior
   custo (`"Mai"`) com uma seta e o texto `"Pico de custos"`.
7. No gráfico do item 4, formate os rótulos do eixo Y para aparecerem como
   moeda (`"R$ 4.000"` em vez de `4000`), usando `ax.set_yticks` e
   `ax.set_yticklabels`.
8. Crie dois gráficos de barra separados (em figuras diferentes) para
   `categorias = ["Norte", "Sul"]` com os mesmos valores
   `valores = [100, 200]`, mas usando a mesma cor fixa (`"#805ad5"`) nos
   dois, para simular consistência de cor entre gráficos de um relatório.
9. Com `plt.style.use("seaborn-v0_8-whitegrid")`, redesenhe o gráfico do
   item 1 e depois volte ao estilo padrão com `plt.style.use("default")`.
10. Combine em um único gráfico de barra (dados do item 4): `figsize=(9,
    5)`, cores fixas por categoria, título em negrito, grade horizontal
    sutil, remoção das bordas superior/direita e uma anotação destacando a
    região de maior venda.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import matplotlib.pyplot as plt

meses = ["Jan", "Fev", "Mar", "Abr", "Mai"]
custos = [8000, 8500, 7900, 9200, 9800]

fig, ax = plt.subplots(figsize=(8, 5))
ax.plot(meses, custos, color="#2b6cb0", linewidth=2)
plt.show()
```

**2.**
```python
import matplotlib.pyplot as plt

meses = ["Jan", "Fev", "Mar", "Abr", "Mai"]
custos = [8000, 8500, 7900, 9200, 9800]

fig, ax = plt.subplots(figsize=(8, 5))
ax.plot(meses, custos, color="#2b6cb0", linewidth=2)
ax.set_title("Custos mensais", fontsize=14, fontweight="bold")
plt.show()
```

**3.**
```python
import matplotlib.pyplot as plt

meses = ["Jan", "Fev", "Mar", "Abr", "Mai"]
custos = [8000, 8500, 7900, 9200, 9800]

fig, ax = plt.subplots(figsize=(8, 5))
ax.plot(meses, custos, color="#2b6cb0", linewidth=2)
ax.grid(True, alpha=0.3)
plt.show()
```

**4.**
```python
import matplotlib.pyplot as plt

regioes = ["Norte", "Sul", "Leste", "Oeste"]
vendas = [4000, 6200, 5100, 3900]
cores = ["#2b6cb0", "#dd6b20", "#38a169", "#805ad5"]

fig, ax = plt.subplots()
ax.bar(regioes, vendas, color=cores)
plt.show()
```

**5.**
```python
import matplotlib.pyplot as plt

regioes = ["Norte", "Sul", "Leste", "Oeste"]
vendas = [4000, 6200, 5100, 3900]
cores = ["#2b6cb0", "#dd6b20", "#38a169", "#805ad5"]

fig, ax = plt.subplots()
ax.bar(regioes, vendas, color=cores)
ax.spines["top"].set_visible(False)
ax.spines["right"].set_visible(False)
plt.show()
```

**6.**
```python
import matplotlib.pyplot as plt

meses = ["Jan", "Fev", "Mar", "Abr", "Mai"]
custos = [8000, 8500, 7900, 9200, 9800]

fig, ax = plt.subplots(figsize=(8, 5))
ax.plot(meses, custos, color="#2b6cb0", linewidth=2)
ax.annotate(
    "Pico de custos",
    xy=(4, 9800),
    xytext=(2.5, 9500),
    arrowprops=dict(arrowstyle="->", color="gray"),
)
plt.show()
```

**7.**
```python
import matplotlib.pyplot as plt

regioes = ["Norte", "Sul", "Leste", "Oeste"]
vendas = [4000, 6200, 5100, 3900]
cores = ["#2b6cb0", "#dd6b20", "#38a169", "#805ad5"]

fig, ax = plt.subplots()
ax.bar(regioes, vendas, color=cores)
ax.set_yticks([4000, 5000, 6000])
ax.set_yticklabels([f"R$ {v:,.0f}".replace(",", ".") for v in ax.get_yticks()])
plt.show()
```

**8.**
```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots()
ax.bar(["Norte", "Sul"], [100, 200], color="#805ad5")
ax.set_title("Relatório A")
plt.show()

fig, ax = plt.subplots()
ax.bar(["Norte", "Sul"], [100, 200], color="#805ad5")
ax.set_title("Relatório B")
plt.show()
# a mesma cor fixa em ambos os gráficos garante consistência visual entre
# relatórios diferentes
```

**9.**
```python
import matplotlib.pyplot as plt

meses = ["Jan", "Fev", "Mar", "Abr", "Mai"]
custos = [8000, 8500, 7900, 9200, 9800]

plt.style.use("seaborn-v0_8-whitegrid")
fig, ax = plt.subplots(figsize=(8, 5))
ax.plot(meses, custos, linewidth=2)
ax.set_title("Custos mensais (com estilo)")
plt.show()
plt.style.use("default")
```

**10.**
```python
import matplotlib.pyplot as plt

regioes = ["Norte", "Sul", "Leste", "Oeste"]
vendas = [4000, 6200, 5100, 3900]
cores = ["#2b6cb0", "#dd6b20", "#38a169", "#805ad5"]

fig, ax = plt.subplots(figsize=(9, 5))
ax.bar(regioes, vendas, color=cores)
ax.set_title("Vendas por região", fontweight="bold")
ax.grid(True, axis="y", alpha=0.3)
ax.spines["top"].set_visible(False)
ax.spines["right"].set_visible(False)
ax.annotate(
    "Maior venda",
    xy=(1, 6200),
    xytext=(1.3, 6700),
    arrowprops=dict(arrowstyle="->", color="gray"),
)
plt.show()
```

</details>

## 6. Introdução ao Seaborn

1. Com `np.random.seed(30)` e um `pd.DataFrame` contendo
   `idade = np.random.normal(30, 8, 250)`, crie um `sns.histplot(data=df,
   x="idade", bins=25)`.
2. Com `np.random.seed(31)`, crie um `pd.DataFrame` com `cidade =
   np.random.choice(["SP", "RJ", "BH"], size=180)` e
   `renda = np.random.normal(4000, 1200, 180)`, e desenhe um
   `sns.histplot(data=df, x="renda", hue="cidade", bins=20)`.
3. Usando o `df` do item 2, crie um `sns.boxplot(data=df, x="cidade",
   y="renda")`.
4. Com `np.random.seed(32)`, crie um `pd.DataFrame` com `horas_estudo =
   np.random.uniform(0, 10, 100)`, `nota = horas_estudo * 6 +
   np.random.normal(0, 5, 100)` e `curso = np.random.choice(["Exatas",
   "Humanas"], size=100)`, e desenhe um `sns.scatterplot(data=df,
   x="horas_estudo", y="nota", hue="curso", alpha=0.6)`.
5. Usando o `df` do item 2, crie um `sns.barplot(data=df, x="cidade",
   y="renda", errorbar="sd")`, mostrando a renda média por cidade com
   desvio padrão.
6. Com `np.random.seed(33)`, crie um `pd.DataFrame` com três colunas
   numéricas (`preco`, `custo`, `lucro`, cada uma com `np.random.uniform`
   em faixas plausíveis, 150 linhas), calcule `.corr()` e desenhe um
   `sns.heatmap(..., annot=True, cmap="coolwarm", vmin=-1, vmax=1)`.
7. Usando o `df` do item 6, crie um `sns.pairplot(df)`.
8. Com `np.random.seed(34)`, crie um `pd.DataFrame` com `departamento =
   np.random.choice(["Vendas", "Suporte", "TI"], size=200)` e `satisfacao =
   np.random.uniform(1, 10, 200)`, e desenhe, lado a lado (usando `plt.
   subplots` com `ax=ax` passado para o Seaborn), um `sns.boxplot` e um
   `sns.histplot` com `hue="departamento"`.
9. Explique em um comentário a diferença entre usar `sns.barplot` (que
   calcula a média) e usar `df.groupby("cidade")["renda"].sum()` seguido de
   um gráfico de barra do Pandas, usando o `df` do item 2 como exemplo, e
   implemente as duas versões.
10. Com `np.random.seed(35)`, crie um `pd.DataFrame` com `plano =
    np.random.choice(["Free", "Pro", "Enterprise"], size=300)`,
    `uso_mensal_gb = np.random.exponential(5, 300)` e `nota_suporte =
    np.random.uniform(1, 5, 300)`. Aplique `sns.set_theme(style=
    "whitegrid")` e crie uma figura com `sns.boxplot(data=df, x="plano",
    y="uso_mensal_gb")` e título.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

np.random.seed(30)
df = pd.DataFrame({"idade": np.random.normal(30, 8, 250)})

sns.histplot(data=df, x="idade", bins=25)
plt.show()
```

**2.**
```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

np.random.seed(31)
df = pd.DataFrame({
    "cidade": np.random.choice(["SP", "RJ", "BH"], size=180),
    "renda": np.random.normal(4000, 1200, 180),
})

sns.histplot(data=df, x="renda", hue="cidade", bins=20)
plt.show()
```

**3.**
```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

np.random.seed(31)
df = pd.DataFrame({
    "cidade": np.random.choice(["SP", "RJ", "BH"], size=180),
    "renda": np.random.normal(4000, 1200, 180),
})

sns.boxplot(data=df, x="cidade", y="renda")
plt.show()
```

**4.**
```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

np.random.seed(32)
horas_estudo = np.random.uniform(0, 10, 100)
df = pd.DataFrame({
    "horas_estudo": horas_estudo,
    "nota": horas_estudo * 6 + np.random.normal(0, 5, 100),
    "curso": np.random.choice(["Exatas", "Humanas"], size=100),
})

sns.scatterplot(data=df, x="horas_estudo", y="nota", hue="curso", alpha=0.6)
plt.show()
```

**5.**
```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

np.random.seed(31)
df = pd.DataFrame({
    "cidade": np.random.choice(["SP", "RJ", "BH"], size=180),
    "renda": np.random.normal(4000, 1200, 180),
})

sns.barplot(data=df, x="cidade", y="renda", errorbar="sd")
plt.show()
```

**6.**
```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

np.random.seed(33)
df = pd.DataFrame({
    "preco": np.random.uniform(20, 200, 150),
    "custo": np.random.uniform(10, 120, 150),
    "lucro": np.random.uniform(5, 80, 150),
})

matriz = df.corr()
sns.heatmap(matriz, annot=True, cmap="coolwarm", vmin=-1, vmax=1)
plt.show()
```

**7.**
```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

np.random.seed(33)
df = pd.DataFrame({
    "preco": np.random.uniform(20, 200, 150),
    "custo": np.random.uniform(10, 120, 150),
    "lucro": np.random.uniform(5, 80, 150),
})

sns.pairplot(df)
plt.show()
```

**8.**
```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

np.random.seed(34)
df = pd.DataFrame({
    "departamento": np.random.choice(["Vendas", "Suporte", "TI"], size=200),
    "satisfacao": np.random.uniform(1, 10, 200),
})

fig, eixos = plt.subplots(1, 2, figsize=(11, 4))
sns.boxplot(data=df, x="departamento", y="satisfacao", ax=eixos[0])
sns.histplot(data=df, x="satisfacao", hue="departamento", ax=eixos[1])
plt.tight_layout()
plt.show()
```

**9.**
```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

np.random.seed(31)
df = pd.DataFrame({
    "cidade": np.random.choice(["SP", "RJ", "BH"], size=180),
    "renda": np.random.normal(4000, 1200, 180),
})

# sns.barplot calcula a MÉDIA de renda por cidade
sns.barplot(data=df, x="cidade", y="renda")
plt.title("Renda média por cidade (Seaborn)")
plt.show()

# groupby + sum calcula o TOTAL de renda por cidade -- resultado bem
# diferente do barplot padrão, mesmo usando os mesmos dados
soma_por_cidade = df.groupby("cidade")["renda"].sum()
soma_por_cidade.plot(kind="bar", title="Renda total por cidade (Pandas)")
plt.show()
```

**10.**
```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

np.random.seed(35)
df = pd.DataFrame({
    "plano": np.random.choice(["Free", "Pro", "Enterprise"], size=300),
    "uso_mensal_gb": np.random.exponential(5, 300),
    "nota_suporte": np.random.uniform(1, 5, 300),
})

sns.set_theme(style="whitegrid")
sns.boxplot(data=df, x="plano", y="uso_mensal_gb")
plt.title("Uso mensal (GB) por plano")
plt.show()
```

</details>

## 7. Escolhendo o gráfico certo

Para cada exercício, escolha o tipo de gráfico mais adequado à pergunta,
**justifique em uma frase (comentário no código)** e implemente com os
dados fornecidos.

1. "Como o número de assinantes cresceu nos últimos 12 meses?" — use
   `meses = [f"M{i}" for i in range(1, 13)]` e
   `assinantes = np.cumsum(np.random.uniform(50, 300, 12)) + 1000`
   (`np.random.seed(40)`).
2. "Qual a distribuição do tempo de sessão dos usuários no app (em
   minutos)?" — use `np.random.seed(41)` e
   `tempo_sessao = np.random.exponential(8, 500)`.
3. "Existe relação entre o número de e-mails de marketing enviados e a
   taxa de cancelamento (churn)?" — use `np.random.seed(42)`,
   `emails_enviados = np.random.uniform(0, 20, 70)` e
   `churn = emails_enviados * 0.3 + np.random.normal(0, 2, 70)`.
4. "Como o ticket médio varia entre as 4 categorias de plano da
   assinatura?" — use `np.random.seed(43)`, `plano =
   np.random.choice(["Bronze", "Prata", "Ouro", "Platina"], size=200)` e
   `ticket = np.random.uniform(20, 400, 200)`.
5. "Quais métricas do produto (sessões, cliques, conversões, tempo_medio)
   parecem mais correlacionadas entre si?" — gere um `pd.DataFrame` com
   essas 4 colunas numéricas usando `np.random.seed(44)` e
   `np.random.uniform` em faixas plausíveis (150 linhas).
6. "Qual a proporção de clientes por região e por tipo de plano
   (combinando as duas categorias)?" — use `np.random.seed(45)`,
   `regiao = np.random.choice(["Norte", "Sul", "Sudeste"], size=300)` e
   `plano = np.random.choice(["Free", "Pago"], size=300)`; monte um
   `pd.crosstab` e desenhe o gráfico adequado.
7. "A distribuição de nota de satisfação difere entre clientes que usam
   suporte por chat e por telefone?" — use `np.random.seed(46)`,
   `canal_suporte = np.random.choice(["Chat", "Telefone"], size=160)` e
   `nota = np.random.uniform(1, 10, 160)` (some `1.5` às notas de quem usa
   `"Chat"` para simular uma diferença real).
8. "Como o preço de um produto se relaciona com a quantidade vendida, e
   essa relação muda entre as categorias 'Eletrônicos' e 'Papelaria'?" —
   use `np.random.seed(47)`, `preco = np.random.uniform(5, 500, 120)`,
   `quantidade = 2000 / preco + np.random.normal(0, 5, 120)` e
   `categoria = np.random.choice(["Eletrônicos", "Papelaria"], size=120)`.
9. Pegue o gráfico produzido no item 4 e aplique o checklist de qualidade
   do tópico (título, rótulos com unidade, cores consistentes, ausência de
   poluição visual), reescrevendo-o com essas melhorias.
10. Explique, em comentários, por que um gráfico de pizza **não** seria
    adequado para a pergunta do item 4 (4 categorias, mas seria pior com
    mais), e por que um gráfico 3D não ajudaria a responder a pergunta do
    item 3.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import matplotlib.pyplot as plt
import numpy as np

# evolução ao longo do tempo -> gráfico de LINHA
np.random.seed(40)
meses = [f"M{i}" for i in range(1, 13)]
assinantes = np.cumsum(np.random.uniform(50, 300, 12)) + 1000

fig, ax = plt.subplots()
ax.plot(meses, assinantes, marker="o")
ax.set_title("Crescimento de assinantes")
ax.set_ylabel("Assinantes")
plt.show()
```

**2.**
```python
import matplotlib.pyplot as plt
import numpy as np

# distribuição de uma variável numérica -> HISTOGRAMA
np.random.seed(41)
tempo_sessao = np.random.exponential(8, 500)

fig, ax = plt.subplots()
ax.hist(tempo_sessao, bins=30, color="steelblue", edgecolor="white")
ax.set_title("Distribuição do tempo de sessão")
ax.set_xlabel("Minutos")
plt.show()
```

**3.**
```python
import matplotlib.pyplot as plt
import numpy as np

# relação entre duas variáveis numéricas -> SCATTER PLOT
np.random.seed(42)
emails_enviados = np.random.uniform(0, 20, 70)
churn = emails_enviados * 0.3 + np.random.normal(0, 2, 70)

fig, ax = plt.subplots()
ax.scatter(emails_enviados, churn, alpha=0.6, color="steelblue")
ax.set_title("E-mails enviados x Churn")
ax.set_xlabel("E-mails enviados")
ax.set_ylabel("Churn (%)")
plt.show()
```

**4.**
```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# comparação numérica entre categorias -> BOXPLOT (mostra a distribuição
# completa do ticket em cada plano, não só a média)
np.random.seed(43)
df = pd.DataFrame({
    "plano": np.random.choice(["Bronze", "Prata", "Ouro", "Platina"], size=200),
    "ticket": np.random.uniform(20, 400, 200),
})

fig, ax = plt.subplots()
df.boxplot(column="ticket", by="plano", ax=ax)
ax.set_title("Ticket médio por plano")
plt.suptitle("")
plt.show()
```

**5.**
```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# correlação entre muitas variáveis numéricas -> HEATMAP
np.random.seed(44)
df = pd.DataFrame({
    "sessoes": np.random.uniform(1, 50, 150),
    "cliques": np.random.uniform(1, 200, 150),
    "conversoes": np.random.uniform(0, 30, 150),
    "tempo_medio": np.random.uniform(1, 15, 150),
})

sns.heatmap(df.corr(), annot=True, cmap="coolwarm", vmin=-1, vmax=1)
plt.title("Correlação entre métricas do produto")
plt.show()
```

**6.**
```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# duas variáveis categóricas -> barra agrupada a partir de um crosstab
np.random.seed(45)
df = pd.DataFrame({
    "regiao": np.random.choice(["Norte", "Sul", "Sudeste"], size=300),
    "plano": np.random.choice(["Free", "Pago"], size=300),
})

tabela = pd.crosstab(df["regiao"], df["plano"])
tabela.plot(kind="bar", figsize=(7, 4))
plt.title("Clientes por região e plano")
plt.ylabel("Quantidade")
plt.tight_layout()
plt.show()
```

**7.**
```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# numérica x categórica -> BOXPLOT por grupo
np.random.seed(46)
df = pd.DataFrame({
    "canal_suporte": np.random.choice(["Chat", "Telefone"], size=160),
    "nota": np.random.uniform(1, 10, 160),
})
df.loc[df["canal_suporte"] == "Chat", "nota"] += 1.5

fig, ax = plt.subplots()
df.boxplot(column="nota", by="canal_suporte", ax=ax)
ax.set_title("Nota de satisfação por canal de suporte")
plt.suptitle("")
plt.show()
```

**8.**
```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# duas variáveis numéricas + uma categórica -> SCATTER PLOT colorido por
# categoria (hue)
np.random.seed(47)
preco = np.random.uniform(5, 500, 120)
df = pd.DataFrame({
    "preco": preco,
    "quantidade": 2000 / preco + np.random.normal(0, 5, 120),
    "categoria": np.random.choice(["Eletrônicos", "Papelaria"], size=120),
})

fig, ax = plt.subplots()
for c, cor in [("Eletrônicos", "steelblue"), ("Papelaria", "orange")]:
    subset = df[df["categoria"] == c]
    ax.scatter(subset["preco"], subset["quantidade"], label=c, alpha=0.6, color=cor)
ax.set_title("Preço x Quantidade vendida, por categoria")
ax.legend()
plt.show()
```

**9.**
```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

np.random.seed(43)
df = pd.DataFrame({
    "plano": np.random.choice(["Bronze", "Prata", "Ouro", "Platina"], size=200),
    "ticket": np.random.uniform(20, 400, 200),
})

fig, ax = plt.subplots(figsize=(8, 5))
df.boxplot(column="ticket", by="plano", ax=ax)
ax.set_title("Distribuição do ticket médio por plano", fontsize=13, fontweight="bold")
ax.set_xlabel("Plano")
ax.set_ylabel("Ticket (R$)")
ax.grid(True, axis="y", alpha=0.3)
plt.suptitle("")
plt.tight_layout()
plt.show()
```

**10.**
```python
# Item 4 (ticket médio por plano): um gráfico de pizza com 4 fatias já
# dificulta comparar tamanhos com precisão, e piora ainda mais se novos
# planos forem adicionados no futuro -- barra ou boxplot (que já usamos)
# comunicam a comparação com muito mais clareza.

# Item 3 (e-mails x churn): a pergunta envolve só DUAS variáveis numéricas,
# então um gráfico 3D não adicionaria nenhuma informação real -- só
# tornaria mais difícil ler os valores com precisão, já que perspectivas 3D
# distorcem a percepção de posição dos pontos.
```

</details>
