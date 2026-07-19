# pip (instalando pacotes)

> Módulo 2 — Python Intermediário e Ambiente · Tópico 6 de 11

## O que é e por que importa

Até agora você só usou o que já vem "de fábrica" no Python (`random`, `re`, `json`, `csv` — módulos embutidos que não precisam de instalação). Mas o que faz do Python uma linguagem tão forte em análise de dados são bibliotecas externas como pandas, numpy e matplotlib, que **não** vêm instaladas junto com o Python — você precisa buscá-las e instalá-las separadamente.

`pip` é o "gerenciador de pacotes" do Python: um programa de linha de comando que baixa e instala bibliotecas de um repositório público chamado PyPI (*Python Package Index*). Pensa nele como uma loja de aplicativos para o seu Python — em vez de procurar o instalador de cada biblioteca manualmente na internet, você digita um comando e o `pip` baixa, instala e organiza tudo para você.

Esse tópico é a ponte entre "Python puro" (o que você aprendeu até aqui) e as ferramentas de dados que vêm a partir do Módulo 3. Antes de instalar pandas e numpy, você precisa saber como o `pip` funciona — inclusive porque, no mercado de trabalho, é comum um projeto especificar exatamente quais bibliotecas (e quais versões delas) ele precisa, para garantir que o código funcione igual na sua máquina e na de outra pessoa.

## Como funciona (com exemplo comentado)

`pip` é usado no terminal (a tela de linha de comando), não dentro de um arquivo `.py`. Abra o terminal do seu computador (ou o terminal integrado do VS Code, que veremos em `09-vs-code.md`) e experimente:

```bash
# Verifica se o pip está instalado e qual versão
pip --version

# Instala a versão mais recente disponível de uma biblioteca
pip install pandas

# Instala uma versão ESPECÍFICA de uma biblioteca (útil quando um projeto
# exige uma versão exata, para evitar incompatibilidades)
pip install pandas==2.1.0

# Instala uma versão MÍNIMA (qualquer uma igual ou mais nova que a indicada)
pip install pandas>=2.0.0

# Lista todas as bibliotecas instaladas no ambiente atual, com suas versões
pip list

# Mostra detalhes de uma biblioteca já instalada (versão, local, dependências)
pip show pandas

# Desinstala uma biblioteca
pip uninstall pandas

# Gera um arquivo requirements.txt com todas as bibliotecas instaladas e suas
# versões -- um "resumo" de tudo que o projeto precisa para funcionar
pip freeze > requirements.txt

# Instala TODAS as bibliotecas listadas em um requirements.txt de uma vez --
# muito comum ao pegar um projeto de outra pessoa ou configurar uma máquina nova
pip install -r requirements.txt
```

Um `requirements.txt` de exemplo, como o que a Loja da Ana usaria em um projeto real de análise de dados:

```text
pandas==2.1.0
numpy==1.26.0
matplotlib==3.8.0
```

Esse arquivo funciona como uma "lista de compras": qualquer pessoa (ou você mesmo, em outro computador) roda `pip install -r requirements.txt` e recria exatamente o mesmo ambiente, com as mesmas bibliotecas e versões.

## Erros comuns de quem está começando

- Rodar `pip install` dentro do código Python (ex: escrever `pip install pandas` num arquivo `.py`) — isso é um comando de terminal, não uma instrução Python, e vai gerar erro de sintaxe se colado num script.
- Instalar uma biblioteca em um projeto e ela "não aparecer" no outro — geralmente é sinal de que os dois projetos estão usando ambientes Python diferentes (veremos como isolar isso em `07-ambientes-virtuais-venv.md`).
- Ignorar mensagens de erro do `pip install` achando que "deu certo mesmo assim". Erros de instalação costumam indicar problema de versão do Python, permissão, ou conexão com a internet — vale sempre ler a mensagem antes de tentar de novo.

## Exercício prático

Sem precisar rodar nada (ou, se quiser, rode de verdade no seu terminal):

1. Escreva o comando que instalaria a versão `1.5.3` exata da biblioteca `requests`.
2. Escreva o comando que lista todas as bibliotecas instaladas no seu ambiente atual.
3. Escreva o conteúdo de um `requirements.txt` fictício para um projeto que usa `pandas` versão `2.1.0` e `matplotlib` versão `3.8.0`.

**Desafio bônus (opcional):** se você já tem Python instalado, rode `pip list` de verdade no seu terminal e identifique se `pip` já veio instalado junto (em instalações modernas do Python, geralmente vem).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```bash
# 1. Instalar versão exata do requests
pip install requests==1.5.3

# 2. Listar bibliotecas instaladas
pip list

# 3. Conteúdo de um requirements.txt
```
```text
pandas==2.1.0
matplotlib==3.8.0
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar o que é o pip e para que serve um `requirements.txt`
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Sei a diferença entre `pip install nome`, `pip install nome==versao` e `pip install nome>=versao`
