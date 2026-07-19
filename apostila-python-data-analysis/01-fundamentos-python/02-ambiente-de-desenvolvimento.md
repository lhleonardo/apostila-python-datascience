# Ambiente de desenvolvimento

> Módulo 1 — Fundamentos de Python · Tópico 2 de 25

## O que é e por que importa

Para escrever e rodar código Python, você precisa de duas coisas: o **Python
instalado** no seu computador (o "motor" que entende e executa o código) e um
lugar para **escrever** esse código (um editor de texto). Pense no Python
como o motor de um carro e o editor como o painel — você precisa dos dois
para dirigir.

Neste tópico você vai instalar o Python e escrever seu primeiro script:
um arquivo `.py` com instruções que o computador executa de cima para baixo,
linha por linha. É a base de tudo que vem depois — inclusive das ferramentas
de análise de dados (pandas, numpy) que você vai usar mais para frente, que
nada mais são do que "extensões" que você adiciona a esse mesmo Python.

Mais para frente (Módulo 2) você vai conhecer ambientes mais sofisticados
como JupyterLab e Google Colab, que são melhores para explorar dados
interativamente. Mas para aprender lógica de programação, um editor simples e
um arquivo `.py` são suficientes — e ajudam a entender o que está acontecendo
por baixo dos panos antes de usar ferramentas mais "automáticas".

## Como funciona (com exemplo comentado)

Passo a passo:

1. Baixe e instale o Python em [python.org/downloads](https://www.python.org/downloads/)
   (marque a opção "Add Python to PATH" durante a instalação, no Windows).
2. Instale um editor de código. O mais comum é o [VS Code](https://code.visualstudio.com/)
   (gratuito). Depois de instalar, adicione a extensão "Python" dentro dele.
3. Crie uma pasta no seu computador para os exercícios desta apostila, por
   exemplo `loja-da-ana`.
4. Dentro dessa pasta, crie um arquivo chamado `primeiro_script.py`.
5. Escreva o código abaixo nesse arquivo e rode (no VS Code, botão "Run" ou
   `Ctrl+F5`; pelo terminal, comando `python primeiro_script.py`).

```python
# Este é um comentário — o Python ignora tudo depois do #.
# Comentários servem para explicar o código para humanos, não para o computador.

# print() é a instrução que mostra algo na tela.
print("Bem-vindo à Loja da Ana!")

# Podemos rodar quantas instruções quisermos, uma por linha.
print("Sistema de análise de vendas iniciado.")
```

Se aparecer `Bem-vindo à Loja da Ana!` e `Sistema de análise de vendas
iniciado.` na tela (no "terminal" ou "console"), seu ambiente está funcionando.

## Erros comuns de quem está começando

- Instalar o Python mas esquecer de marcar "Add to PATH" no Windows — isso faz
  o terminal não encontrar o comando `python`. Se isso acontecer, reinstale
  marcando a opção.
- Salvar o arquivo com extensão errada (ex: `.txt` em vez de `.py`) — o editor
  não vai reconhecer como código Python.
- Confundir "rodar o arquivo" com "abrir o arquivo". Abrir só mostra o texto;
  rodar é o que faz o computador executar as instruções.

## Exercício prático

Crie um arquivo chamado `loja_da_ana.py` na sua pasta de exercícios. Nele,
use `print()` para mostrar, em linhas separadas:

1. O nome da loja: `Loja da Ana`
2. Um "slogan" qualquer que você inventar
3. A frase `Relatorio de vendas - Dia 1`

Rode o arquivo e confirme que as três linhas aparecem na tela, na ordem
correta.

**Desafio bônus (opcional):** pesquise como comentar múltiplas linhas de uma
vez (sem colocar `#` em cada uma) e adicione um bloco de comentário no topo do
arquivo explicando o que o script faz.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
# Script de abertura do relatorio da Loja da Ana

print("Loja da Ana")
print("Qualidade que cabe no seu bolso")
print("Relatorio de vendas - Dia 1")

# Cada print() joga uma linha nova na tela — por isso elas aparecem
# empilhadas, na mesma ordem em que escrevemos.
```

</details>

## Checklist antes de avançar

- [ ] Tenho Python instalado e consigo rodar um arquivo `.py`
- [ ] Tenho um editor de código configurado
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Entendo a diferença entre "abrir" e "rodar" um script
