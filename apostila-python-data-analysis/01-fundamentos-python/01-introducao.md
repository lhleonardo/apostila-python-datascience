# Introdução

> Módulo 1 — Fundamentos de Python · Tópico 1 de 25

## O que é e por que importa

Python é uma linguagem de programação criada para ser fácil de ler e escrever.
Isso pode parecer um detalhe bobo, mas é o motivo principal pelo qual ela virou
a linguagem mais usada em análise de dados: você passa menos tempo lutando com
a sintaxe e mais tempo pensando no problema que quer resolver.

Pensa assim: se Excel é uma calculadora com superpoderes para tabelas, Python é
uma calculadora ainda mais poderosa, sem limite de linhas, que você programa
para fazer exatamente o que quiser — repetir uma tarefa mil vezes, cruzar
dados de fontes diferentes, gerar gráficos, detectar padrões. A diferença é
que, em vez de clicar em menus, você escreve instruções em texto.

"Análise de dados" é o processo de pegar um monte de números e informações
soltas (vendas de um mês, respostas de uma pesquisa, temperaturas de uma
cidade) e transformar isso em respostas para perguntas concretas: "qual
produto vendeu mais?", "os clientes estão satisfeitos?", "vai chover
amanhã?". Python entra como a ferramenta que te ajuda a carregar esses dados,
limpá-los, calcular coisas sobre eles e visualizar o resultado.

Ao longo desta apostila, você vai construir esse conhecimento em cima de um
exemplo que se repete: os dados de vendas da "Loja da Ana", uma lojinha
fictícia de bairro. Começamos do zero absoluto e, módulo a módulo, vamos
adicionando ferramentas até você conseguir fazer uma análise completa sozinho.

## Como funciona (com exemplo comentado)

Ainda não vamos escrever código de verdade neste tópico (isso começa no
próximo, quando configuramos o ambiente). Mas para você já sentir o gostinho,
aqui está o tipo de coisa que você será capaz de fazer ao final do Módulo 1:

```python
# Uma lista com o valor de cada venda do dia, na Loja da Ana
vendas_do_dia = [45.90, 120.00, 15.50, 200.00, 33.00]

# Somando todas as vendas para saber o faturamento do dia
faturamento = sum(vendas_do_dia)

# Mostrando o resultado na tela
print("Faturamento do dia:", faturamento)
```

Repare que o código lê quase como português: "some as vendas do dia" e
"mostre o faturamento". Essa é a filosofia do Python — código que se lê como
uma receita de bolo.

## Erros comuns de quem está começando

- Achar que precisa "decorar" Python antes de começar a programar. Na
  prática, você aprende programando e errando — ninguém decora a sintaxe
  inteira antes de escrever a primeira linha.
- Confundir "aprender Python" com "aprender análise de dados". Python é a
  ferramenta; análise de dados é o objetivo. Esta apostila ensina os dois
  juntos, mas é normal sentir que está demorando para "chegar no que
  interessa" — os fundamentos deste módulo são o alicerce de tudo depois.
- Comparar seu progresso com o de outras pessoas. Lógica de programação é uma
  habilidade nova para o cérebro, e é normal levar tempo para "clicar".

## Exercício prático

Não há exercício de código neste tópico (ainda não instalamos nada). Em vez
disso, responda por escrito, com suas próprias palavras:

1. O que você espera conseguir fazer com dados depois de terminar esta
   apostila?
2. Pense em um dado do seu dia a dia (gastos do mês, horas de sono, o que
   for). Que pergunta você gostaria de responder sobre esse dado?

Guarde essas respostas — vamos usar ideias parecidas nos exercícios mais para
frente.

**Desafio bônus (opcional):** pesquise rapidamente três áreas de trabalho que
usam Python para análise de dados (ex: mercado financeiro, saúde, marketing)
e anote uma frase sobre cada uma.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

Este tópico é conceitual, então não há uma "resposta certa" — a solução é
reflexiva. O importante é que você tenha uma ideia (mesmo vaga) do tipo de
pergunta que quer responder com dados. Isso vai te dar motivação real ao
longo da apostila.

</details>

## Checklist antes de avançar

- [ ] Consigo explicar com minhas palavras o que é Python e para que serve em
      análise de dados
- [ ] Entendo que vamos usar a "Loja da Ana" como exemplo contínuo
- [ ] Escrevi minhas respostas do exercício
