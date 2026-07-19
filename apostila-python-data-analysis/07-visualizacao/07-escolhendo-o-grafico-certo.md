# Escolhendo o gráfico certo

> Módulo 7 — Visualização · Tópico 7 de 7 (último do módulo)

## O que é e por que importa

Com Matplotlib e Seaborn no repertório, a última habilidade a desenvolver
não é técnica — é de **julgamento**: dado um conjunto de dados e uma
pergunta, qual gráfico comunica a resposta com mais clareza? Este tópico
fecha o módulo com um guia de decisão e um checklist de qualidade, para você
não escolher um gráfico só porque "é o que sei fazer", mas porque é o mais
adequado à pergunta.

## Como funciona (guia de decisão)

A escolha do gráfico depende principalmente de dois fatores: **quantas
variáveis** você quer mostrar, e **de que tipo** elas são (numérica ou
categórica).

```
Uma variável numérica          -> Histograma ou boxplot (Tópico 3)
Uma variável categórica        -> Gráfico de barra com contagens (Tópico 2)
Evolução ao longo do tempo     -> Gráfico de linha (Tópico 2)
Duas variáveis numéricas       -> Scatter plot (Tópico 4)
Numérica x categórica          -> Boxplot por grupo, ou barra com médias (Tópicos 3 e 6)
Duas variáveis categóricas     -> Barra empilhada/agrupada, ou heatmap de uma crosstab
Muitas variáveis numéricas     -> Heatmap de correlação, ou pairplot (Tópico 6)
```

```python
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
import numpy as np

np.random.seed(4)
df = pd.DataFrame({
    "categoria": np.random.choice(["Papelaria", "Eletronicos", "Roupas"], size=200),
    "regiao": np.random.choice(["Norte", "Sul"], size=200),
    "preco": np.random.uniform(10, 200, 200),
    "avaliacao": np.random.uniform(3, 5, 200),
})

# Exemplo de "duas variáveis categóricas" -- barra agrupada a partir de um crosstab
# (revisão do Módulo 6, Tópico 6)
tabela = pd.crosstab(df["categoria"], df["regiao"])
tabela.plot(kind="bar", figsize=(7, 4))
plt.title("Quantidade de produtos por categoria e região")
plt.ylabel("Quantidade")
plt.tight_layout()
plt.show()

# Checklist de qualidade -- aplicando num gráfico "final", pronto para apresentar
fig, ax = plt.subplots(figsize=(8, 5))
sns.boxplot(data=df, x="categoria", y="preco", ax=ax)
ax.set_title("Distribuição de preço por categoria", fontsize=13, fontweight="bold")
ax.set_xlabel("Categoria")
ax.set_ylabel("Preço (R$)")
ax.grid(True, axis="y", alpha=0.3)
plt.tight_layout()
plt.show()

# Perguntas para revisar antes de considerar um gráfico "pronto":
# 1. O tipo de gráfico é o mais adequado para a pergunta e o tipo de dado?
# 2. Título e eixos estão rotulados (com unidade, quando fizer sentido)?
# 3. As cores são consistentes com outros gráficos do mesmo relatório?
# 4. Dá para entender o gráfico sem precisar de explicação adicional em texto?
# 5. Não há elementos visuais desnecessários (grades excessivas, 3D sem
#    necessidade, cores demais) competindo por atenção?
```

## Erros comuns de quem está começando

- Escolher gráfico de pizza para comparar muitas categorias — pizza fica
  ilegível com mais de 4-5 fatias, e comparar tamanhos de fatia é mais
  difícil visualmente do que comparar o comprimento de barras; para a
  maioria dos casos, barra é a escolha mais segura.
- Usar 3D "porque parece mais impressionante" quando duas dimensões já
  bastam — gráficos 3D costumam ser mais difíceis de ler com precisão do
  que a versão 2D equivalente, mesmo quando parecem visualmente
  interessantes.
- Gerar o gráfico e considerar a tarefa terminada sem revisar título,
  rótulos e clareza — um gráfico sem rótulos claros exige que quem o
  interpreta já saiba o contexto de antemão, o que raramente é o caso fora
  da sua própria análise.

## Exercício prático

Para cada pergunta abaixo, escolha o tipo de gráfico mais adequado
(justificando em uma frase) e implemente com dados fictícios de sua
escolha:

1. "Como o faturamento da empresa evoluiu nos últimos 12 meses?"
2. "Qual a distribuição de idades dos clientes?"
3. "Existe relação entre gastos em marketing e vendas?"
4. "Como o preço médio varia entre as 5 categorias de produto da loja?"
5. "Quais variáveis numéricas do meu dataset parecem mais correlacionadas
   entre si?"

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
import numpy as np

# 1. Evolução no tempo -> gráfico de LINHA
meses = [f"M{i}" for i in range(1, 13)]
faturamento = np.cumsum(np.random.uniform(-500, 2000, 12)) + 10000
fig, ax = plt.subplots()
ax.plot(meses, faturamento, marker="o")
ax.set_title("Faturamento nos últimos 12 meses")
plt.show()

# 2. Distribuição de uma variável numérica -> HISTOGRAMA
idades = np.random.normal(35, 12, 300)
fig, ax = plt.subplots()
ax.hist(idades, bins=25, color="steelblue", edgecolor="white")
ax.set_title("Distribuição de idades dos clientes")
plt.show()

# 3. Relação entre duas numéricas -> SCATTER PLOT
marketing = np.random.uniform(1000, 10000, 50)
vendas = marketing * 2 + np.random.normal(0, 2000, 50)
fig, ax = plt.subplots()
ax.scatter(marketing, vendas, alpha=0.6)
ax.set_title("Marketing x Vendas")
plt.show()

# 4. Comparação numérica entre categorias -> BARRA (média) ou BOXPLOT (distribuição)
categorias = [f"Cat{i}" for i in range(1, 6)]
preco_medio = np.random.uniform(20, 100, 5)
fig, ax = plt.subplots()
ax.bar(categorias, preco_medio, color="steelblue")
ax.set_title("Preço médio por categoria")
plt.show()

# 5. Correlação entre muitas numéricas -> HEATMAP
df_numerico = pd.DataFrame({
    "preco": np.random.uniform(10, 200, 100),
    "avaliacao": np.random.uniform(3, 5, 100),
    "vendas": np.random.uniform(10, 500, 100),
})
sns.heatmap(df_numerico.corr(), annot=True, cmap="coolwarm", vmin=-1, vmax=1)
plt.show()
```

</details>

## Checklist antes de avançar

- [ ] Sei escolher o gráfico adequado com base no tipo e quantidade de variáveis
- [ ] Sei revisar um gráfico usando o checklist de qualidade (título, rótulos, clareza)
- [ ] Sei explicar por que evitar gráfico de pizza com muitas categorias e gráficos 3D desnecessários
- [ ] Resolvi o exercício sem olhar a solução

## Checklist do Módulo 7

Antes de seguir para o Projeto Final, confirme que você consegue, sem
consultar a apostila:

- [ ] Criar um gráfico básico com `fig, ax = plt.subplots()`
- [ ] Escolher entre gráfico de linha e de barra de acordo com o tipo de dado
- [ ] Criar histogramas e boxplots, e interpretá-los
- [ ] Criar scatter plots e interpretar padrões (lineares e não-lineares)
- [ ] Customizar título, rótulos, cores e anotações de um gráfico
- [ ] Usar Seaborn para gráficos estatísticos direto de um DataFrame
- [ ] Escolher o tipo de gráfico certo para uma pergunta de análise específica

Pronto? Siga para o [Projeto Final](../08-projeto-final.md).
