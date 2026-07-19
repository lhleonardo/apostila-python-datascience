# JupyterLab

> Módulo 2 — Python Intermediário e Ambiente · Tópico 10 de 11

## O que é e por que importa

Até agora, você escreveu código em arquivos `.py` que rodam de cima para baixo, do início ao fim, toda vez. JupyterLab propõe outra forma de trabalhar: um **notebook** (arquivo `.ipynb`), que é dividido em pequenos blocos chamados **células**, cada uma podendo ser executada de forma independente e na ordem que você quiser.

Pensa num notebook como um caderno de anotações de laboratório: em vez de escrever um relatório inteiro de uma vez e só ver o resultado no final, você testa um pedaço, vê o resultado ali mesmo, ajusta, testa o próximo pedaço — sem precisar rodar tudo de novo desde o início cada vez que muda algo. Isso é exatamente o que análise de dados exige na prática: carregar os dados uma vez (processo que pode demorar), e depois ir testando cálculos e gráficos diferentes em cima deles, sem recarregar tudo a cada tentativa.

Existem dois tipos de célula: **células de código**, que rodam Python de verdade (e mostram o resultado logo abaixo, incluindo tabelas e gráficos), e **células de markdown**, que mostram texto formatado (títulos, listas, explicações) — úteis para documentar o raciocínio da análise junto com o código, como se fosse um relatório interativo.

JupyterLab é ótimo para **explorar** dados — testar hipóteses, visualizar rapidamente, ajustar um filtro e ver o efeito na hora. Mas é ruim para **produção** (código que vai rodar automaticamente todo dia, por exemplo): notebooks não são feitos para isso, são mais difíceis de testar automaticamente, de versionar bem, e de rodar de forma confiável sem intervenção manual. Scripts `.py` (o que você já aprendeu) continuam sendo a escolha certa para automatizar processos.

## Como funciona (com exemplo comentado)

Passo a passo para instalar e abrir:

```bash
# Com um ambiente virtual ativado (visto em 07-ambientes-virtuais-venv.md),
# instale o JupyterLab
pip install jupyterlab

# Rode o comando abaixo dentro da pasta do seu projeto para abrir o
# JupyterLab no navegador
jupyter lab
```

```text
1. O comando "jupyter lab" abre uma aba no seu navegador com a interface do
   JupyterLab.
2. Clique em "Notebook" (sob Python 3) para criar um notebook novo (.ipynb).
3. Uma célula vazia aparece -- por padrão, é uma célula de código.
4. Escreva código Python nela e rode com Shift+Enter (roda a célula atual e
   já cria/pula para a próxima).
5. Para transformar uma célula em markdown, selecione a célula e mude o tipo
   no menu suspenso da barra de ferramentas (de "Code" para "Markdown").
```

Um exemplo do que aconteceria célula por célula, num notebook de análise da Loja da Ana:

```python
# --- Célula 1 (código) ---
vendas_do_dia = [45.90, 120.00, 15.50, 200.00, 33.00]
```

```python
# --- Célula 2 (código) ---
# Essa célula só funciona se a Célula 1 já tiver rodado antes --
# ela depende da variável "vendas_do_dia" já existir na memória do notebook
faturamento = sum(vendas_do_dia)
print("Faturamento do dia:", faturamento)
```

```text
--- Célula 3 (markdown) ---
## Análise do faturamento

O faturamento do dia foi calculado somando todas as vendas registradas.
```

A **ordem de execução** é o ponto mais importante de entender: o notebook não roda "de cima para baixo" automaticamente como um script — ele roda a célula que **você** mandar rodar, na ordem que você mandar. Ao lado de cada célula de código aparece um número entre colchetes, como `[1]`, `[2]`, `[3]`, mostrando em que ordem aquela célula foi executada de verdade. Isso é poderoso (permite testar coisas fora de ordem, refazer só um pedaço), mas também é a maior fonte de confusão de quem está começando.

## Erros comuns de quem está começando

- Rodar células fora de ordem e se confundir com o resultado. Se você rodar a Célula 2 antes da Célula 1, ou rodar a Célula 1 de novo depois de mudar uma variável em outro lugar, o estado da memória pode não bater com o que você vê na tela, escrito de cima para baixo.
- Achar que "salvar o notebook" garante que ele vai rodar do mesmo jeito depois. Um notebook salvo guarda o **resultado** da última execução de cada célula, mas não garante que rodar tudo de novo, na ordem das células, dê o mesmo resultado (variáveis podem ter sido alteradas fora de ordem).
- Usar notebooks para código que precisa rodar sozinho, todo dia, sem supervisão (como um relatório automático) — para isso, o ideal continua sendo um script `.py`, não um notebook.

## Exercício prático

Instale o JupyterLab no seu ambiente virtual e crie um notebook novo. Nele:

1. Em uma célula de markdown, escreva um título tipo `## Análise de vendas — Loja da Ana`.
2. Em uma célula de código, crie uma lista `vendas_do_dia` com pelo menos 5 valores.
3. Em outra célula de código, calcule e imprima o faturamento total (soma da lista).
4. Em uma terceira célula de código, calcule e imprima a venda média (faturamento dividido pelo número de vendas).

**Desafio bônus (opcional):** rode a célula do faturamento total, depois volte e mude um valor da lista `vendas_do_dia` na primeira célula, sem rodar essa célula de novo. Rode a célula da venda média e observe: ela usa o valor antigo ou o novo? Explique por quê, com suas próprias palavras.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```text
Célula 1 (markdown):
## Análise de vendas — Loja da Ana
```

```python
# Célula 2 (código)
vendas_do_dia = [45.90, 120.00, 15.50, 200.00, 33.00]
```

```python
# Célula 3 (código)
faturamento_total = sum(vendas_do_dia)
print("Faturamento total:", faturamento_total)
```

```python
# Célula 4 (código)
venda_media = faturamento_total / len(vendas_do_dia)
print("Venda média:", venda_media)
```

Desafio bônus: se você mudar a lista na Célula 2 mas não rodar essa célula de novo, a variável `vendas_do_dia` na memória do notebook continua com o valor **antigo** — a Célula 4 vai usar o `faturamento_total` calculado com o valor antigo, mesmo que o texto na tela mostre a lista "nova". Isso acontece porque o notebook guarda o estado da última execução de cada célula, não o texto que está escrito nela.

</details>

## Checklist antes de avançar

- [ ] Consigo explicar a diferença entre célula de código e célula de markdown
- [ ] Entendo por que a ordem de execução pode ser diferente da ordem visual das células
- [ ] Resolvi o exercício sem olhar a solução
