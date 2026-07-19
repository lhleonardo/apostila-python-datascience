# Strings (fundamentos)

> Módulo 1 — Fundamentos de Python · Tópico 13 de 25

## O que é e por que importa

String é o tipo de dado usado para texto: nomes, endereços, descrições de produtos, categorias. Em Python, o tipo se chama `str`, e você já usou strings desde o primeiro tópico, sempre que escreveu algo entre aspas, como `"Loja da Ana"`.

Em análise de dados, uma parte enorme do trabalho é com texto: nome de clientes, nome de produtos, categorias de venda, respostas abertas de pesquisas. Diferente de números, texto tem particularidades próprias — você pode juntar duas strings, pegar um pedaço específico dela, contar quantos caracteres tem, e muito mais (isso será aprofundado em `14-metodos-de-string.md` e `15-strip-replace-split.md`).

Uma ideia importante deste tópico é a de "índice": cada caractere de uma string tem uma posição numerada, começando em 0 (igual ao `range()` visto em `12-loops.md`). Isso permite pegar pedaços específicos do texto, como as três primeiras letras de um nome.

## Como funciona (com exemplo comentado)

```python
nome_produto = "Caneta Azul"

# Strings podem usar aspas simples ou duplas -- tanto faz, desde que combinem no início e no fim
categoria = 'Papelaria'

# Concatenação: juntar strings com +
descricao = nome_produto + " - " + categoria
print(descricao)  # Caneta Azul - Papelaria

# len() mede o comprimento de uma string (quantos caracteres tem)
tamanho_nome = len(nome_produto)
print("Tamanho do nome do produto:", tamanho_nome)

# Indexação: cada caractere tem uma posição, começando em 0
primeira_letra = nome_produto[0]
print("Primeira letra:", primeira_letra)  # C

# Índices negativos contam a partir do final (-1 é o último caractere)
ultima_letra = nome_produto[-1]
print("Última letra:", ultima_letra)  # l

# Fatiamento (slicing): pegar um pedaço da string, do índice inicial (incluso)
# até o final (excluso)
primeiras_6_letras = nome_produto[0:6]
print("Primeiras 6 letras:", primeiras_6_letras)  # Caneta

# f-strings: forma moderna e prática de montar mensagens com valores dentro do texto
preco = 5.90
mensagem = f"O produto {nome_produto} custa R$ {preco}"
print(mensagem)
```

## Erros comuns de quem está começando

- Esquecer que índices começam em 0, não em 1. `nome_produto[1]` pega o segundo caractere, não o primeiro.
- Tentar concatenar string com número diretamente (`"Total: " + 10`), o que gera erro. É preciso converter o número para string primeiro com `str()` (visto em `07-conversao-de-tipos.md`), ou usar f-string, que faz essa conversão automaticamente.
- Achar que fatiamento (`[0:6]`) inclui o índice final. `nome_produto[0:6]` pega os caracteres nas posições 0 a 5 — a posição 6 fica de fora.

## Exercício prático

A Loja da Ana tem um produto chamado `"Caderno Universitário 96 folhas"`.

1. Descubra e mostre quantos caracteres tem esse nome, usando `len()`.
2. Mostre apenas a palavra `"Caderno"` usando fatiamento (`[0:7]`).
3. Monte e mostre uma f-string com a frase: `"O produto Caderno Universitário 96 folhas tem 32 caracteres"` (usando os valores calculados, não digitando o número na mão).

**Desafio bônus (opcional):** mostre o último caractere do nome do produto usando índice negativo, e explique (num comentário) por que ele é um espaço em branco ou uma letra, dependendo de como você escreveu a string.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
nome_produto = "Caderno Universitário 96 folhas"

# Contando os caracteres
tamanho = len(nome_produto)
print("Tamanho do nome:", tamanho)

# Pegando apenas "Caderno" com fatiamento
palavra_inicial = nome_produto[0:7]
print("Primeira palavra:", palavra_inicial)

# Montando a frase com f-string, reaproveitando as variáveis calculadas
mensagem = f"O produto {nome_produto} tem {tamanho} caracteres"
print(mensagem)

# Desafio bônus
ultimo_caractere = nome_produto[-1]
print("Último caractere:", repr(ultimo_caractere))
# repr() aqui só ajuda a visualizar se é uma letra ou um espaço em branco,
# já que print() sozinho não deixa espaços visíveis com clareza
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar o que é uma string e um índice com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Sei usar fatiamento (`[inicio:fim]`) para pegar um pedaço de um texto
