# Funções e métodos (diferença entre os dois)

> Módulo 1 — Fundamentos de Python · Tópico 21 de 25

## O que é e por que importa

Você já usou os dois conceitos deste tópico sem uma explicação formal: funções, como `print()`, `len()`, `sum()`, `int()`; e métodos, como `.upper()`, `.strip()`, `.append()` (vistos em `14-metodos-de-string.md` e `16-listas.md`). Chegou a hora de formalizar a diferença entre eles, porque isso ajuda a entender qualquer código Python que você ler daqui para frente.

Uma função é independente: ela existe "solta" e você a chama passando o que ela precisa entre parênteses, como `len(nome_produto)` — aqui, `len` é a função, e `nome_produto` é o dado que ela processa. Já um método é uma função que "pertence" a um valor específico e só pode ser chamada a partir dele, com a sintaxe `valor.metodo()` — como `nome_produto.upper()`, onde `upper()` só existe porque `nome_produto` é uma string, e strings sabem se transformar em maiúsculas.

Pensa assim: função é uma ferramenta genérica na caixa de ferramentas (qualquer coisa compatível pode usar); método é uma habilidade que só um tipo específico de objeto tem (só string sabe fazer `.upper()`, só lista sabe fazer `.append()`). Entender essa diferença evita a confusão comum de tentar chamar `upper(nome_produto)` (função, errado) ou `len.nome_produto()` (método, errado) — e também prepara terreno para `22-definindo-funcoes.md`, onde você vai aprender a criar suas próprias funções.

## Como funciona (com exemplo comentado)

```python
nome_produto = "  caneta azul  "

# Função: chamada como algo_independente(valor)
tamanho = len(nome_produto)          # len() é função, funciona com string, lista, dict...
print("Tamanho (com espaços):", tamanho)

tipo_do_dado = type(nome_produto)    # type() também é função
print("Tipo do dado:", tipo_do_dado)

# Método: chamado como valor.algo_do_valor()
nome_limpo = nome_produto.strip()    # strip() é método, só existe porque é uma string
nome_maiusculo = nome_limpo.upper()  # upper() também é método de string
print(nome_maiusculo)

# Um mesmo nome pode existir como função OU como método, com comportamentos diferentes.
# Por exemplo, não existe "sort" como função solta para ordenar qualquer coisa da mesma forma,
# mas listas têm o método .sort():
vendas = [45.90, 120.00, 15.50, 200.00]
vendas.sort()  # método -- ordena a própria lista
print(vendas)

# Já a função sorted() (função, não método) funciona em várias coleções e devolve uma lista nova
vendas_originais = [45.90, 120.00, 15.50, 200.00]
vendas_ordenadas = sorted(vendas_originais)  # função -- não altera a lista original
print("Original:", vendas_originais)
print("Ordenada (nova lista):", vendas_ordenadas)

# Métodos podem ser "encadeados" um atrás do outro, já que cada um devolve um novo valor
nome_formatado = "  ana silva  ".strip().title()
print(nome_formatado)  # "Ana Silva"
```

## Erros comuns de quem está começando

- Tentar chamar um método como se fosse função, escrevendo `upper(nome_produto)` em vez de `nome_produto.upper()`. Métodos sempre precisam do valor "dono" antes do ponto.
- Achar que todo tipo de dado tem os mesmos métodos. `.upper()` só existe em string; tentar usar em uma lista ou número gera erro `AttributeError`.
- Confundir método que altera o valor original (como `.append()` e `.sort()` em listas) com método que devolve um valor novo sem alterar o original (como `.upper()` em strings, ou `sorted()`, que é função). Vale sempre checar a documentação ou testar quando tiver dúvida.

## Exercício prático

Considere a string `"  Loja Da ANA  "` e a lista `[89.90, 45.00, 200.00, 15.50]`.

1. Use uma função para descobrir quantos caracteres tem a string original (com espaços).
2. Use métodos encadeados para limpar os espaços e formatar a string no padrão "Título" (primeira letra de cada palavra maiúscula).
3. Use uma função (não método) para criar uma nova lista ordenada a partir da lista de vendas, sem alterar a lista original.
4. Mostre a lista original e a lista ordenada lado a lado, para confirmar que a original não mudou.

**Desafio bônus (opcional):** explique, em um comentário no código, por que `sorted(lista)` é uma função e `lista.sort()` é um método, e qual a diferença prática de efeito colateral entre os dois.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
texto = "  Loja Da ANA  "
vendas = [89.90, 45.00, 200.00, 15.50]

# Função len() para contar caracteres (com espaços)
tamanho_com_espacos = len(texto)
print("Tamanho com espaços:", tamanho_com_espacos)

# Métodos encadeados: strip() remove espaços, title() padroniza capitalização
texto_formatado = texto.strip().title()
print("Texto formatado:", texto_formatado)

# Função sorted() cria uma lista NOVA ordenada, sem mexer na original
vendas_ordenadas = sorted(vendas)

print("Lista original:", vendas)
print("Lista ordenada (nova):", vendas_ordenadas)

# Desafio bônus:
# sorted(lista) é uma função porque não "pertence" a nenhum tipo específico --
# ela recebe qualquer coleção e devolve uma lista nova, sem alterar a original.
# lista.sort() é um método porque só listas o possuem, e ele altera a própria
# lista (efeito colateral), não devolvendo nada de útil (devolve None).
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar a diferença entre função e método com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Sei identificar, olhando o código, se algo é uma função ou um método
