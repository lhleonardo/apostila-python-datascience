# Lista de exercícios — Módulo 2

> Módulo 2 — Python Intermediário e Ambiente · Lista de exercícios de revisão

Esta lista reúne 10 exercícios práticos para cada tópico do módulo, para
consolidar o que foi aprendido antes de avançar. Tente resolver cada
exercício sem consultar o tópico original primeiro — as soluções vêm logo
depois de cada bloco, dentro de um "clique para ver".

## 1. OOP para análise de dados

1. Crie uma classe `Produto` com `__init__` recebendo `nome` e `preco`. Crie um objeto `Produto("Caneta", 2.50)` e imprima seus atributos.
2. Adicione à classe `Produto` um método `aplicar_desconto(percentual)` que reduz o preço proporcionalmente. Teste aplicando 10% de desconto.
3. Crie uma classe `Estoque` com `__init__` recebendo `quantidade`. Adicione um método `esta_em_falta()` que devolve `True` se `quantidade` for igual a zero.
4. Crie uma classe `Funcionario` com `nome` e `salario`. Adicione um método `aumentar_salario(percentual)` que atualiza `self.salario`.
5. Crie a classe `Produto` do exercício 1 com um atributo extra `categoria`. Crie três objetos diferentes e imprima o nome de todos os que são da categoria `"Papelaria"`.
6. Crie uma classe `CarrinhoDeCompras` com `__init__` iniciando uma lista vazia `self.itens`. Adicione um método `adicionar_item(nome, preco)` que guarda uma tupla `(nome, preco)` na lista.
7. Na classe `CarrinhoDeCompras` do exercício 6, adicione um método `total()` que soma o preço de todos os itens adicionados.
8. Crie uma classe `Vendedor` com `nome` e uma lista `vendas` (inicializada vazia). Adicione um método `registrar_venda(valor)` que adiciona o valor à lista, e um método `total_vendido()` que soma tudo.
9. Crie uma classe `Loja` que guarda uma lista de objetos `Produto` (da classe do exercício 1). Adicione um método `valor_total_estoque()` que soma o preço de todos os produtos cadastrados.
10. Combine as classes `Produto` e `Venda` vistas no tópico: crie três produtos diferentes, crie uma lista de vendas (objetos `Venda`) para cada um, e imprima o total de cada venda usando um `for`.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
class Produto:
    def __init__(self, nome, preco):
        self.nome = nome
        self.preco = preco

produto = Produto("Caneta", 2.50)
print(produto.nome, produto.preco)
```

**2.**
```python
class Produto:
    def __init__(self, nome, preco):
        self.nome = nome
        self.preco = preco

    def aplicar_desconto(self, percentual):
        self.preco = self.preco * (1 - percentual)

produto = Produto("Caneta", 2.50)
produto.aplicar_desconto(0.10)
print(produto.preco)  # 2.25
```

**3.**
```python
class Estoque:
    def __init__(self, quantidade):
        self.quantidade = quantidade

    def esta_em_falta(self):
        return self.quantidade == 0

estoque = Estoque(0)
print(estoque.esta_em_falta())  # True
```

**4.**
```python
class Funcionario:
    def __init__(self, nome, salario):
        self.nome = nome
        self.salario = salario

    def aumentar_salario(self, percentual):
        self.salario = self.salario * (1 + percentual)

func = Funcionario("Ana", 2000.00)
func.aumentar_salario(0.05)
print(func.salario)  # 2100.0
```

**5.**
```python
class Produto:
    def __init__(self, nome, preco, categoria):
        self.nome = nome
        self.preco = preco
        self.categoria = categoria

produtos = [
    Produto("Caneta", 2.50, "Papelaria"),
    Produto("Mochila", 89.90, "Acessorios"),
    Produto("Caderno", 15.90, "Papelaria"),
]

for produto in produtos:
    if produto.categoria == "Papelaria":
        print(produto.nome)
```

**6.**
```python
class CarrinhoDeCompras:
    def __init__(self):
        self.itens = []

    def adicionar_item(self, nome, preco):
        self.itens.append((nome, preco))

carrinho = CarrinhoDeCompras()
carrinho.adicionar_item("Caneta", 2.50)
carrinho.adicionar_item("Caderno", 15.90)
print(carrinho.itens)
```

**7.**
```python
class CarrinhoDeCompras:
    def __init__(self):
        self.itens = []

    def adicionar_item(self, nome, preco):
        self.itens.append((nome, preco))

    def total(self):
        soma = 0
        for nome, preco in self.itens:
            soma += preco
        return soma

carrinho = CarrinhoDeCompras()
carrinho.adicionar_item("Caneta", 2.50)
carrinho.adicionar_item("Caderno", 15.90)
print(carrinho.total())  # 18.4
```

**8.**
```python
class Vendedor:
    def __init__(self, nome):
        self.nome = nome
        self.vendas = []

    def registrar_venda(self, valor):
        self.vendas.append(valor)

    def total_vendido(self):
        return sum(self.vendas)

vendedor = Vendedor("Ana")
vendedor.registrar_venda(150.00)
vendedor.registrar_venda(320.00)
print(vendedor.total_vendido())  # 470.0
```

**9.**
```python
class Produto:
    def __init__(self, nome, preco):
        self.nome = nome
        self.preco = preco

class Loja:
    def __init__(self):
        self.produtos = []

    def adicionar_produto(self, produto):
        self.produtos.append(produto)

    def valor_total_estoque(self):
        return sum(produto.preco for produto in self.produtos)

loja = Loja()
loja.adicionar_produto(Produto("Caneta", 2.50))
loja.adicionar_produto(Produto("Mochila", 89.90))
print(loja.valor_total_estoque())  # 92.4
```

**10.**
```python
class Produto:
    def __init__(self, nome, preco):
        self.nome = nome
        self.preco = preco

class Venda:
    def __init__(self, produto, quantidade):
        self.produto = produto
        self.quantidade = quantidade

    def total(self):
        return self.produto.preco * self.quantidade

caneta = Produto("Caneta", 2.50)
caderno = Produto("Caderno", 15.90)
mochila = Produto("Mochila", 89.90)

vendas = [
    Venda(caneta, 5),
    Venda(caderno, 2),
    Venda(mochila, 1),
]

for venda in vendas:
    print(venda.produto.nome, "-", venda.total())
```

</details>

## 2. Módulo random

1. Importe o módulo `random` e use `random.choice` para sortear um item de uma lista com pelo menos 4 nomes de produtos.
2. Use `random.randint(1, 20)` para sortear a quantidade vendida de um produto e imprima o resultado.
3. Use `random.sample` para sortear 3 clientes diferentes de uma lista com pelo menos 6 nomes.
4. Use `random.uniform(5.0, 100.0)` para sortear um preço, arredondando o resultado para 2 casas decimais com `round()`.
5. Use `random.seed(3)` e depois `random.randint(1, 100)` duas vezes seguidas. Explique em um comentário por que os dois valores impressos serão sempre os mesmos toda vez que o script rodar.
6. Usando `random.seed(1)`, gere uma lista de 6 números inteiros aleatórios entre 1 e 10 com um `for`, guardando-os em uma lista chamada `numeros`.
7. Simule 10 vendas da Loja da Ana usando `random.seed(20)`: cada venda é um dicionário com `"produto"` (sorteado de uma lista de 5 produtos) e `"quantidade"` (entre 1 e 8). Imprima todas.
8. A partir da lista de vendas do exercício 7, use `random.sample` para sortear 3 vendas para uma "auditoria surpresa" e imprima só essas três.
9. Crie uma lista de 5 clientes e use `random.shuffle` para embaralhar a ordem da lista (consulte a documentação do módulo `random` se precisar). Imprima a lista embaralhada.
10. Simule uma base de 15 vendas com `random.seed(99)`, cada uma com `"produto"`, `"quantidade"` (1 a 10) e `"preco_unitario"` (entre 2.0 e 80.0, arredondado com `round`). Depois, calcule e imprima o faturamento total da base.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import random

produtos = ["Caneta", "Caderno", "Mochila", "Lapis"]
sorteado = random.choice(produtos)
print(sorteado)
```

**2.**
```python
import random

quantidade = random.randint(1, 20)
print(quantidade)
```

**3.**
```python
import random

clientes = ["Ana", "Beto", "Carla", "Diego", "Elisa", "Fabio"]
sorteados = random.sample(clientes, 3)
print(sorteados)
```

**4.**
```python
import random

preco = round(random.uniform(5.0, 100.0), 2)
print(preco)
```

**5.**
```python
import random

random.seed(3)
print(random.randint(1, 100))
print(random.randint(1, 100))
# Os valores são sempre os mesmos porque random.seed "trava" o ponto de
# partida do gerador de números aleatórios -- a sequência gerada a partir
# dali é sempre idêntica, na mesma ordem, toda vez que o script roda
```

**6.**
```python
import random

random.seed(1)
numeros = []
for _ in range(6):
    numeros.append(random.randint(1, 10))
print(numeros)
```

**7.**
```python
import random

random.seed(20)
produtos = ["Caneta", "Caderno", "Mochila", "Lapis", "Borracha"]

vendas = []
for _ in range(10):
    venda = {
        "produto": random.choice(produtos),
        "quantidade": random.randint(1, 8),
    }
    vendas.append(venda)

for venda in vendas:
    print(venda)
```

**8.**
```python
# continuando o exercício 7
auditadas = random.sample(vendas, 3)
print("Vendas selecionadas para auditoria:")
for venda in auditadas:
    print(venda)
```

**9.**
```python
import random

clientes = ["Ana", "Beto", "Carla", "Diego", "Elisa"]
random.shuffle(clientes)  # embaralha a lista "no lugar" (não devolve uma nova lista)
print(clientes)
```

**10.**
```python
import random

random.seed(99)
produtos = ["Caneta", "Caderno", "Mochila", "Lapis", "Borracha"]

vendas = []
for _ in range(15):
    venda = {
        "produto": random.choice(produtos),
        "quantidade": random.randint(1, 10),
        "preco_unitario": round(random.uniform(2.0, 80.0), 2),
    }
    vendas.append(venda)

faturamento_total = sum(v["quantidade"] * v["preco_unitario"] for v in vendas)
print("Faturamento total:", faturamento_total)
```

</details>

## 3. Expressões regulares (re) — nível básico

1. Use `re.search(r"\d+", ...)` para encontrar o primeiro número dentro do texto `"Pedido #789 confirmado"` e imprima o resultado com `.group()`.
2. Use `re.findall(r"\d+", ...)` para extrair todos os números do texto `"Total: 3 itens, R$ 45, entrega em 2 dias"`.
3. Use `re.match(r"[A-Z]{2}", ...)` para verificar se o código `"RJ12345"` começa com exatamente duas letras maiúsculas.
4. Escreva um padrão regex que valide se uma string de e-mail (`r"^[\w.]+@[\w.]+\.\w+$"`) bate com `"contato@lojadaana.com"`, imprimindo uma mensagem de válido/inválido.
5. Extraia o valor numérico do texto `"R$ 129,90"` usando `re.findall(r"\d+,\d+", ...)` e converta o resultado para `float` (trocando vírgula por ponto).
6. Dada a lista de descrições `["Cliente: Ana - Tel: 11987654321", "Cliente: Beto - Tel: 21912345678"]`, extraia apenas os números de telefone de cada uma usando `re.findall(r"\d+", ...)`.
7. Escreva uma função `codigo_valido(codigo)` que usa `re.match(r"^[A-Z]{3}\d{3}$", codigo)` para verificar se um código de produto tem exatamente 3 letras maiúsculas seguidas de 3 números (ex: `"CAN001"`). Teste com pelo menos 3 códigos diferentes.
8. Dada a lista `["ana@email.com", "beto-arroba-email.com", "carla@outro.com.br"]`, use um `for` e `re.match` com o padrão de e-mail visto no tópico para imprimir só os e-mails válidos.
9. Extraia, de cada string da lista `["Produto A: R$ 10,50", "Produto B: R$ 200,00", "Produto C: R$ 5,99"]`, o nome do produto (tudo antes dos dois-pontos) e o preço, usando `re.findall` separadamente para letras/espaços e para o padrão de preço.
10. Dada a lista de pedidos `["Pedido #101 - Caderno", "Pedido #204 - Caneta", "Pedido #999 - Mochila"]`, extraia os números de pedido, valide com `re.match(r"^\d{3}$", ...)` se cada um tem exatamente 3 dígitos, e imprima só os pedidos cujo número é maior que 200 (convertendo para `int`).

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import re

texto = "Pedido #789 confirmado"
resultado = re.search(r"\d+", texto)
if resultado:
    print(resultado.group())  # 789
```

**2.**
```python
import re

texto = "Total: 3 itens, R$ 45, entrega em 2 dias"
numeros = re.findall(r"\d+", texto)
print(numeros)  # ['3', '45', '2']
```

**3.**
```python
import re

codigo = "RJ12345"
if re.match(r"[A-Z]{2}", codigo):
    print("Código começa com 2 letras maiúsculas")
else:
    print("Formato inválido")
```

**4.**
```python
import re

email = "contato@lojadaana.com"
padrao = r"^[\w.]+@[\w.]+\.\w+$"
if re.match(padrao, email):
    print("E-mail válido")
else:
    print("E-mail inválido")
```

**5.**
```python
import re

texto = "R$ 129,90"
valor = re.findall(r"\d+,\d+", texto)[0]
valor_float = float(valor.replace(",", "."))
print(valor_float)  # 129.9
```

**6.**
```python
import re

descricoes = [
    "Cliente: Ana - Tel: 11987654321",
    "Cliente: Beto - Tel: 21912345678",
]

for descricao in descricoes:
    telefone = re.findall(r"\d+", descricao)[0]
    print(telefone)
```

**7.**
```python
import re

def codigo_valido(codigo):
    return re.match(r"^[A-Z]{3}\d{3}$", codigo) is not None

print(codigo_valido("CAN001"))   # True
print(codigo_valido("can001"))   # False
print(codigo_valido("CAN01"))    # False
```

**8.**
```python
import re

emails = ["ana@email.com", "beto-arroba-email.com", "carla@outro.com.br"]
padrao = r"^[\w.]+@[\w.]+\.\w+$"

for email in emails:
    if re.match(padrao, email):
        print(email)
```

**9.**
```python
import re

produtos = ["Produto A: R$ 10,50", "Produto B: R$ 200,00", "Produto C: R$ 5,99"]

for item in produtos:
    nome = re.findall(r"^[\w\s]+(?=:)", item)[0]
    preco = re.findall(r"\d+,\d+", item)[0]
    print(nome.strip(), "-", preco)
```

**10.**
```python
import re

pedidos = [
    "Pedido #101 - Caderno",
    "Pedido #204 - Caneta",
    "Pedido #999 - Mochila",
]

for pedido in pedidos:
    numero = re.findall(r"\d+", pedido)[0]
    if re.match(r"^\d{3}$", numero) and int(numero) > 200:
        print(pedido)
```

</details>

## 4. JSON (ler e escrever)

1. Crie um dicionário representando um produto (`"nome"`, `"preco"`, `"quantidade_em_estoque"`) e imprima sua versão em texto JSON usando `json.dumps(produto, indent=2)`.
2. Salve o dicionário do exercício 1 em um arquivo `produto_ex.json` usando `json.dump`, com `encoding="utf-8"` e `ensure_ascii=False`.
3. Leia de volta o arquivo `produto_ex.json` usando `json.load` e imprima o tipo do valor retornado (`type(...)`).
4. Use `json.loads` para converter a string `'{"nome": "Mochila", "preco": 89.90}'` em um dicionário Python e imprima o preço.
5. Crie uma lista com 3 dicionários de produtos e salve tudo em um arquivo `produtos_ex.json` de uma vez, usando `json.dump`.
6. Leia o arquivo `produtos_ex.json` do exercício 5 e, usando um `for`, imprima só o nome de cada produto.
7. Crie um dicionário de cliente com `"nome"`, `"email"` e `"total_gasto"`. Salve em `cliente_ex.json`, leia de volta, e imprima uma mensagem dizendo se o cliente é VIP (`total_gasto` maior que 500).
8. Crie uma lista de 5 clientes (dicionários) e salve em `clientes_ex.json`. Depois carregue o arquivo e use um `for` para calcular a soma de `total_gasto` de todos os clientes.
9. Carregue o arquivo `clientes_ex.json` do exercício 8 e crie uma nova lista contendo só os nomes dos clientes com `total_gasto` acima da média calculada.
10. Crie um dicionário representando o estoque completo da loja, no formato `{"produtos": [ {...}, {...} ]}` (uma lista de produtos dentro de uma chave). Salve em `estoque_ex.json`, leia de volta, e imprima o valor total em estoque (soma de `preco * quantidade_em_estoque` de cada produto).

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import json

produto = {
    "nome": "Caneta Azul",
    "preco": 2.50,
    "quantidade_em_estoque": 100,
}

print(json.dumps(produto, indent=2))
```

**2.**
```python
import json

produto = {
    "nome": "Caneta Azul",
    "preco": 2.50,
    "quantidade_em_estoque": 100,
}

with open("produto_ex.json", "w", encoding="utf-8") as arquivo:
    json.dump(produto, arquivo, indent=2, ensure_ascii=False)
```

**3.**
```python
import json

with open("produto_ex.json", "r", encoding="utf-8") as arquivo:
    produto_carregado = json.load(arquivo)

print(type(produto_carregado))  # <class 'dict'>
```

**4.**
```python
import json

texto = '{"nome": "Mochila", "preco": 89.90}'
produto = json.loads(texto)
print(produto["preco"])  # 89.9
```

**5.**
```python
import json

produtos = [
    {"nome": "Caneta Azul", "preco": 2.50},
    {"nome": "Caderno", "preco": 15.90},
    {"nome": "Mochila", "preco": 89.90},
]

with open("produtos_ex.json", "w", encoding="utf-8") as arquivo:
    json.dump(produtos, arquivo, indent=2, ensure_ascii=False)
```

**6.**
```python
import json

with open("produtos_ex.json", "r", encoding="utf-8") as arquivo:
    produtos = json.load(arquivo)

for produto in produtos:
    print(produto["nome"])
```

**7.**
```python
import json

cliente = {
    "nome": "Julia",
    "email": "julia@email.com",
    "total_gasto": 620.00,
}

with open("cliente_ex.json", "w", encoding="utf-8") as arquivo:
    json.dump(cliente, arquivo, indent=2, ensure_ascii=False)

with open("cliente_ex.json", "r", encoding="utf-8") as arquivo:
    cliente_carregado = json.load(arquivo)

if cliente_carregado["total_gasto"] > 500:
    print(cliente_carregado["nome"], "é VIP")
else:
    print(cliente_carregado["nome"], "não é VIP")
```

**8.**
```python
import json

clientes = [
    {"nome": "Marcos", "total_gasto": 320.00},
    {"nome": "Julia", "total_gasto": 620.00},
    {"nome": "Beto", "total_gasto": 120.00},
    {"nome": "Carla", "total_gasto": 890.00},
    {"nome": "Diego", "total_gasto": 45.00},
]

with open("clientes_ex.json", "w", encoding="utf-8") as arquivo:
    json.dump(clientes, arquivo, indent=2, ensure_ascii=False)

with open("clientes_ex.json", "r", encoding="utf-8") as arquivo:
    clientes_carregados = json.load(arquivo)

soma = 0
for c in clientes_carregados:
    soma += c["total_gasto"]
print("Soma total gasto:", soma)
```

**9.**
```python
import json

with open("clientes_ex.json", "r", encoding="utf-8") as arquivo:
    clientes = json.load(arquivo)

media = sum(c["total_gasto"] for c in clientes) / len(clientes)

acima_da_media = []
for c in clientes:
    if c["total_gasto"] > media:
        acima_da_media.append(c["nome"])

print(acima_da_media)
```

**10.**
```python
import json

estoque = {
    "produtos": [
        {"nome": "Caneta Azul", "preco": 2.50, "quantidade_em_estoque": 100},
        {"nome": "Caderno", "preco": 15.90, "quantidade_em_estoque": 40},
        {"nome": "Mochila", "preco": 89.90, "quantidade_em_estoque": 15},
    ]
}

with open("estoque_ex.json", "w", encoding="utf-8") as arquivo:
    json.dump(estoque, arquivo, indent=2, ensure_ascii=False)

with open("estoque_ex.json", "r", encoding="utf-8") as arquivo:
    estoque_carregado = json.load(arquivo)

valor_total = sum(
    p["preco"] * p["quantidade_em_estoque"] for p in estoque_carregado["produtos"]
)
print("Valor total em estoque:", valor_total)
```

</details>

## 5. CSV (ler e escrever sem pandas)

1. Crie uma lista de listas com cabeçalho `["nome", "preco"]` e 3 produtos. Salve em `produtos_ex.csv` usando `csv.writer`.
2. Leia o arquivo `produtos_ex.csv` de volta usando `csv.reader` e imprima cada linha (repare que tudo vem como string).
3. Leia o arquivo `produtos_ex.csv` usando `csv.DictReader` e imprima só a coluna `"nome"` de cada linha.
4. Crie uma lista de dicionários de clientes (`"nome"`, `"email"`) e salve em `clientes_ex.csv` usando `csv.DictWriter`, lembrando de chamar `.writeheader()`.
5. Leia `clientes_ex.csv` com `csv.DictReader` e imprima quantas linhas (clientes) o arquivo tem.
6. Crie um CSV `vendas_ex.csv` com colunas `produto`, `quantidade`, `preco_unitario` e pelo menos 5 vendas usando `csv.writer`. Depois leia com `csv.DictReader`, convertendo `quantidade` e `preco_unitario` para número, e imprima o total de cada venda.
7. A partir da leitura do exercício 6, calcule e imprima o faturamento total somando o total de todas as vendas.
8. A partir da leitura do exercício 6, encontre e imprima o nome do produto com a maior quantidade vendida em uma única linha.
9. Crie um CSV `estoque_baixo.csv` com colunas `produto` e `quantidade_em_estoque`, com pelo menos 6 produtos (alguns com quantidade baixa, outros alta). Leia o arquivo e imprima só os produtos com `quantidade_em_estoque` menor que 10.
10. Escreva uma função `csv_para_lista_de_dicionarios(caminho_arquivo)` que recebe o caminho de um CSV e devolve uma lista de dicionários (usando `csv.DictReader` por dentro). Teste a função com o arquivo `vendas_ex.csv` do exercício 6.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import csv

produtos = [
    ["nome", "preco"],
    ["Caneta Azul", 2.50],
    ["Caderno", 15.90],
    ["Mochila", 89.90],
]

with open("produtos_ex.csv", "w", newline="", encoding="utf-8") as arquivo:
    escritor = csv.writer(arquivo)
    escritor.writerows(produtos)
```

**2.**
```python
import csv

with open("produtos_ex.csv", "r", encoding="utf-8") as arquivo:
    leitor = csv.reader(arquivo)
    for linha in leitor:
        print(linha)
```

**3.**
```python
import csv

with open("produtos_ex.csv", "r", encoding="utf-8") as arquivo:
    leitor = csv.DictReader(arquivo)
    for linha in leitor:
        print(linha["nome"])
```

**4.**
```python
import csv

clientes = [
    {"nome": "Marcos", "email": "marcos@email.com"},
    {"nome": "Julia", "email": "julia@email.com"},
]

with open("clientes_ex.csv", "w", newline="", encoding="utf-8") as arquivo:
    campos = ["nome", "email"]
    escritor = csv.DictWriter(arquivo, fieldnames=campos)
    escritor.writeheader()
    for cliente in clientes:
        escritor.writerow(cliente)
```

**5.**
```python
import csv

with open("clientes_ex.csv", "r", encoding="utf-8") as arquivo:
    leitor = csv.DictReader(arquivo)
    linhas = list(leitor)

print("Total de clientes:", len(linhas))
```

**6.**
```python
import csv

vendas = [
    ["produto", "quantidade", "preco_unitario"],
    ["Caneta Azul", 3, 2.50],
    ["Caderno", 1, 15.90],
    ["Mochila", 2, 89.90],
    ["Lapis HB", 5, 1.20],
    ["Borracha", 4, 3.00],
]

with open("vendas_ex.csv", "w", newline="", encoding="utf-8") as arquivo:
    escritor = csv.writer(arquivo)
    escritor.writerows(vendas)

with open("vendas_ex.csv", "r", encoding="utf-8") as arquivo:
    leitor = csv.DictReader(arquivo)
    for linha in leitor:
        total = float(linha["quantidade"]) * float(linha["preco_unitario"])
        print(linha["produto"], "-", total)
```

**7.**
```python
import csv

faturamento_total = 0

with open("vendas_ex.csv", "r", encoding="utf-8") as arquivo:
    leitor = csv.DictReader(arquivo)
    for linha in leitor:
        total = float(linha["quantidade"]) * float(linha["preco_unitario"])
        faturamento_total += total

print("Faturamento total:", faturamento_total)
```

**8.**
```python
import csv

maior_quantidade = -1
produto_mais_vendido = None

with open("vendas_ex.csv", "r", encoding="utf-8") as arquivo:
    leitor = csv.DictReader(arquivo)
    for linha in leitor:
        quantidade = float(linha["quantidade"])
        if quantidade > maior_quantidade:
            maior_quantidade = quantidade
            produto_mais_vendido = linha["produto"]

print(produto_mais_vendido)
```

**9.**
```python
import csv

estoque = [
    ["produto", "quantidade_em_estoque"],
    ["Caneta Azul", 100],
    ["Caderno", 8],
    ["Mochila", 15],
    ["Lapis HB", 5],
    ["Borracha", 60],
    ["Marca-texto", 3],
]

with open("estoque_baixo.csv", "w", newline="", encoding="utf-8") as arquivo:
    escritor = csv.writer(arquivo)
    escritor.writerows(estoque)

with open("estoque_baixo.csv", "r", encoding="utf-8") as arquivo:
    leitor = csv.DictReader(arquivo)
    for linha in leitor:
        if float(linha["quantidade_em_estoque"]) < 10:
            print(linha["produto"])
```

**10.**
```python
import csv

def csv_para_lista_de_dicionarios(caminho_arquivo):
    with open(caminho_arquivo, "r", encoding="utf-8") as arquivo:
        leitor = csv.DictReader(arquivo)
        return list(leitor)

vendas = csv_para_lista_de_dicionarios("vendas_ex.csv")
print(vendas)
```

</details>

## 6. pip (instalando pacotes)

1. Escreva o comando que verifica a versão do `pip` instalada no seu computador.
2. Escreva o comando para instalar a biblioteca `numpy` na versão mais recente disponível.
3. Escreva o comando para instalar a versão exata `1.24.0` da biblioteca `numpy`.
4. Escreva o comando para instalar qualquer versão de `numpy` igual ou mais nova que `1.20.0`.
5. Escreva o comando que lista todas as bibliotecas instaladas no ambiente atual.
6. Escreva o comando que mostra detalhes (versão, dependências) da biblioteca `pandas` já instalada.
7. Escreva o comando para desinstalar a biblioteca `matplotlib`.
8. Escreva o comando que gera um arquivo `requirements.txt` com todas as bibliotecas do ambiente atual.
9. Escreva o conteúdo de um `requirements.txt` para um projeto que usa `pandas==2.0.3`, `numpy==1.25.0` e `seaborn==0.12.2`, e o comando que instalaria tudo a partir desse arquivo.
10. Sua colega mandou um projeto que usa `requests` e `beautifulsoup4`, mas não especificou versões. Escreva o comando para instalar as duas de uma vez (sem versão fixa) e, em seguida, o comando para gerar o `requirements.txt` depois de instaladas.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```bash
pip --version
```

**2.**
```bash
pip install numpy
```

**3.**
```bash
pip install numpy==1.24.0
```

**4.**
```bash
pip install numpy>=1.20.0
```

**5.**
```bash
pip list
```

**6.**
```bash
pip show pandas
```

**7.**
```bash
pip uninstall matplotlib
```

**8.**
```bash
pip freeze > requirements.txt
```

**9.**
```text
pandas==2.0.3
numpy==1.25.0
seaborn==0.12.2
```
```bash
pip install -r requirements.txt
```

**10.**
```bash
pip install requests beautifulsoup4
pip freeze > requirements.txt
```

</details>

## 7. Ambientes virtuais (venv)

1. Dentro de uma pasta de teste nova, crie um ambiente virtual chamado `venv` usando o comando correto.
2. Ative o ambiente virtual criado no exercício 1 (use o comando do seu sistema operacional).
3. Com o ambiente ativado, confirme visualmente (olhando o terminal) que ele está ativo, e descreva o que muda na aparência da linha de comando.
4. Instale a biblioteca `requests` dentro do ambiente ativado.
5. Rode `pip list` dentro do ambiente ativado e confirme que `requests` aparece na lista.
6. Desative o ambiente virtual com o comando `deactivate`.
7. Crie um segundo ambiente virtual chamado `venv_teste2` em outra pasta, ative-o, e confirme (com `pip list`) que ele **não** tem `requests` instalado (prova de que os ambientes são isolados).
8. Com um ambiente ativado, gere um `requirements.txt` a partir dele usando `pip freeze > requirements.txt`.
9. Descreva o passo a passo completo (em comandos) para começar um projeto novo do zero: criar a pasta, criar o ambiente, ativar, instalar `pandas`, e gerar o `requirements.txt`.
10. Simule que você recebeu um projeto de outra pessoa, com um `requirements.txt` já pronto, mas sem o ambiente virtual (a pasta `venv` não veio, como é o correto). Escreva os comandos, em ordem, para recriar o ambiente e instalar todas as dependências listadas no arquivo.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```bash
python -m venv venv
```

**2.**
```bash
# Windows (PowerShell)
venv\Scripts\Activate.ps1

# Mac/Linux
source venv/bin/activate
```

**3.**
Passo a passo: depois de ativar, o nome do ambiente aparece entre parênteses no início da linha do terminal, por exemplo `(venv) C:\pasta-de-teste>`. Isso confirma visualmente que os próximos comandos `pip install` vão rodar isolados dentro dessa "gaveta", e não no Python global do computador.

**4.**
```bash
pip install requests
```

**5.**
```bash
pip list
# "requests" deve aparecer na lista, junto com a versão instalada
```

**6.**
```bash
deactivate
```

**7.**
```bash
python -m venv venv_teste2
venv_teste2\Scripts\Activate.ps1
pip list
# "requests" NÃO deve aparecer aqui, pois esse é um ambiente novo e
# separado do ambiente "venv" do exercício 4
```

**8.**
```bash
pip freeze > requirements.txt
```

**9.**
```bash
mkdir loja-da-ana-analise
cd loja-da-ana-analise
python -m venv venv
venv\Scripts\Activate.ps1
pip install pandas
pip freeze > requirements.txt
```

**10.**
```bash
# 1. Entrar na pasta do projeto recebido
cd projeto-recebido

# 2. Criar o ambiente virtual do zero
python -m venv venv

# 3. Ativar o ambiente
venv\Scripts\Activate.ps1

# 4. Instalar todas as dependências listadas no requirements.txt do projeto
pip install -r requirements.txt
```

</details>

## 8. Conda (alternativa ao venv)

1. Escreva o comando para criar um ambiente conda chamado `loja-ana-conda` usando Python 3.11.
2. Escreva o comando para ativar o ambiente `loja-ana-conda`.
3. Com o ambiente ativado, escreva o comando para instalar `pandas` e `numpy` de uma vez usando `conda install`.
4. Escreva o comando para listar todos os ambientes conda já criados no computador.
5. Escreva o comando para listar os pacotes instalados dentro do ambiente ativo no momento.
6. Escreva o comando para desativar o ambiente atual e voltar ao ambiente `base`.
7. Escreva o comando para remover completamente o ambiente `loja-ana-conda` do computador.
8. Explique, com suas próprias palavras (em um comentário), a principal diferença entre o que `conda` gerencia e o que `venv` gerencia.
9. Você está começando um projeto que usa `scipy`, uma biblioteca científica com dependências fora do Python puro. Justifique, em uma frase, se `conda` ou `venv` seria a escolha mais segura, e escreva o comando de criação do ambiente para essa escolha.
10. Escreva a sequência completa de comandos para: criar um ambiente `dados-ml` com Python 3.10, ativá-lo, instalar `pandas`, `scikit-learn` e `matplotlib`, e por fim listar os pacotes instalados para conferir.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```bash
conda create --name loja-ana-conda python=3.11
```

**2.**
```bash
conda activate loja-ana-conda
```

**3.**
```bash
conda install pandas numpy
```

**4.**
```bash
conda env list
```

**5.**
```bash
conda list
```

**6.**
```bash
conda deactivate
```

**7.**
```bash
conda env remove --name loja-ana-conda
```

**8.**
```text
# venv isola só bibliotecas Python dentro do Python que já está instalado
# no computador. conda isola pacotes de qualquer tipo, incluindo diferentes
# versões do próprio Python e bibliotecas com dependências que não são
# Python puro (como componentes escritos em C ou Fortran), comuns em
# bibliotecas científicas.
```

**9.**
```text
# scipy é uma biblioteca científica com dependências fora do Python puro,
# então conda é a escolha mais segura, pois sabe instalar essas peças
# extras sozinho.
```
```bash
conda create --name projeto-scipy python=3.11
```

**10.**
```bash
conda create --name dados-ml python=3.10
conda activate dados-ml
conda install pandas scikit-learn matplotlib
conda list
```

</details>

## 9. VS Code (configuração básica para Python)

1. Abra o VS Code e instale a extensão "Python" (da Microsoft) pela aba de Extensões.
2. Enquanto estiver na aba de Extensões, instale também a extensão "Jupyter".
3. Abra (com "Open Folder") a pasta de um projeto onde você já tenha um ambiente virtual criado (do tópico de venv). Descreva o que aparece no canto inferior direito do VS Code.
4. Clique no nome do interpretador no canto inferior direito e selecione o interpretador correspondente ao ambiente virtual do projeto (algo como `venv\Scripts\python.exe`).
5. Crie um arquivo `teste.py` dentro da pasta do projeto com um `print("Olá, VS Code")` e rode com Ctrl+F5 (ou o botão de play).
6. Abra o terminal integrado (Ctrl+`) e confirme que ele já abre dentro da pasta do projeto.
7. No terminal integrado, rode `pip install requests` e depois `pip list`, conferindo que `requests` aparece na lista.
8. Feche o VS Code, abra de novo, e confirme que o interpretador selecionado anteriormente continua sendo o mesmo (ou selecione-o de novo, se necessário).
9. Escreva propositalmente um erro de sintaxe simples em um arquivo `.py` (por exemplo, esquecer os dois-pontos de um `if`) e observe o sublinhado vermelho que a extensão Python desenha antes mesmo de rodar o código.
10. Abra um arquivo `.py` "solto" (sem usar "Open Folder" para abrir a pasta inteira do projeto) e compare com abrir a pasta inteira — anote a diferença que você percebe no comportamento do interpretador selecionado.

<details>
<summary>Clique para ver as soluções</summary>

Não há código para essa tarefa — são exercícios de configuração e uso da ferramenta. Passo a passo esperado para cada um:

**1.** Ctrl+Shift+X para abrir a aba de Extensões, buscar "Python", clicar em "Install".

**2.** Na mesma aba, buscar "Jupyter" e clicar em "Install".

**3.** Menu > File > Open Folder, selecionar a pasta do projeto. No canto inferior direito deve aparecer o nome de um interpretador Python, como "Python 3.11.4".

**4.** Clicar no nome do interpretador no canto inferior direito, escolher na lista o caminho que aponta para dentro da pasta `venv` do projeto (ex: `venv\Scripts\python.exe`).

**5.** Criar `teste.py` com `print("Olá, VS Code")`, salvar, e rodar com Ctrl+F5 — o resultado deve aparecer no terminal integrado.

**6.** Ctrl+` abre o terminal integrado; o caminho mostrado no terminal deve ser o da pasta do projeto aberta.

**7.** Rodar `pip install requests` seguido de `pip list` no terminal integrado — `requests` deve aparecer na lista, confirmando que a instalação foi para o ambiente correto.

**8.** Reabrir o VS Code na mesma pasta do projeto — o interpretador selecionado geralmente é lembrado automaticamente; se não for, repetir o passo do exercício 4.

**9.** Escrever `if True` sem os dois-pontos gera um sublinhado vermelho embaixo do trecho com erro, mesmo sem rodar o código — passar o mouse por cima mostra a mensagem de erro de sintaxe.

**10.** Ao abrir um arquivo solto (sem "Open Folder"), o VS Code costuma não reconhecer automaticamente o ambiente virtual do projeto, podendo mostrar o interpretador Python global em vez do `venv` — abrir a pasta inteira é o jeito recomendado para evitar essa confusão.

</details>

## 10. JupyterLab

1. Com um ambiente virtual ativado, instale o JupyterLab com `pip install jupyterlab` e abra-o com `jupyter lab`.
2. Crie um notebook novo (`.ipynb`) e, na primeira célula (markdown), escreva um título `## Testes do módulo 2`.
3. Em uma célula de código, crie uma lista `precos = [10.0, 25.5, 8.90, 42.0]` e rode a célula com Shift+Enter.
4. Em outra célula, calcule e imprima a soma da lista `precos` (repare que essa célula depende da célula anterior já ter rodado).
5. Crie uma célula de markdown explicando, em texto, o que a célula de código anterior calculou.
6. Rode as células fora de ordem propositalmente: mude o valor de `precos` na primeira célula de código, mas rode só a célula da soma (sem rodar a célula que muda `precos` de novo). Observe e anote se a soma mudou ou não.
7. Adicione uma célula nova que calcula a média da lista `precos` (soma dividido pelo tamanho da lista), e rode-a.
8. Verifique, ao lado de cada célula de código, o número entre colchetes (ex: `[1]`, `[2]`) e explique o que ele representa.
9. Salve o notebook, feche o JupyterLab, abra de novo e confirme que os resultados das células continuam visíveis (mesmo sem rodar de novo).
10. Crie um notebook novo do zero que simula vendas da Loja da Ana: uma célula de markdown com título, uma célula que usa `random` (visto em `02-modulo-random.md`) para gerar 5 vendas com seed fixa, e uma célula final que calcula o faturamento total.

<details>
<summary>Clique para ver as soluções</summary>

Não há código de "lógica" para resolver — são exercícios de uso da ferramenta. Passo a passo esperado:

**1.**
```bash
pip install jupyterlab
jupyter lab
```

**2.** No JupyterLab, clicar em "Notebook" sob Python 3, mudar o tipo da primeira célula para "Markdown" na barra de ferramentas, e escrever `## Testes do módulo 2`.

**3.**
```python
precos = [10.0, 25.5, 8.90, 42.0]
```
Rodar com Shift+Enter.

**4.**
```python
print(sum(precos))
```

**5.** Célula de markdown com um texto como: "A célula acima soma todos os valores da lista `precos` usando a função embutida `sum`."

**6.** Se você mudar `precos` na primeira célula mas não rodar essa célula de novo, a soma calculada na célula seguinte continua usando o valor **antigo** de `precos`, pois o notebook guarda o estado da última execução de cada célula, não o texto atual escrito nela.

**7.**
```python
media = sum(precos) / len(precos)
print(media)
```

**8.** O número entre colchetes (ex: `[3]`) indica a ordem real em que aquela célula foi executada — não necessariamente a ordem visual de cima para baixo do notebook.

**9.** Salvar com Ctrl+S (ou o ícone de salvar), fechar a aba, reabrir o mesmo arquivo `.ipynb` pelo JupyterLab — os resultados da última execução de cada célula continuam aparecendo, mesmo sem rodar de novo.

**10.**
```text
Célula 1 (markdown):
## Simulação de vendas — Loja da Ana
```
```python
# Célula 2 (código)
import random

random.seed(4)
produtos = ["Caneta", "Caderno", "Mochila", "Lapis"]

vendas = []
for _ in range(5):
    venda = {
        "produto": random.choice(produtos),
        "quantidade": random.randint(1, 6),
        "preco_unitario": round(random.uniform(2.0, 50.0), 2),
    }
    vendas.append(venda)

for venda in vendas:
    print(venda)
```
```python
# Célula 3 (código)
faturamento = sum(v["quantidade"] * v["preco_unitario"] for v in vendas)
print("Faturamento total:", faturamento)
```

</details>

## 11. Google Colab

1. Acesse colab.research.google.com e crie um novo notebook em branco.
2. Na primeira célula, mude o tipo para texto (markdown) e escreva um título `## Testes do Google Colab`.
3. Em uma célula de código, importe `random`, defina `random.seed(2)`, e imprima um número sorteado com `random.randint(1, 50)`.
4. Rode a célula com Shift+Enter e confirme que o notebook salva automaticamente no Google Drive (observe o indicador de "salvando..." no topo).
5. Adicione uma nova célula de código que importa `pandas` (sem precisar instalar nada antes) e imprima `pandas.__version__` para confirmar que a biblioteca já vem pré-instalada.
6. Em uma célula de código, use `!pip install` (com o ponto de exclamação) para instalar uma biblioteca que não vem pré-instalada, por exemplo `unidecode`.
7. Simule 6 vendas da Loja da Ana usando `random` com seed fixa, em uma célula, e calcule a quantidade total vendida em outra célula.
8. Feche a aba do notebook, espere alguns minutos, reabra pelo Google Drive (menu "Colab Notebooks") e rode as células de novo na ordem, confirmando que o resultado bate (graças à seed fixa).
9. Explique, em um comentário de texto, o que acontece com as variáveis calculadas quando uma sessão do Colab expira por inatividade, e o que continua salvo mesmo assim.
10. Crie um notebook completo simulando um pequeno relatório da Loja da Ana: título em markdown, uma célula gerando vendas simuladas com `random` (seed fixa), uma célula calculando o faturamento total, e uma célula de markdown final resumindo o resultado encontrado.

<details>
<summary>Clique para ver as soluções</summary>

Não há código de "lógica" para resolver — são exercícios de uso da ferramenta. Passo a passo esperado:

**1.** Acessar colab.research.google.com, fazer login com uma conta Google, clicar em "New Notebook".

**2.** Clicar em "+ Texto" na barra superior, escrever `## Testes do Google Colab` na célula criada.

**3.**
```python
import random

random.seed(2)
print(random.randint(1, 50))
```

**4.** Rodar com Shift+Enter; no topo da página aparece um indicador temporário (algo como "Salvando..." ou o ícone de nuvem) confirmando que o notebook foi salvo automaticamente na pasta "Colab Notebooks" do Google Drive.

**5.**
```python
import pandas
print(pandas.__version__)
```
Deve rodar sem erro de instalação, pois o Colab já vem com pandas pré-instalado.

**6.**
```python
!pip install unidecode
```
O `!` no início indica que a linha é um comando de terminal, não Python.

**7.**
```python
import random

random.seed(6)
produtos = ["Caneta", "Caderno", "Mochila", "Lapis"]

vendas = []
for _ in range(6):
    venda = {
        "produto": random.choice(produtos),
        "quantidade": random.randint(1, 5),
    }
    vendas.append(venda)

for venda in vendas:
    print(venda)
```
```python
quantidade_total = sum(v["quantidade"] for v in vendas)
print("Quantidade total vendida:", quantidade_total)
```

**8.** Fechar a aba, esperar alguns minutos, acessar drive.google.com > pasta "Colab Notebooks", abrir o notebook de novo, rodar as células na ordem — como a seed é fixa, o resultado impresso é idêntico ao de antes.

**9.**
```text
Quando a sessão expira por inatividade, o Colab desconecta o servidor que
estava rodando o Python -- todas as variáveis calculadas na memória se
perdem. O texto e o código escritos em cada célula, porém, continuam salvos
no Google Drive; basta rodar as células de novo, na ordem certa, para
recalcular tudo.
```

**10.**
```text
Célula 1 (markdown):
## Relatório de vendas — Loja da Ana
```
```python
# Célula 2 (código)
import random

random.seed(8)
produtos = ["Caneta", "Caderno", "Mochila", "Lapis", "Borracha"]

vendas = []
for _ in range(10):
    venda = {
        "produto": random.choice(produtos),
        "quantidade": random.randint(1, 6),
        "preco_unitario": round(random.uniform(2.0, 60.0), 2),
    }
    vendas.append(venda)
```
```python
# Célula 3 (código)
faturamento_total = sum(v["quantidade"] * v["preco_unitario"] for v in vendas)
print("Faturamento total:", faturamento_total)
```
```text
Célula 4 (markdown):
## Conclusão

O faturamento total simulado para o período foi calculado somando o
resultado de cada venda gerada aleatoriamente, com seed fixa para garantir
que o relatório seja reproduzível.
```

</details>
