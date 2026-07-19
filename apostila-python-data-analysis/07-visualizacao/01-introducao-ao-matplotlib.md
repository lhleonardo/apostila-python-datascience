# Introdução ao Matplotlib

> Módulo 7 — Visualização · Tópico 1 de 7

## O que é e por que importa

Matplotlib é a biblioteca de visualização mais fundamental do Python — quase
todas as outras (incluindo o `.plot()` do Pandas, visto de leve no Módulo 6,
e o Seaborn, visto no Tópico 6 deste módulo) são construídas em cima dela ou
inspiradas nela. Entender sua estrutura básica (mesmo que você acabe usando
Seaborn no dia a dia) é o que permite customizar qualquer detalhe de um
gráfico quando as bibliotecas de mais alto nível não oferecem a opção
pronta.

Instalação (se ainda não tiver):

```bash
pip install matplotlib
```

A convenção universal é importar o submódulo `pyplot` com o apelido `plt`:

```python
import matplotlib.pyplot as plt
```

## Como funciona (com exemplo comentado)

```python
import matplotlib.pyplot as plt

# Estrutura básica: uma FIGURE (a "folha" inteira) contém um ou mais AXES
# (os "eixos", a área onde o gráfico de fato é desenhado)
fig, ax = plt.subplots()  # cria uma figura com um único conjunto de eixos

x = [1, 2, 3, 4, 5]
y = [10, 25, 15, 30, 22]

ax.plot(x, y)  # desenha uma linha conectando os pontos (x, y)
ax.set_title("Vendas por dia")
ax.set_xlabel("Dia")
ax.set_ylabel("Vendas (R$)")

plt.show()  # em um script .py, abre a janela do gráfico
# em um notebook Jupyter, o gráfico costuma aparecer automaticamente após a
# célula, mas plt.show() continua funcionando sem problema

# Forma mais direta (sem criar fig/ax explicitamente) -- comum para gráficos
# rápidos de exploração, mas dá menos controle
plt.plot(x, y)
plt.title("Vendas por dia (forma direta)")
plt.show()

# Salvando um gráfico em arquivo, em vez de (ou além de) mostrar na tela
fig, ax = plt.subplots()
ax.plot(x, y)
fig.savefig("grafico_vendas.png", dpi=150, bbox_inches="tight")
# dpi controla a resolução; bbox_inches="tight" evita cortar rótulos nas bordas

# Múltiplos gráficos na mesma figura -- subplots com mais de um eixo
fig, eixos = plt.subplots(1, 2, figsize=(10, 4))  # 1 linha, 2 colunas de gráficos
eixos[0].plot(x, y)
eixos[0].set_title("Gráfico 1")
eixos[1].bar(x, y)
eixos[1].set_title("Gráfico 2")
plt.tight_layout()  # ajusta espaçamento para os títulos/rótulos não se sobreporem
plt.show()
```

A dupla `fig, ax = plt.subplots()` é o ponto de partida recomendado para
praticamente todo gráfico a partir de agora: `fig` controla propriedades da
figura inteira (tamanho, salvar em arquivo), `ax` controla o conteúdo do
gráfico em si (dados, títulos, eixos). Essa é a chamada **abordagem
orientada a objetos** do Matplotlib, mais previsível que a forma direta
(`plt.plot(...)` sem `ax`) quando os gráficos ficam mais complexos.

## Erros comuns de quem está começando

- Misturar a forma direta (`plt.plot`, `plt.title`) com a orientada a
  objetos (`ax.plot`, `ax.set_title`) sem perceber a diferença — os métodos
  têm nomes ligeiramente diferentes (`plt.title()` vs `ax.set_title()`), e
  misturar as duas formas de forma inconsistente costuma gerar confusão em
  gráficos com múltiplos subplots.
- Esquecer `plt.show()` em um script `.py` rodado fora de notebook e achar
  que "nada aconteceu" — sem essa chamada, a janela do gráfico nunca é
  aberta (em notebooks isso normalmente já acontece automaticamente, o que
  mascara o hábito de esquecer o `.show()`).
- Não usar `fig, ax = plt.subplots()` desde o início e precisar reescrever
  tudo depois para adicionar um segundo gráfico — vale começar já com essa
  estrutura mesmo em gráficos simples, para facilitar expandir depois.

## Exercício prático

1. Crie uma figura com `plt.subplots()` e desenhe uma linha com os dados
   `x = [1, 2, 3, 4, 5]` e `y = [5, 7, 4, 9, 12]`.
2. Adicione título `"Meu primeiro gráfico"`, rótulo `"X"` no eixo horizontal
   e `"Y"` no eixo vertical.
3. Crie uma figura com 2 subplots lado a lado (`1, 2`): no primeiro, desenhe
   a linha do item 1; no segundo, desenhe um gráfico de barras (`ax.bar`)
   com os mesmos dados.
4. Salve a figura do item 3 em um arquivo `meus_graficos.png`.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [5, 7, 4, 9, 12]

fig, ax = plt.subplots()
ax.plot(x, y)
ax.set_title("Meu primeiro gráfico")
ax.set_xlabel("X")
ax.set_ylabel("Y")
plt.show()

fig, eixos = plt.subplots(1, 2, figsize=(10, 4))
eixos[0].plot(x, y)
eixos[0].set_title("Linha")
eixos[1].bar(x, y)
eixos[1].set_title("Barra")
plt.tight_layout()
fig.savefig("meus_graficos.png", dpi=150, bbox_inches="tight")
plt.show()
```

</details>

## Checklist antes de avançar

- [ ] Entendo a diferença entre `figure` e `axes` no Matplotlib
- [ ] Sei criar um gráfico simples com `fig, ax = plt.subplots()`
- [ ] Sei criar múltiplos subplots numa mesma figura
- [ ] Sei salvar um gráfico em arquivo com `fig.savefig()`
- [ ] Resolvi o exercício sem olhar a solução
