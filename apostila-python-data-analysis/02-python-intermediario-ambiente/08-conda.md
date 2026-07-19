# Conda (alternativa ao venv)

> Módulo 2 — Python Intermediário e Ambiente · Tópico 8 de 11

## O que é e por que importa

No tópico anterior (`07-ambientes-virtuais-venv.md`) você viu que `venv` cria "gavetas" isoladas de bibliotecas Python por projeto. `conda` resolve o mesmo problema — isolar dependências por projeto — mas com uma diferença importante: `conda` não gerencia só bibliotecas Python, ele gerencia **pacotes de qualquer tipo**, incluindo o próprio Python (diferentes versões dele) e bibliotecas que dependem de código escrito em outras linguagens (como C ou Fortran), muito comuns em bibliotecas científicas e de dados.

Pensa assim: `venv` é como uma gaveta dentro de um guarda-roupa que já é seu (o Python que você já tem instalado). `conda` é como um guarda-roupa completo e independente, que você pode montar do zero, escolhendo até que "modelo" de Python vai morar ali dentro. Isso é útil especialmente em bibliotecas de dados e ciência (numpy, pandas, scipy) que às vezes dependem de componentes que não são Python puro — o `conda` sabe instalar essas peças extras sozinho, enquanto o `pip`/`venv` às vezes exige que você instale essas peças manualmente no sistema operacional.

`conda` vem geralmente através da distribuição **Anaconda** (ou sua versão mais enxuta, **Miniconda**) — um pacote de instalação que já traz Python, `conda` e várias bibliotecas de dados populares pré-instaladas, muito usado por quem trabalha com ciência de dados e machine learning.

## Como funciona (com exemplo comentado)

Depois de instalar Anaconda ou Miniconda, os comandos rodam no terminal (no Windows, geralmente em um terminal específico chamado "Anaconda Prompt"):

```bash
# Cria um ambiente conda chamado "loja-da-ana", já especificando a versão do Python
conda create --name loja-da-ana python=3.11

# Ativa o ambiente -- note que o comando é diferente do venv
conda activate loja-da-ana

# Com o ambiente ativado, instala pacotes -- pode usar "conda install" ou "pip install"
conda install pandas numpy matplotlib

# Lista todos os ambientes conda já criados no seu computador
conda env list

# Lista os pacotes instalados no ambiente ativo no momento
conda list

# Desativa o ambiente atual, voltando ao ambiente "base"
conda deactivate

# Remove um ambiente que não é mais necessário
conda env remove --name loja-da-ana
```

Quando escolher um ou outro, na prática:

- Use **venv** quando seu projeto usa só bibliotecas Python "normais" (a maioria dos casos) e você já tem Python instalado — é mais leve e já vem embutido, sem precisar instalar nada extra.
- Use **conda** quando trabalha bastante com bibliotecas científicas pesadas (numpy, scipy, bibliotecas de machine learning), quando precisa alternar entre várias versões diferentes do próprio Python facilmente, ou quando alguma biblioteca exige componentes que não são Python puro e o `pip` sozinho tem dificuldade de instalar.

Para o restante desta apostila, `venv` é suficiente — mas é comum encontrar `conda` no mercado de trabalho, especialmente em times de ciência de dados, então vale reconhecer os comandos.

## Erros comuns de quem está começando

- Achar que precisa escolher entre `venv` OU `conda` para sempre. É perfeitamente normal usar `conda` em um projeto e `venv` em outro, dependendo da necessidade.
- Misturar `conda install` e `pip install` sem entender a ordem — em geral, é mais seguro instalar tudo que der com `conda install` primeiro, e só usar `pip install` para o que não estiver disponível via `conda`.
- Esquecer de ativar o ambiente conda certo antes de instalar algo (igual ao erro equivalente no `venv`) — os comandos `conda install` sem um ambiente ativado adequado vão parar no ambiente errado.

## Exercício prático

Sem precisar instalar nada (a menos que já tenha Anaconda/Miniconda e queira testar de verdade), escreva os comandos que você usaria para:

1. Criar um ambiente conda chamado `analise-vendas` com Python 3.10.
2. Ativar esse ambiente.
3. Instalar `pandas` e `matplotlib` dentro dele.
4. Listar todos os ambientes conda existentes no computador.

**Desafio bônus (opcional):** pesquise a diferença entre Anaconda e Miniconda e escreva, em uma frase, qual delas você instalaria em um computador com pouco espaço em disco e por quê.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```bash
# 1. Criar o ambiente
conda create --name analise-vendas python=3.10

# 2. Ativar
conda activate analise-vendas

# 3. Instalar bibliotecas
conda install pandas matplotlib

# 4. Listar ambientes existentes
conda env list
```

Desafio bônus: Miniconda é uma versão enxuta que traz só o essencial (Python + conda), sem as dezenas de bibliotecas pré-instaladas do Anaconda completo — é a escolha melhor para pouco espaço em disco, já que você instala só o que realmente vai usar.

</details>

## Checklist antes de avançar

- [ ] Consigo explicar a principal diferença entre `conda` e `venv`
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Sei em que situação faria mais sentido escolher `conda` em vez de `venv`
