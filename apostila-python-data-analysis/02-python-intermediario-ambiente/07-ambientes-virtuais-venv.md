# Ambientes virtuais (venv)

> Módulo 2 — Python Intermediário e Ambiente · Tópico 7 de 11

## O que é e por que importa

Imagine que você tem dois projetos no seu computador: o da Loja da Ana, que usa `pandas` versão `2.1.0`, e outro projeto antigo de um cliente, que só funciona com `pandas` versão `1.3.0`. Se você instalar as bibliotecas com `pip install` "no computador todo" (o que chamamos de Python "global"), só é possível ter **uma** versão de cada biblioteca instalada por vez — instalar a versão nova para um projeto quebra o outro.

Um **ambiente virtual** resolve isso criando uma "caixa" isolada de Python e bibliotecas para cada projeto. Pensa nele como uma gaveta separada para cada projeto: dentro da gaveta da Loja da Ana, você guarda a versão de pandas que aquele projeto precisa; em outra gaveta, outro projeto guarda a versão que ele precisa — e as duas gavetas nunca se misturam. `venv` é o módulo embutido do Python que cria essas "gavetas".

Isolar dependências por projeto é uma das práticas mais básicas (e mais importantes) no dia a dia de quem trabalha com dados: evita o clássico problema de "no meu computador funciona" quando alguém tenta rodar seu código em outra máquina, e evita que atualizar uma biblioteca para um projeto novo quebre silenciosamente um projeto antigo.

## Como funciona (com exemplo comentado)

Todos os comandos abaixo rodam no terminal, dentro da pasta do seu projeto:

```bash
# Cria um ambiente virtual chamado "venv" (o nome é uma convenção, pode ser
# qualquer nome, mas "venv" é o mais usado) dentro da pasta atual do projeto
python -m venv venv

# No Windows, ativa o ambiente virtual (PowerShell)
venv\Scripts\Activate.ps1

# No Windows, ativa o ambiente virtual (cmd.exe)
venv\Scripts\activate.bat

# No Mac/Linux, ativa o ambiente virtual
source venv/bin/activate

# Depois de ativado, o nome do ambiente aparece entre parênteses no início da
# linha do terminal, algo como:
# (venv) C:\Users\voce\loja-da-ana>

# Com o ambiente ativado, qualquer "pip install" instala SÓ dentro dessa gaveta,
# sem afetar o Python do resto do computador nem outros projetos
pip install pandas==2.1.0

# Para sair do ambiente virtual e voltar ao Python "global"
deactivate
```

Passo a passo típico para começar um projeto novo:

1. Crie a pasta do projeto (ex: `loja-da-ana-analise`).
2. Dentro dela, rode `python -m venv venv` para criar o ambiente.
3. Ative o ambiente (`venv\Scripts\Activate.ps1` no Windows/PowerShell).
4. Instale as bibliotecas que o projeto precisa (`pip install pandas`).
5. Trabalhe normalmente — sempre que voltar a esse projeto em outro dia, ative o ambiente de novo antes de rodar ou instalar algo.
6. Ao terminar a sessão de trabalho, rode `deactivate` (opcional — fechar o terminal também "desativa" o ambiente).

## Erros comuns de quem está começando

- Esquecer de ativar o ambiente virtual antes de instalar uma biblioteca — nesse caso, o `pip install` vai direto para o Python global, e não para a "gaveta" do projeto.
- Colocar a pasta `venv` dentro do controle de versão do projeto (ex: subir ela para o Git). Ela é pesada e específica da sua máquina — o correto é listar as bibliotecas em um `requirements.txt` (visto em `06-pip.md`) e deixar cada pessoa criar seu próprio ambiente virtual.
- Achar que criar o ambiente virtual (`python -m venv venv`) já é suficiente. É preciso **ativar** o ambiente (`Activate.ps1` ou equivalente) toda vez que for usá-lo — criar só prepara a gaveta, ativar é "entrar" nela.

## Exercício prático

No seu computador, dentro de uma pasta de teste:

1. Crie um ambiente virtual chamado `venv` com `python -m venv venv`.
2. Ative o ambiente (use o comando correspondente ao seu sistema operacional).
3. Confirme que o ambiente está ativo (o nome deve aparecer entre parênteses no terminal).
4. Instale uma biblioteca qualquer, por exemplo `pip install requests`.
5. Rode `pip list` e confirme que `requests` aparece na lista.
6. Desative o ambiente com `deactivate`.

**Desafio bônus (opcional):** com o ambiente ativado, rode `pip freeze > requirements.txt` (visto em `06-pip.md`) e abra o arquivo gerado para ver o que foi salvo.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```bash
# 1. Criar o ambiente
python -m venv venv

# 2. Ativar (exemplo Windows PowerShell)
venv\Scripts\Activate.ps1

# 3. Confirmar ativação -- o terminal deve mostrar algo como:
# (venv) C:\pasta-de-teste>

# 4. Instalar biblioteca
pip install requests

# 5. Listar bibliotecas instaladas
pip list
# deve aparecer "requests" na lista

# 6. Desativar
deactivate
```

Se todos os passos rodaram sem erro e `requests` apareceu isolado nesse ambiente (sem afetar outros projetos), o exercício foi concluído com sucesso.

</details>

## Checklist antes de avançar

- [ ] Consigo explicar com minhas próprias palavras por que isolar dependências por projeto é importante
- [ ] Consegui criar e ativar um ambiente virtual no meu computador
- [ ] Entendo a diferença entre "criar" e "ativar" um ambiente virtual
