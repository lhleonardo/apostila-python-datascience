# Trabalhando com strings (métodos gerais)

> Módulo 1 — Fundamentos de Python · Tópico 14 de 25

## O que é e por que importa

Método é uma "ação" que um valor sabe executar em si mesmo. A sintaxe é `valor.metodo()` — por exemplo, `"ana".upper()` transforma o texto em maiúsculas. Pensa em método como um "botão" que já vem embutido no próprio dado: toda string em Python já nasce com um conjunto de botões prontos para maiúsculas, minúsculas, busca de palavras etc. (a diferença formal entre "função" e "método" será explicada com calma em `21-funcoes-e-metodos.md` — por ora, use método como "uma função que pertence a um valor").

Em análise de dados, texto quase nunca chega "limpo": nomes de clientes com maiúsculas trocadas, categorias de produto escritas de formas diferentes ("papelaria", "Papelaria", "PAPELARIA"), espaços a mais. Métodos de string são a ferramenta para padronizar e investigar esse texto antes de usá-lo em qualquer análise.

Este tópico cobre os métodos mais gerais de string. Os métodos de "limpeza e separação" mais usados em dados (`strip`, `replace`, `split`) ganham um tópico próprio, `15-strip-replace-split.md`, porque merecem atenção especial.

## Como funciona (com exemplo comentado)

```python
nome_cliente = "  ana Paula Da Silva  "

# upper() deixa tudo maiúsculo, lower() deixa tudo minúsculo
print(nome_cliente.upper())   # "  ANA PAULA DA SILVA  "
print(nome_cliente.lower())   # "  ana paula da silva  "

# title() deixa a primeira letra de cada palavra maiúscula (bom para nomes próprios)
print(nome_cliente.title())   # "  Ana Paula Da Silva  "

# Métodos não alteram a string original -- eles retornam uma nova string
print(nome_cliente)  # continua com espaços e caixa original

# Padronizar texto para comparação é um uso comum em análise de dados
categoria_1 = "Papelaria"
categoria_2 = "PAPELARIA"
sao_a_mesma_categoria = categoria_1.lower() == categoria_2.lower()
print("São a mesma categoria?", sao_a_mesma_categoria)  # True

# in verifica se um texto contém outro pedaço de texto
descricao_produto = "Caneta esferográfica azul, ponta fina"
tem_palavra_azul = "azul" in descricao_produto
print("Descrição menciona 'azul'?", tem_palavra_azul)  # True

# startswith() e endswith() checam início e fim do texto
codigo_produto = "PAP-001"
eh_da_papelaria = codigo_produto.startswith("PAP")
print("Código é da categoria papelaria?", eh_da_papelaria)  # True

# count() conta quantas vezes um pedaço aparece no texto
qtd_letra_a = nome_cliente.lower().count("a")
print("Quantidade de 'a' no nome:", qtd_letra_a)
```

## Erros comuns de quem está começando

- Achar que `.upper()` (ou qualquer método de string) muda a variável original. Strings em Python são "imutáveis" — o método sempre devolve uma string nova, então é preciso guardar o resultado em uma variável (`nome = nome.upper()`) se quiser manter a mudança.
- Comparar textos sem padronizar maiúsculas/minúsculas antes, e concluir erroneamente que "Papelaria" e "papelaria" são categorias diferentes.
- Esquecer o parênteses ao chamar um método, escrevendo `nome_cliente.upper` em vez de `nome_cliente.upper()`. Sem os parênteses, o Python não executa o método, apenas referencia ele.

## Exercício prático

A Loja da Ana recebeu os seguintes nomes de clientes de um cadastro malfeito, com maiúsculas inconsistentes:

```python
clientes = ["ANA SILVA", "bruno costa", "Carla Dias"]
```

(Vamos usar listas de verdade em breve, em `16-listas.md` — por ora, trate cada nome como uma string separada.)

1. Usando os três nomes acima como variáveis separadas (`cliente_1`, `cliente_2`, `cliente_3`), padronize todos para o formato "Nome Sobrenome" (primeira letra maiúscula) usando `.title()`.
2. Verifique, para cada nome padronizado, se ele contém a palavra `"Silva"` usando o operador `in`.

**Desafio bônus (opcional):** conte quantas vezes a letra `"a"` aparece em cada nome (ignorando maiúsculas/minúsculas).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
cliente_1 = "ANA SILVA"
cliente_2 = "bruno costa"
cliente_3 = "Carla Dias"

# Padronizando com .title()
cliente_1_padronizado = cliente_1.title()
cliente_2_padronizado = cliente_2.title()
cliente_3_padronizado = cliente_3.title()

print(cliente_1_padronizado)
print(cliente_2_padronizado)
print(cliente_3_padronizado)

# Verificando se contém "Silva"
print("Contém 'Silva'?", "Silva" in cliente_1_padronizado)
print("Contém 'Silva'?", "Silva" in cliente_2_padronizado)
print("Contém 'Silva'?", "Silva" in cliente_3_padronizado)

# Desafio bônus: contando letra "a", ignorando caixa
print(cliente_1.lower().count("a"))
print(cliente_2.lower().count("a"))
print(cliente_3.lower().count("a"))
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar o que é um método (`valor.metodo()`) com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Entendo que métodos de string retornam um valor novo, sem alterar o original
