# Expressões regulares (re) — nível básico

> Módulo 2 — Python Intermediário e Ambiente · Tópico 3 de 11

## O que é e por que importa

Expressão regular (ou "regex", abreviação de *regular expression*) é uma forma de descrever um **padrão de texto** para o computador procurar. Em vez de procurar uma palavra exata, você descreve uma "forma": "um número de telefone tem esse formato", "um e-mail sempre tem um `@` no meio", "um código de produto começa com três letras seguidas de quatro números".

Pensa em regex como uma busca do tipo "encontre arquivos" no seu computador, mas para pedaços de texto dentro de uma string: em vez de `*.pdf` para achar arquivos PDF, você escreve um padrão tipo `\d+` para achar "um ou mais números seguidos" dentro de um texto qualquer.

Em análise de dados, regex aparece o tempo todo na etapa de **limpeza de dados**: validar se um campo de telefone está no formato certo, extrair só a parte numérica de um preço escrito como `"R$ 45,90"`, checar se um e-mail de cliente parece válido antes de usá-lo, ou separar um código de pedido do resto de uma descrição. O módulo embutido do Python para isso se chama `re`.

Regex tem fama de assustadora por causa dos símbolos, mas neste tópico vamos ver só o essencial — o suficiente para resolver 80% dos casos do dia a dia em análise de dados.

## Como funciona (com exemplo comentado)

```python
import re  # módulo embutido de expressões regulares

# re.search procura o padrão em QUALQUER parte do texto e devolve
# um "objeto de match" se encontrar, ou None se não encontrar
descricao = "Pedido #4521 - Caneta Azul - R$ 2,50"

resultado = re.search(r"\d+", descricao)
# \d significa "um dígito" (0-9). O + significa "um ou mais seguidos".
# O "r" antes da string (string "raw") evita que o Python interprete a barra
# invertida de forma estranha -- é praticamente obrigatório usar r"" em regex

if resultado:
    print("Encontrado:", resultado.group())  # .group() pega o texto que deu match
else:
    print("Nenhum número encontrado")

# re.findall devolve TODOS os trechos que combinam com o padrão, em uma lista
numeros = re.findall(r"\d+", descricao)
print(numeros)  # ['4521', '2', '50']

# re.match só verifica o INÍCIO do texto (diferente de re.search, que procura em qualquer lugar)
codigo_produto = "CAN001"
if re.match(r"[A-Z]{3}", codigo_produto):
    # [A-Z] significa "uma letra maiúscula de A a Z". {3} significa "exatamente 3 vezes seguidas"
    print("Código começa com 3 letras maiúsculas -- formato válido")
else:
    print("Formato de código inválido")

# Validando um formato de e-mail de cliente (padrão simples, não cobre todos os casos)
email_cliente = "ana.compras@lojadaana.com"
padrao_email = r"^[\w.]+@[\w.]+\.\w+$"
# ^ marca o início do texto, $ marca o fim (garante que o texto INTEIRO precisa bater)
# \w significa "letra, número ou underline". O + de novo é "um ou mais"
if re.match(padrao_email, email_cliente):
    print("E-mail parece válido")
else:
    print("E-mail parece inválido")

# Extraindo só o valor numérico de um preço escrito como texto
preco_texto = "R$ 45,90"
valor = re.findall(r"\d+,\d+", preco_texto)[0]  # pega o primeiro (e único) match
valor_convertido = float(valor.replace(",", "."))  # troca vírgula por ponto para converter em float
print(valor_convertido)  # 45.9
```

## Erros comuns de quem está começando

- Esquecer o `r` antes da string do padrão (ex: usar `"\d+"` em vez de `r"\d+"`). Na maioria dos casos simples funciona igual, mas em padrões mais complexos a barra invertida pode ser interpretada errado — o hábito de sempre usar `r""` evita dor de cabeça.
- Confundir `re.match` (só olha o começo do texto) com `re.search` (procura em qualquer parte). Usar `match` esperando que ele ache um padrão no meio do texto é um erro comum.
- Esquecer de checar se o resultado de `re.search` ou `re.match` é `None` antes de chamar `.group()` nele. Se o padrão não for encontrado, o resultado é `None`, e chamar `.group()` em `None` gera erro.

## Exercício prático

Você recebeu uma lista de descrições de pedidos da Loja da Ana, cada uma no formato `"Pedido #NUMERO - NOME_DO_PRODUTO"`, por exemplo `"Pedido #101 - Caderno"`. Usando `re.findall(r"\d+", ...)` (visto acima), extraia apenas o número do pedido de cada descrição da lista abaixo e imprima todos:

```python
pedidos = [
    "Pedido #101 - Caderno",
    "Pedido #204 - Caneta Azul",
    "Pedido #305 - Mochila",
]
```

**Desafio bônus (opcional):** usando `re.match`, valide se cada número de pedido extraído tem exatamente 3 dígitos (padrão `r"^\d{3}$"`), e imprima uma mensagem dizendo se o formato está correto para cada um.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import re

pedidos = [
    "Pedido #101 - Caderno",
    "Pedido #204 - Caneta Azul",
    "Pedido #305 - Mochila",
]

numeros_pedidos = []
for pedido in pedidos:
    numero = re.findall(r"\d+", pedido)[0]
    numeros_pedidos.append(numero)
    print(numero)

# Desafio bônus
for numero in numeros_pedidos:
    if re.match(r"^\d{3}$", numero):
        print(f"{numero}: formato válido (3 dígitos)")
    else:
        print(f"{numero}: formato inválido")
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar com minhas próprias palavras a diferença entre `re.search`, `re.match` e `re.findall`
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Entendo o que fazem os símbolos `\d`, `+` e `^`/`$` usados neste tópico
