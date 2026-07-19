# CSV (ler e escrever sem pandas)

> Módulo 2 — Python Intermediário e Ambiente · Tópico 5 de 11

## O que é e por que importa

CSV (*Comma-Separated Values*, "valores separados por vírgula") é o formato de arquivo mais comum para guardar dados em forma de tabela — é basicamente o que você vê quando exporta uma planilha do Excel ou Google Sheets como "CSV". Cada linha do arquivo é uma linha da tabela, e cada valor dentro da linha é separado por vírgula (ou outro caractere, como ponto e vírgula).

Pensa num CSV como uma planilha "crua", sem formatação, cores ou fórmulas — só os dados em texto puro, um valor depois do outro. Por ser simples, é o formato mais universal para trocar dados de tabela entre sistemas diferentes: praticamente qualquer ferramenta de dados (Excel, Google Sheets, bancos de dados, pandas) consegue abrir um CSV.

Você vai usar pandas para trabalhar com CSVs de forma mais poderosa a partir do Módulo 4, mas entender como o módulo `csv` embutido do Python funciona por baixo é importante: ajuda a entender o que está acontecendo quando o pandas "mastiga" o arquivo para você, e serve para casos simples onde instalar uma biblioteca extra seria exagero. Vamos guardar as vendas da Loja da Ana em CSV, exatamente como aconteceria numa exportação real de um sistema de vendas.

## Como funciona (com exemplo comentado)

```python
import csv  # módulo embutido, não precisa instalar

vendas = [
    ["produto", "quantidade", "preco_unitario"],   # cabeçalho (nomes das colunas)
    ["Caneta Azul", 3, 2.50],
    ["Caderno", 1, 15.90],
    ["Mochila", 2, 89.90],
]

# csv.writer escreve linha por linha em um arquivo, a partir de listas
with open("vendas.csv", "w", newline="", encoding="utf-8") as arquivo:
    # newline="" evita linhas em branco extras no Windows -- é praticamente
    # obrigatório usar esse parâmetro ao escrever CSV
    escritor = csv.writer(arquivo)
    for linha in vendas:
        escritor.writerow(linha)
    # ou, em uma linha só, para todas as linhas de uma vez:
    # escritor.writerows(vendas)

# csv.reader lê o arquivo de volta, linha por linha, cada linha vira uma lista de strings
with open("vendas.csv", "r", encoding="utf-8") as arquivo:
    leitor = csv.reader(arquivo)
    for linha in leitor:
        print(linha)
    # Saída:
    # ['produto', 'quantidade', 'preco_unitario']
    # ['Caneta Azul', '3', '2.5']
    # ['Caderno', '1', '15.9']
    # ['Mochila', '2', '89.9']
    # Repare que TUDO vira string -- csv.reader não sabe que "3" era um número

# DictReader lê o CSV e já transforma cada linha em um dicionário,
# usando o cabeçalho como chaves -- muito mais prático que csv.reader puro
with open("vendas.csv", "r", encoding="utf-8") as arquivo:
    leitor_dict = csv.DictReader(arquivo)
    for linha in leitor_dict:
        print(linha["produto"], "-", linha["quantidade"])
        # ainda são strings! para calcular, é preciso converter:
        total = float(linha["quantidade"]) * float(linha["preco_unitario"])
        print("Total:", total)

# DictWriter escreve dicionários direto, sem precisar montar listas na mão
clientes = [
    {"nome": "Marcos", "email": "marcos@email.com"},
    {"nome": "Julia", "email": "julia@email.com"},
]

with open("clientes.csv", "w", newline="", encoding="utf-8") as arquivo:
    campos = ["nome", "email"]  # precisa informar os nomes das colunas
    escritor_dict = csv.DictWriter(arquivo, fieldnames=campos)
    escritor_dict.writeheader()  # escreve a linha de cabeçalho
    for cliente in clientes:
        escritor_dict.writerow(cliente)
```

## Erros comuns de quem está começando

- Esquecer que **tudo que vem de um CSV é string**, mesmo números. Somar `"3"` com `"5"` sem converter para `int`/`float` primeiro (como visto em `07-conversao-de-tipos.md` do Módulo 1) gera erro ou concatenação de texto em vez de soma.
- Esquecer o `newline=""` ao abrir o arquivo para escrita no Windows, o que pode gerar linhas em branco extras entre cada linha do CSV.
- No `DictWriter`, esquecer de chamar `.writeheader()` antes de escrever as linhas — sem isso, o arquivo não terá a linha de cabeçalho com os nomes das colunas.

## Exercício prático

Crie uma lista de listas representando vendas da Loja da Ana, com cabeçalho `["produto", "quantidade", "preco_unitario"]` e pelo menos 4 vendas. Salve em um arquivo `vendas_loja.csv` usando `csv.writer`. Depois, leia o arquivo de volta com `csv.DictReader` e calcule o total de cada venda (`quantidade * preco_unitario`, lembrando de converter os valores para número), imprimindo o produto e o total.

**Desafio bônus (opcional):** some o total de todas as vendas lidas do CSV e imprima o faturamento total.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import csv

vendas = [
    ["produto", "quantidade", "preco_unitario"],
    ["Caneta Azul", 3, 2.50],
    ["Caderno", 1, 15.90],
    ["Mochila", 2, 89.90],
    ["Lapis HB", 5, 1.20],
]

with open("vendas_loja.csv", "w", newline="", encoding="utf-8") as arquivo:
    escritor = csv.writer(arquivo)
    escritor.writerows(vendas)

faturamento_total = 0

with open("vendas_loja.csv", "r", encoding="utf-8") as arquivo:
    leitor = csv.DictReader(arquivo)
    for linha in leitor:
        quantidade = float(linha["quantidade"])
        preco_unitario = float(linha["preco_unitario"])
        total = quantidade * preco_unitario
        faturamento_total += total
        print(linha["produto"], "-", total)

# Desafio bônus
print("Faturamento total:", faturamento_total)
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar por que os valores lidos de um CSV vêm sempre como string
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Entendo a diferença entre `csv.reader`/`writer` e `csv.DictReader`/`DictWriter`
