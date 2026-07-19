# Projeto Final — Projeto Integrador

> 3–5 dias

## O que é este projeto

Você passou por sete módulos: fundamentos de Python, ambiente e ferramentas,
NumPy, Pandas, limpeza de dados, estatística/EDA e visualização. Este
projeto final não ensina nada novo — ele junta tudo em um fluxo de trabalho
único, do jeito que aconteceria numa análise de dados real: carregar dados
brutos, limpá-los, explorá-los estatisticamente, visualizar os achados e
comunicar uma conclusão.

Não existe "a" solução certa aqui. Duas pessoas podem analisar o mesmo
dataset e chegar a recortes, gráficos e conclusões diferentes — o que
importa é que cada decisão seja justificada e que o processo seja sólido.

## O dataset

Sugestão: **dados de qualidade do ar / poluição** ou **vendas de uma loja
de e-commerce** — qualquer dataset público tabular com pelo menos:

- 500+ linhas
- Uma mistura de colunas numéricas e categóricas
- Pelo menos uma coluna de data
- Problemas reais de qualidade (valores ausentes, duplicatas, tipos
  inconsistentes) — datasets "perfeitos demais" não deixam você praticar a
  parte de limpeza

Algumas fontes conhecidas de datasets públicos: Kaggle, dados.gov.br, UCI
Machine Learning Repository, Google Dataset Search. Escolha um tema que
genuinamente desperte sua curiosidade — você vai passar alguns dias
olhando para esses dados.

**Backup caso não consiga baixar nada:** monte você mesmo um dataset
sintético parecido com o do exercício do Módulo 5, Tópico 7 (checklist de
qualidade de dados), só que maior — por exemplo, gere 500-1000 linhas de
vendas fictícias com `numpy.random`, introduzindo de propósito valores
ausentes, duplicatas e tipos inconsistentes, para ter algo realista para
praticar.

## Etapas do projeto

### 1. Pergunta de negócio

Antes de escrever qualquer código, defina 2-3 perguntas que você quer
responder com os dados (ex: "quais produtos têm a maior margem de lucro?",
"existe sazonalidade nas vendas ao longo do ano?", "que fatores parecem
associados a avaliações baixas?"). Elas guiam todas as decisões seguintes —
sem uma pergunta, é fácil se perder explorando dados sem rumo.

### 2. Carregar e diagnosticar (Módulos 4 e 5)

- Carregue o dataset com Pandas.
- Rode o roteiro de diagnóstico do Módulo 5, Tópico 7: `.info()`,
  `.isnull().sum()`, `.duplicated().sum()`, tipos de cada coluna,
  `.unique()` de colunas de texto.
- Documente (em comentários ou markdown, se estiver num notebook) os
  problemas encontrados antes de corrigir qualquer coisa.

### 3. Limpar (Módulo 5)

- Trate valores ausentes com uma estratégia justificada (remover, preencher
  com estatística, preencher por grupo).
- Remova duplicatas.
- Corrija tipos de dados (números, datas).
- Padronize texto inconsistente.
- Trate outliers, decidindo caso a caso se são erros ou eventos legítimos.
- Valide o resultado final (confirme que os problemas foram resolvidos).

### 4. Explorar (Módulo 6)

- Faça a análise univariada das colunas mais relevantes para suas
  perguntas de negócio (tendência central, dispersão, forma da
  distribuição).
- Faça a análise bivariada relevante (`groupby`, `crosstab`, correlação).
- Se aplicável, monte uma amostra e reflita sobre o quanto seus achados
  generalizariam para um conjunto de dados maior (Módulo 6, Tópico 7).

### 5. Visualizar (Módulo 7)

Produza pelo menos 4 gráficos, cada um respondendo diretamente a uma das
perguntas definidas no passo 1. Para cada gráfico:

- Escolha o tipo certo para a pergunta e o tipo de dado (Módulo 7, Tópico
  7).
- Garanta título, rótulos de eixo e, se necessário, legenda.
- Use cores consistentes se houver mais de um gráfico com as mesmas
  categorias.

### 6. Comunicar

Escreva uma síntese final (um parágrafo por pergunta de negócio) com:

- A resposta encontrada, com base nos números e gráficos.
- O nível de confiança nessa resposta (os dados são suficientes? há
  limitações, como amostra pequena ou muitos valores ausentes numa coluna
  chave?).
- Uma recomendação prática, se fizer sentido para o contexto escolhido.

## Checklist de conclusão

- [ ] Defini 2-3 perguntas de negócio antes de começar a analisar
- [ ] Diagnostiquei o dataset (ausentes, duplicatas, tipos, inconsistências de texto) antes de limpar
- [ ] Apliquei e justifiquei estratégias de limpeza para cada problema encontrado
- [ ] Validei que a limpeza funcionou (sem ausentes/duplicatas remanescentes não intencionais)
- [ ] Fiz análise univariada e bivariada relevante para as perguntas definidas
- [ ] Produzi pelo menos 4 gráficos, cada um respondendo a uma pergunta específica
- [ ] Todos os gráficos têm título, rótulos e (quando aplicável) legenda
- [ ] Escrevi uma síntese final com resposta, nível de confiança e recomendação para cada pergunta

## E depois?

Terminar este projeto significa que você tem, na prática, o fluxo completo
de um analista de dados júnior: carregar, limpar, explorar, visualizar e
comunicar. A partir daqui, os próximos passos naturais (fora do escopo desta
apostila) costumam ser: aprofundar SQL para buscar dados direto de bancos,
aprender uma ferramenta de dashboard (Power BI, Tableau, ou Streamlit em
Python), ou seguir para Machine Learning com scikit-learn, que usa
diretamente os DataFrames que você já sabe preparar.

Parabéns por chegar até aqui — o caminho de "sabe o básico de Python" até
"consegue tocar uma análise de dados do início ao fim" não é curto.
