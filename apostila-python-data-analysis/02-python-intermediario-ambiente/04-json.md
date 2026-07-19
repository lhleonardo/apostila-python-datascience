# JSON (ler e escrever)

> Módulo 2 — Python Intermediário e Ambiente · Tópico 4 de 11

## O que é e por que importa

JSON (*JavaScript Object Notation*) é um formato de texto para guardar dados estruturados em arquivo — parecido com os dicionários e listas que você já conhece do Módulo 1, só que salvo como um arquivo `.json` que pode ser lido por praticamente qualquer linguagem de programação, não só Python. É um dos formatos mais usados hoje para troca de dados entre sistemas (uma API de e-commerce, por exemplo, costuma devolver informações em JSON).

Pensa em JSON como uma "foto" de um dicionário Python guardada em disco: se você tem `{"nome": "Caneta Azul", "preco": 2.50}` na memória do seu programa, o JSON é a versão desse mesmo conteúdo salva em um arquivo de texto, para você poder fechar o programa hoje e abrir o mesmo dado amanhã (ou mandar esse arquivo para outra pessoa).

Até agora, os dados da Loja da Ana existiam só enquanto o script rodava — ao fechar o programa, tudo se perdia. A partir de agora, vamos guardar os dados de vendas, produtos e clientes em arquivos, para simular como isso funciona de verdade no mercado de trabalho. O módulo `json`, embutido no Python, converte dicionários e listas Python em texto JSON (e vice-versa) automaticamente.

## Como funciona (com exemplo comentado)

```python
import json  # módulo embutido, não precisa instalar nada

produto = {
    "nome": "Caneta Azul",
    "preco": 2.50,
    "quantidade_em_estoque": 100,
    "categoria": "Papelaria",
}

# json.dumps converte um dicionário/lista Python em uma STRING no formato JSON
# ("dumps" = "dump string", ou seja, "despeje como string")
texto_json = json.dumps(produto, indent=2)  # indent=2 deixa o texto formatado, mais legível
print(texto_json)

# json.dump faz a mesma coisa, mas escreve DIRETO em um arquivo
with open("produto.json", "w", encoding="utf-8") as arquivo:
    # "w" significa "write" (escrever) -- se o arquivo já existir, ele é sobrescrito
    json.dump(produto, arquivo, indent=2, ensure_ascii=False)
    # ensure_ascii=False permite salvar acentos e caracteres especiais corretamente

# json.load lê um arquivo .json e devolve um dicionário/lista Python pronto para uso
with open("produto.json", "r", encoding="utf-8") as arquivo:
    # "r" significa "read" (ler)
    produto_carregado = json.load(arquivo)

print(produto_carregado["nome"])   # Caneta Azul
print(type(produto_carregado))     # <class 'dict'>

# json.loads (com "s" no final) faz o mesmo que json.load, mas a partir de uma STRING
# que já está na memória, não de um arquivo aberto
texto_recebido = '{"nome": "Mochila", "preco": 89.90}'
produto_2 = json.loads(texto_recebido)
print(produto_2["preco"])  # 89.9

# JSON também guarda listas de dicionários -- útil para uma base inteira de vendas
vendas = [
    {"produto": "Caneta Azul", "quantidade": 3, "total": 7.50},
    {"produto": "Caderno", "quantidade": 1, "total": 15.90},
]

with open("vendas.json", "w", encoding="utf-8") as arquivo:
    json.dump(vendas, arquivo, indent=2, ensure_ascii=False)

with open("vendas.json", "r", encoding="utf-8") as arquivo:
    vendas_carregadas = json.load(arquivo)

for venda in vendas_carregadas:
    print(venda["produto"], "-", venda["total"])
```

Repare no `with open(...) as arquivo:` — essa construção abre o arquivo, executa o bloco indentado, e fecha o arquivo automaticamente no final (mesmo se der erro no meio do caminho). É a forma recomendada de trabalhar com arquivos em Python.

## Erros comuns de quem está começando

- Usar `"w"` (write) quando queria `"r"` (read), ou vice-versa. Abrir para escrita (`"w"`) em um arquivo que já tem dados importantes **apaga o conteúdo anterior**.
- Confundir `json.dump`/`json.load` (trabalham com **arquivos** abertos) com `json.dumps`/`json.loads` (trabalham com **strings** na memória). O "s" extra no nome é a pista: "s" de string.
- Esquecer `encoding="utf-8"` ao abrir arquivos com acentos (nomes de produtos, cidades etc.) — em alguns sistemas isso causa erro ou caracteres corrompidos ao salvar/ler.

## Exercício prático

Crie um dicionário representando um cliente da Loja da Ana, com as chaves `"nome"`, `"email"` e `"total_gasto"`. Salve esse dicionário em um arquivo chamado `cliente.json` usando `json.dump`. Depois, em outra parte do código, leia o arquivo de volta com `json.load` e imprima o nome do cliente carregado.

**Desafio bônus (opcional):** crie uma lista com três clientes (dicionários) e salve todos em um único arquivo `clientes.json`. Depois carregue o arquivo e, usando um `for`, imprima só os nomes dos clientes que têm `total_gasto` maior que R$ 300.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import json

cliente = {
    "nome": "Marcos Silva",
    "email": "marcos@email.com",
    "total_gasto": 320.00,
}

with open("cliente.json", "w", encoding="utf-8") as arquivo:
    json.dump(cliente, arquivo, indent=2, ensure_ascii=False)

with open("cliente.json", "r", encoding="utf-8") as arquivo:
    cliente_carregado = json.load(arquivo)

print(cliente_carregado["nome"])

# Desafio bônus
clientes = [
    {"nome": "Marcos", "total_gasto": 320.00},
    {"nome": "Julia", "total_gasto": 550.00},
    {"nome": "Beto", "total_gasto": 120.00},
]

with open("clientes.json", "w", encoding="utf-8") as arquivo:
    json.dump(clientes, arquivo, indent=2, ensure_ascii=False)

with open("clientes.json", "r", encoding="utf-8") as arquivo:
    clientes_carregados = json.load(arquivo)

for c in clientes_carregados:
    if c["total_gasto"] > 300:
        print(c["nome"])
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar a diferença entre `json.dump`/`load` e `json.dumps`/`loads`
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Entendo por que `"w"` sobrescreve o conteúdo de um arquivo
