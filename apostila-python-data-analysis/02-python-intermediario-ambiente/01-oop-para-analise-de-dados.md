# OOP para análise de dados

> Módulo 2 — Python Intermediário e Ambiente · Tópico 1 de 11

## O que é e por que importa

Até agora, os dados da Loja da Ana viviam em variáveis soltas ou em dicionários: um dicionário para cada produto, uma lista de dicionários para as vendas. Isso funciona, mas em algum momento fica repetitivo — toda venda tem "produto", "quantidade" e "preço", e toda vez que você quer calcular o total daquela venda, reescreve a mesma fórmula.

OOP (Programação Orientada a Objetos, do inglês "Object-Oriented Programming") é uma forma de organizar código em torno de "coisas" do mundo real. Em vez de espalhar dados e funções separadamente, você cria um **objeto** que já sabe quais informações carrega e o que sabe fazer com elas. Pensa numa ficha de cadastro: uma ficha de produto tem campos fixos (nome, preço, categoria) e ações associadas (calcular imposto, aplicar desconto). Uma **classe** é o molde dessa ficha; um **objeto** é uma ficha preenchida a partir desse molde.

Isso importa em análise de dados porque, conforme seus scripts crescem, você começa a lidar com "coisas" que se repetem — produtos, vendas, clientes — cada uma com os mesmos campos e os mesmos cálculos. Uma classe evita que você repita a lógica de cálculo em vários lugares e deixa o código mais parecido com a forma como você pensa no problema ("pegue essa venda e calcule o total dela", em vez de "pegue esse dicionário, ache a chave 'preco', multiplique pela chave 'quantidade'").

Não se preocupe em virar um "programador orientado a objetos" agora — aqui vamos só o suficiente para reconhecer classes quando aparecerem (inclusive dentro de bibliotecas como pandas, que usa objetos por baixo dos panos) e para criar as suas próprias quando ajudar a organizar os dados da Loja da Ana.

## Como funciona (com exemplo comentado)

```python
# "class" define o molde. Por convenção, nomes de classes começam com letra maiúscula
class Produto:
    # __init__ é um método especial, chamado automaticamente quando você cria um objeto.
    # "self" representa o próprio objeto sendo criado -- é assim que o objeto
    # guarda seus próprios dados
    def __init__(self, nome, preco, quantidade_em_estoque):
        self.nome = nome
        self.preco = preco
        self.quantidade_em_estoque = quantidade_em_estoque

    # Um "método" é uma função que pertence à classe -- ela sempre recebe "self"
    # como primeiro parâmetro, para poder acessar os dados do objeto
    def valor_total_em_estoque(self):
        return self.preco * self.quantidade_em_estoque

    def aplicar_reajuste(self, percentual):
        self.preco = self.preco * (1 + percentual)


# Criando objetos a partir do molde "Produto" -- cada um é uma "ficha" independente
caneta = Produto("Caneta Azul", 2.50, 100)
caderno = Produto("Caderno Capa Dura", 15.90, 40)

# Acessando os atributos (os dados guardados no objeto)
print(caneta.nome, caneta.preco)          # Caneta Azul 2.5
print(caderno.quantidade_em_estoque)      # 40

# Chamando os métodos (as ações que o objeto sabe fazer)
print("Valor em estoque da caneta:", caneta.valor_total_em_estoque())    # 250.0
print("Valor em estoque do caderno:", caderno.valor_total_em_estoque())  # 636.0

caneta.aplicar_reajuste(0.10)  # reajuste de 10%
print("Novo preço da caneta:", caneta.preco)  # 2.75

# Uma classe para representar uma venda, reaproveitando um objeto Produto
class Venda:
    def __init__(self, produto, quantidade):
        self.produto = produto
        self.quantidade = quantidade

    def total(self):
        return self.produto.preco * self.quantidade

venda_1 = Venda(caneta, 3)
print("Total da venda:", venda_1.total())  # 8.25
```

Repare que `caneta` e `caderno` foram criados a partir do **mesmo** molde (`Produto`), mas cada um guarda seus próprios valores — mudar o preço da caneta não afeta o caderno. Isso é o que chamamos de "instância": cada objeto é uma instância independente da classe.

## Erros comuns de quem está começando

- Esquecer o `self` como primeiro parâmetro de um método (inclusive do `__init__`). Sem ele, o Python não sabe a quem pertencem os dados, e você recebe um erro de argumentos.
- Confundir a classe (o molde, ex: `Produto`) com o objeto (a ficha preenchida, ex: `caneta`). Você define a classe uma vez, mas pode criar quantos objetos quiser a partir dela.
- Tentar acessar um atributo antes de criar o objeto, ou esquecer o `self.` na frente do nome do atributo dentro dos métodos (escrever `preco` em vez de `self.preco`) — isso faz o Python procurar uma variável solta que não existe.

## Exercício prático

Crie uma classe `Cliente` com:

1. `__init__` recebendo `nome` e `total_gasto` (valor já gasto na loja até agora).
2. Um método `e_cliente_vip()` que devolve `True` se `total_gasto` for maior que R$ 500, e `False` caso contrário.
3. Um método `registrar_compra(valor)` que soma `valor` ao `total_gasto` do cliente.

Crie um objeto `Cliente("Marcos", 320.00)`, registre uma nova compra de R$ 250.00, e depois imprima se ele é VIP.

**Desafio bônus (opcional):** crie uma lista com três objetos `Cliente` diferentes e use um `for` (visto em `12-loops.md` do Módulo 1) para imprimir o nome de todos que são VIP.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
class Cliente:
    def __init__(self, nome, total_gasto):
        self.nome = nome
        self.total_gasto = total_gasto

    def e_cliente_vip(self):
        return self.total_gasto > 500

    def registrar_compra(self, valor):
        self.total_gasto = self.total_gasto + valor

marcos = Cliente("Marcos", 320.00)
marcos.registrar_compra(250.00)
print(marcos.e_cliente_vip())  # True, pois 570 > 500

# Desafio bônus
clientes = [
    Cliente("Marcos", 570.00),
    Cliente("Julia", 120.00),
    Cliente("Beto", 800.00),
]

for cliente in clientes:
    if cliente.e_cliente_vip():
        print(cliente.nome)
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar com minhas próprias palavras a diferença entre classe e objeto
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Entendo para que serve o `self` dentro de uma classe
