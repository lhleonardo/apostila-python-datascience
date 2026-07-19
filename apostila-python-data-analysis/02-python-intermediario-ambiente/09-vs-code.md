# VS Code (configuração básica para Python)

> Módulo 2 — Python Intermediário e Ambiente · Tópico 9 de 11

## O que é e por que importa

Você já instalou o VS Code no Módulo 1 (`02-ambiente-de-desenvolvimento.md`) para escrever seus primeiros scripts. Agora que você vai lidar com bibliotecas externas, ambientes virtuais e arquivos de dados, vale configurar o VS Code direito para que ele "converse" bem com tudo isso — em vez de só abrir arquivos de texto, ele pode entender seu ambiente Python, sugerir código, apontar erros antes de você rodar, e até rodar notebooks Jupyter (visto no próximo tópico) sem sair do editor.

Pensa no VS Code como um painel de controle: sozinho, ele é só um editor de texto genérico. As "extensões" são como aplicativos que você instala dentro dele para ganhar funcionalidades específicas — a extensão "Python" ensina o VS Code a entender arquivos `.py`, mostrar erros de sintaxe, sugerir autocompletar, e rodar código diretamente.

Um conceito chave aqui é o **interpretador**: é a instalação específica do Python que o VS Code vai usar para rodar seu código (pode ser o Python global do computador, ou um ambiente virtual específico de um projeto, como visto em `07-ambientes-virtuais-venv.md`). Selecionar o interpretador errado é uma das causas mais comuns de "por que essa biblioteca que eu instalei não aparece no VS Code?".

## Como funciona (com exemplo comentado)

Passo a passo de configuração:

```text
1. Abra o VS Code.
2. Vá até a aba de Extensões (ícone de blocos quadrados na barra lateral,
   ou atalho Ctrl+Shift+X).
3. Busque por "Python" (da Microsoft) e clique em "Install".
4. Enquanto estiver ali, busque também por "Jupyter" (da Microsoft) e instale --
   ela permite abrir e rodar notebooks (.ipynb) direto dentro do VS Code,
   sem precisar abrir o JupyterLab separadamente (veremos no próximo tópico).
```

```text
5. Abra a pasta do seu projeto (Menu > File > Open Folder), por exemplo a
   pasta "loja-da-ana" onde você já tem seu ambiente virtual criado.
6. Abra um arquivo .py qualquer dentro dessa pasta.
7. No canto inferior direito do VS Code, deve aparecer o nome de um
   interpretador Python (ex: "Python 3.11.4"). Clique nele.
8. Uma lista aparece com os interpretadores disponíveis -- escolha o que
   corresponde ao ambiente virtual do seu projeto (geralmente aparece como
   algo como "./venv/bin/python" ou "venv\Scripts\python.exe").
9. Se o ambiente virtual do projeto não aparecer na lista, clique em
   "Enter interpreter path..." e navegue até o arquivo python.exe dentro
   da pasta venv do projeto.
```

```text
10. Para rodar um arquivo .py: com o arquivo aberto, clique no botão de
    "play" (triângulo) no canto superior direito, ou use o atalho Ctrl+F5.
11. O resultado aparece no "terminal integrado" -- uma aba de terminal que
    já vem embutida no próprio VS Code (Menu > Terminal > New Terminal, ou
    atalho Ctrl+`). Esse terminal já roda dentro da pasta do seu projeto e,
    se o interpretador certo estiver selecionado, já usa o ambiente virtual
    ativado automaticamente.
```

Depois de configurado, seu fluxo de trabalho fica assim: abrir a pasta do projeto no VS Code, conferir que o interpretador certo está selecionado (canto inferior direito), escrever o código, e rodar com Ctrl+F5 ou pelo terminal integrado.

## Erros comuns de quem está começando

- Instalar uma biblioteca com `pip install` no terminal integrado, mas o VS Code estar configurado para usar um interpretador Python diferente do que o terminal está usando — resultado: "ModuleNotFoundError" mesmo depois de instalar. A solução é sempre conferir, no canto inferior direito, se o interpretador selecionado é o mesmo ambiente onde você instalou a biblioteca.
- Abrir um arquivo `.py` solto (sem abrir a pasta inteira do projeto com "Open Folder") — isso faz o VS Code não enxergar corretamente o ambiente virtual e outros arquivos relacionados do projeto.
- Ignorar os sublinhados coloridos que a extensão Python desenha no código (avisos e erros antes mesmo de rodar) — vale passar o mouse por cima para entender o que está sendo sinalizado, em vez de só rodar e ver o erro acontecer.

## Exercício prático

No seu computador:

1. Instale as extensões "Python" e "Jupyter" no VS Code.
2. Abra (ou crie) a pasta do projeto onde você tem um ambiente virtual criado (do exercício de `07-ambientes-virtuais-venv.md`).
3. Abra um arquivo `.py` de teste e verifique, no canto inferior direito, qual interpretador está selecionado.
4. Troque para o interpretador do seu ambiente virtual, se ainda não estiver selecionado.
5. Rode o arquivo com Ctrl+F5 e confirme que o resultado aparece no terminal integrado.

**Desafio bônus (opcional):** abra o terminal integrado (Ctrl+`) e rode `pip list` nele — confirme que a lista de bibliotecas bate com o ambiente virtual que você selecionou como interpretador.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

Não há código para essa tarefa — é um exercício de configuração. O sinal de que deu tudo certo é:

- O canto inferior direito do VS Code mostra o caminho do interpretador do seu ambiente virtual (não o Python global do sistema).
- Rodar um arquivo `.py` com `print()` mostra o resultado no terminal integrado, sem erros de "comando não encontrado" ou "módulo não encontrado".
- `pip list` no terminal integrado mostra as mesmas bibliotecas que você instalou dentro daquele ambiente virtual específico.

</details>

## Checklist antes de avançar

- [ ] Instalei as extensões Python e Jupyter no VS Code
- [ ] Consigo selecionar corretamente o interpretador de um ambiente virtual
- [ ] Consigo rodar um arquivo `.py` e ver o resultado no terminal integrado
