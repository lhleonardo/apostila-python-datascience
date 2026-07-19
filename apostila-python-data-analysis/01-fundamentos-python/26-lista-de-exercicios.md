# Lista de exercícios — Módulo 1

> Módulo 1 — Fundamentos de Python · Lista de exercícios de revisão

Esta lista reúne 10 exercícios práticos para cada tópico do módulo, para
consolidar o que foi aprendido antes de avançar. Tente resolver cada
exercício sem consultar o tópico original primeiro — as soluções vêm logo
depois de cada bloco, dentro de um "clique para ver".

## 1. Introdução

1. Escreva, em um arquivo, um comentário de uma linha explicando o que é Python.
2. Escreva um comentário descrevendo a "Loja da Ana" em uma frase.
3. Escreva um `print()` (sem se preocupar em rodar ainda) que mostraria a frase `"Aprendendo Python para análise de dados"`.
4. Liste, em comentários separados, três tipos de dados que uma loja registraria (ex: nome do produto, preço, quantidade).
5. Escreva um comentário com uma pergunta que a Loja da Ana poderia querer responder com dados (ex: qual produto vende mais).
6. Escreva um `print()` que mostre o nome da loja e, em outra linha, o "objetivo" do sistema de análise.
7. Crie, em comentários, uma lista de três áreas (fora de lojas) que poderiam usar análise de dados.
8. Escreva um comentário explicando, com suas palavras, a diferença entre "aprender Python" e "aprender análise de dados".
9. Escreva um pequeno bloco de comentários (3 linhas) descrevendo o "roteiro" que você imagina para analisar as vendas de um mês.
10. Escreva um `print()` que simule a "abertura" de um relatório, mostrando nome da loja, data fictícia e um separador de linha (ex: `"---"`).

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
# Python é uma linguagem de programação fácil de ler e escrever
```

**2.**
```python
# A Loja da Ana é uma lojinha fictícia de bairro usada como exemplo na apostila
```

**3.**
```python
print("Aprendendo Python para análise de dados")
```

**4.**
```python
# Nome do produto
# Preço do produto
# Quantidade vendida
```

**5.**
```python
# Qual produto vendeu mais no último mês?
```

**6.**
```python
print("Loja da Ana")
print("Objetivo: analisar as vendas para tomar decisões melhores")
```

**7.**
```python
# Mercado financeiro
# Saúde
# Marketing
```

**8.**
```python
# Python é a ferramenta (a linguagem); análise de dados é o objetivo
# (o que fazemos com essa ferramenta, como carregar, limpar e interpretar dados)
```

**9.**
```python
# 1. Carregar os dados de vendas do mês
# 2. Calcular totais e médias
# 3. Descobrir quais produtos venderam mais e menos
```

**10.**
```python
print("Loja da Ana")
print("Data: 01/07/2026")
print("---")
```

</details>

## 2. Ambiente de desenvolvimento

1. Escreva um script que use `print()` para mostrar `"Ola, Loja da Ana!"`.
2. Escreva um script com dois `print()` em linhas separadas, mostrando o nome da loja e o endereço fictício.
3. Adicione um comentário de uma linha no topo de um script explicando o que ele faz.
4. Escreva um script que mostre três linhas: nome da loja, slogan e a frase `"Sistema iniciado"`.
5. Escreva um script com um comentário explicando por que ele existe, seguido de um `print()` com o resultado.
6. Escreva um script que mostre uma "linha decorativa" (ex: `"===================="`) antes e depois de uma mensagem de boas-vindas.
7. Escreva um script que combine comentários e `print()` para simular o início de um relatório de vendas com três linhas de informação.
8. Escreva um script que mostre, em `print()`s separados, o nome de três produtos fictícios da loja.
9. Escreva um script com um bloco de comentários no topo (várias linhas com `#`) descrevendo o propósito do arquivo, seguido de pelo menos dois `print()`.
10. Escreva um script completo que simule a abertura de um "relatório de vendas do dia", com comentários explicativos e pelo menos quatro `print()`s organizados (título, data, separador, mensagem final).

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
print("Ola, Loja da Ana!")
```

**2.**
```python
print("Loja da Ana")
print("Rua das Flores, 123")
```

**3.**
```python
# Script de teste do ambiente de desenvolvimento
print("Ambiente configurado com sucesso")
```

**4.**
```python
print("Loja da Ana")
print("Qualidade que cabe no seu bolso")
print("Sistema iniciado")
```

**5.**
```python
# Este script mostra a saudação inicial do sistema da loja
print("Bem-vindo ao sistema da Loja da Ana")
```

**6.**
```python
print("====================")
print("Bem-vindo à Loja da Ana!")
print("====================")
```

**7.**
```python
# Início do relatório de vendas da Loja da Ana
print("Relatorio de Vendas")
print("Loja da Ana")
print("Dia: 01")
```

**8.**
```python
print("Caneta Azul")
print("Caderno")
print("Mochila")
```

**9.**
```python
# Este script inicializa o sistema de vendas da Loja da Ana.
# Ele mostra uma saudação e confirma que o ambiente está pronto.
print("Sistema da Loja da Ana")
print("Ambiente pronto para uso")
```

**10.**
```python
# Relatorio de abertura do dia - Loja da Ana
print("Relatorio de Vendas")
print("Data: 01/07/2026")
print("---")
print("Relatorio gerado com sucesso")
```

</details>

## 3. Variáveis e print()

1. Crie uma variável `nome_loja` com o valor `"Loja da Ana"` e mostre-a com `print()`.
2. Crie variáveis `produto` e `preco` e mostre ambas em um único `print()`, separadas por vírgula.
3. Crie uma variável `faturamento_dia` com o valor `450.75` e mostre uma mensagem `"Faturamento do dia:"` seguida do valor.
4. Crie uma variável `quantidade_vendas` e reatribua um novo valor a ela; mostre o valor antes e depois da mudança.
5. Crie três variáveis (`vendedor`, `produto`, `valor`) e mostre-as todas em um único `print()`.
6. Crie uma variável `nome_produto` com um nome inválido propositalmente incorreto (ex: começando com número) e corrija para um nome válido, mostrando o valor.
7. Crie duas variáveis com o mesmo valor inicial e altere apenas uma delas; mostre que a outra não mudou.
8. Usando f-string, mostre uma frase que combine o nome de um produto e seu preço em uma única mensagem.
9. Crie variáveis para representar uma venda completa (`vendedor`, `produto`, `valor`, `forma_pagamento`) e mostre um resumo formatado com f-string.
10. Crie uma variável `total_vendas` a partir da soma de três outras variáveis numéricas já existentes e mostre o resultado com uma mensagem explicativa.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
nome_loja = "Loja da Ana"
print(nome_loja)
```

**2.**
```python
produto = "Caneta Azul"
preco = 5.90
print(produto, preco)
```

**3.**
```python
faturamento_dia = 450.75
print("Faturamento do dia:", faturamento_dia)
```

**4.**
```python
quantidade_vendas = 10
print("Antes:", quantidade_vendas)
quantidade_vendas = 15
print("Depois:", quantidade_vendas)
```

**5.**
```python
vendedor = "Ana"
produto = "Caderno"
valor = 12.50
print(vendedor, produto, valor)
```

**6.**
```python
# 1produto = "Caneta"  # inválido: nome de variável não pode começar com número
nome_produto = "Caneta"
print(nome_produto)
```

**7.**
```python
preco_original = 20.00
preco_promocional = preco_original
preco_promocional = 15.00
print("Original:", preco_original)
print("Promocional:", preco_promocional)
```

**8.**
```python
produto = "Mochila"
preco = 89.90
print(f"{produto} custa R$ {preco}")
```

**9.**
```python
vendedor = "Ana"
produto = "Tenis"
valor = 150.00
forma_pagamento = "cartao"
print(f"Venda: {produto} por R$ {valor}, vendedor {vendedor}, pagamento em {forma_pagamento}")
```

**10.**
```python
venda_1 = 45.90
venda_2 = 120.00
venda_3 = 15.50
total_vendas = venda_1 + venda_2 + venda_3
print("Total das três vendas:", total_vendas)
```

</details>

## 4. Inteiros (int)

1. Crie uma variável `quantidade_itens` com um número inteiro e mostre seu tipo com `type()`.
2. Some dois números inteiros representando quantidades de produtos vendidos e mostre o resultado.
3. Subtraia a quantidade de itens devolvidos da quantidade total vendida e mostre o resultado.
4. Multiplique a quantidade de um produto pela quantidade de caixas para descobrir o total de unidades.
5. Use `int()` para converter o texto `"25"` (quantidade de vendas) em número inteiro e some 5 a ele.
6. Verifique, com `type()`, se o resultado da divisão inteira (`//`) entre dois inteiros continua sendo `int`.
7. Crie uma variável inteira negativa representando um estorno e some-a a um total positivo.
8. Compare, usando `type()`, o tipo de `10` e o tipo de `10.0`, e explique em um comentário a diferença observada.
9. Crie uma lista de três números inteiros representando vendas por hora e some-os manualmente (sem usar `sum()`), guardando o resultado em uma variável.
10. Escreva um pequeno cálculo que combine soma, subtração e multiplicação de inteiros para simular o estoque final de um produto (estoque inicial + reposição - vendido).

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
quantidade_itens = 12
print(type(quantidade_itens))
```

**2.**
```python
vendidos_manha = 8
vendidos_tarde = 15
total = vendidos_manha + vendidos_tarde
print(total)
```

**3.**
```python
total_vendido = 50
devolvidos = 3
total_final = total_vendido - devolvidos
print(total_final)
```

**4.**
```python
itens_por_caixa = 24
quantidade_caixas = 5
total_unidades = itens_por_caixa * quantidade_caixas
print(total_unidades)
```

**5.**
```python
quantidade_texto = "25"
quantidade = int(quantidade_texto) + 5
print(quantidade)
```

**6.**
```python
resultado = 17 // 5
print(type(resultado))
```

**7.**
```python
total_positivo = 500
estorno = -50
total_final = total_positivo + estorno
print(total_final)
```

**8.**
```python
print(type(10))    # <class 'int'>
print(type(10.0))  # <class 'float'>
# 10 não tem casas decimais; 10.0 tem, por isso são tipos diferentes
```

**9.**
```python
vendas_hora_1 = 3
vendas_hora_2 = 5
vendas_hora_3 = 2
total = vendas_hora_1 + vendas_hora_2 + vendas_hora_3
print(total)
```

**10.**
```python
estoque_inicial = 100
reposicao = 30
vendido = 45
estoque_final = estoque_inicial + reposicao - vendido
print("Estoque final:", estoque_final)
```

</details>

## 5. Floats

1. Crie uma variável `preco_produto` com um valor decimal e mostre seu tipo com `type()`.
2. Some dois valores decimais representando o preço de dois produtos.
3. Divida um valor de faturamento inteiro por uma quantidade de vendas e mostre o resultado (deve dar float).
4. Use `round()` para arredondar `19.876` para duas casas decimais.
5. Multiplique um preço por uma quantidade fracionária (ex: 1.5 kg) e mostre o total.
6. Demonstre, com um `print()`, um caso clássico de imprecisão de ponto flutuante (ex: `0.1 + 0.2`).
7. Use `round()` sem o segundo argumento para arredondar `45.6` para o inteiro mais próximo, e mostre o tipo do resultado.
8. Calcule o preço médio de três produtos com preços decimais diferentes, usando `round()` no resultado final.
9. Crie uma variável de desconto em porcentagem (float) e aplique-a sobre um preço, mostrando o valor final arredondado em duas casas.
10. Escreva um cálculo que simule o troco de uma compra: valor pago (float) menos o total da compra (float), com o resultado arredondado em duas casas.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
preco_produto = 19.90
print(type(preco_produto))
```

**2.**
```python
preco_1 = 12.50
preco_2 = 8.75
total = preco_1 + preco_2
print(total)
```

**3.**
```python
faturamento = 500
quantidade_vendas = 8
ticket_medio = faturamento / quantidade_vendas
print(ticket_medio)
```

**4.**
```python
valor = round(19.876, 2)
print(valor)
```

**5.**
```python
preco_kg = 8.50
peso = 1.5
total = preco_kg * peso
print(total)
```

**6.**
```python
print(0.1 + 0.2)  # 0.30000000000000004, por causa da representação binária de floats
```

**7.**
```python
valor_arredondado = round(45.6)
print(valor_arredondado)
print(type(valor_arredondado))
```

**8.**
```python
preco_1 = 10.90
preco_2 = 25.50
preco_3 = 7.30
preco_medio = round((preco_1 + preco_2 + preco_3) / 3, 2)
print(preco_medio)
```

**9.**
```python
preco = 89.90
desconto_percentual = 0.15
preco_final = round(preco - (preco * desconto_percentual), 2)
print(preco_final)
```

**10.**
```python
valor_pago = 50.00
total_compra = 37.45
troco = round(valor_pago - total_compra, 2)
print(troco)
```

</details>

## 6. Booleanos

1. Crie uma variável `loja_aberta` com o valor `True` e mostre seu tipo com `type()`.
2. Crie uma variável `estoque_vazio` com o valor `False` e mostre-a com `print()`.
3. Avalie a expressão `10 > 5` e guarde o resultado em uma variável booleana.
4. Verifique se o valor `0` é considerado "verdadeiro" ou "falso" usando `bool()`.
5. Verifique se uma string vazia (`""`) e uma string não vazia (`"Ana"`) são `True` ou `False` com `bool()`.
6. Crie uma variável `cliente_fidelidade` como booleano e use-a para decidir (sem `if`, apenas mostrando o valor) se o cliente ganha desconto.
7. Use `bool()` para verificar se uma lista vazia (`[]`) e uma lista com itens são `True` ou `False`.
8. Combine duas variáveis booleanas com `and` e mostre o resultado.
9. Combine duas variáveis booleanas com `or` e mostre o resultado.
10. Crie duas variáveis representando "tem_estoque" e "cliente_pagou", e mostre o resultado da expressão booleana que representa "a venda pode ser concluída" (ambas precisam ser verdadeiras).

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
loja_aberta = True
print(type(loja_aberta))
```

**2.**
```python
estoque_vazio = False
print(estoque_vazio)
```

**3.**
```python
resultado = 10 > 5
print(resultado)
```

**4.**
```python
print(bool(0))  # False
```

**5.**
```python
print(bool(""))     # False
print(bool("Ana"))  # True
```

**6.**
```python
cliente_fidelidade = True
print(cliente_fidelidade)
```

**7.**
```python
print(bool([]))              # False
print(bool([45.90, 12.00]))  # True
```

**8.**
```python
tem_estoque = True
cliente_pagou = False
resultado = tem_estoque and cliente_pagou
print(resultado)
```

**9.**
```python
promocao_ativa = False
cliente_fidelidade = True
resultado = promocao_ativa or cliente_fidelidade
print(resultado)
```

**10.**
```python
tem_estoque = True
cliente_pagou = True
venda_pode_ser_concluida = tem_estoque and cliente_pagou
print(venda_pode_ser_concluida)
```

</details>

## 7. Conversão de tipos (type casting)

1. Converta a string `"120"` para inteiro e some 30 a ela.
2. Converta a string `"19.90"` para float e mostre seu tipo.
3. Converta o número inteiro `45` para string e concatene com `" reais"`.
4. Converta o float `10.0` para inteiro e mostre o resultado.
5. Tente converter a string `"vinte"` para inteiro e explique, em comentário, por que isso gera erro.
6. Converta o booleano `True` para inteiro e mostre o resultado numérico.
7. Converta o número `0` para booleano e mostre o resultado.
8. Some o preço de um produto (float) com uma string numérica convertida para float, mostrando o resultado.
9. Crie uma função de conversão manual: dada uma string com valor de venda (ex: `"150.75"`), converta para float e classifique como "acima de 100" ou "até 100".
10. Dada a lista de strings `["10", "25", "8"]` representando quantidades vendidas, converta cada item para inteiro (usando um laço, sem `int()` direto na lista) e some o total.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
quantidade = int("120") + 30
print(quantidade)
```

**2.**
```python
preco = float("19.90")
print(type(preco))
```

**3.**
```python
valor = 45
texto = str(valor) + " reais"
print(texto)
```

**4.**
```python
valor = int(10.0)
print(valor)
```

**5.**
```python
# int("vinte") gera ValueError, porque "vinte" não é um número em formato
# reconhecível pelo Python -- só dígitos (e sinal/decimal) podem ser convertidos
```

**6.**
```python
valor = int(True)
print(valor)  # 1
```

**7.**
```python
valor = bool(0)
print(valor)  # False
```

**8.**
```python
preco = 10.50
preco_extra_texto = "5.25"
total = preco + float(preco_extra_texto)
print(total)
```

**9.**
```python
venda_texto = "150.75"
venda = float(venda_texto)

if venda > 100:
    print("Acima de 100")
else:
    print("Até 100")
```

**10.**
```python
quantidades_texto = ["10", "25", "8"]
total = 0

for quantidade in quantidades_texto:
    total = total + int(quantidade)

print(total)
```

</details>

## 8. Operadores aritméticos

1. Some dois valores de venda e mostre o total.
2. Subtraia o valor de um desconto de um preço original.
3. Multiplique o preço de um produto pela quantidade comprada.
4. Divida o faturamento total pela quantidade de vendas para achar o ticket médio.
5. Use o operador `//` para descobrir quantas caixas fechadas de 12 unidades cabem em um estoque de 50 itens.
6. Use o operador `%` para descobrir quantas unidades sobram depois de formar caixas fechadas de 12 no exemplo anterior.
7. Use o operador `**` para calcular o quadrado de uma quantidade de vendas (uso didático, sem sentido de negócio).
8. Calcule o valor final de uma venda com acréscimo de 10% usando multiplicação.
9. Combine soma, subtração e divisão em uma única expressão para calcular o lucro médio por venda (faturamento - custo, dividido pela quantidade de vendas).
10. Escreva uma expressão que calcule o valor total de uma compra com desconto percentual e depois some o valor do frete, tudo em uma linha.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
venda_1 = 45.90
venda_2 = 30.00
total = venda_1 + venda_2
print(total)
```

**2.**
```python
preco_original = 100.00
desconto = 15.00
preco_final = preco_original - desconto
print(preco_final)
```

**3.**
```python
preco = 12.50
quantidade = 4
total = preco * quantidade
print(total)
```

**4.**
```python
faturamento = 890.00
quantidade_vendas = 10
ticket_medio = faturamento / quantidade_vendas
print(ticket_medio)
```

**5.**
```python
estoque = 50
caixas_fechadas = estoque // 12
print(caixas_fechadas)
```

**6.**
```python
estoque = 50
unidades_restantes = estoque % 12
print(unidades_restantes)
```

**7.**
```python
vendas = 4
quadrado = vendas ** 2
print(quadrado)
```

**8.**
```python
preco = 80.00
preco_com_acrescimo = preco * 1.10
print(preco_com_acrescimo)
```

**9.**
```python
faturamento = 1000.00
custo = 600.00
quantidade_vendas = 20
lucro_medio = (faturamento - custo) / quantidade_vendas
print(lucro_medio)
```

**10.**
```python
preco = 200.00
desconto_percentual = 0.10
frete = 15.00
total = (preco - preco * desconto_percentual) + frete
print(total)
```

</details>

## 9. Operadores de comparação

1. Compare se `venda_1` é maior que `venda_2` usando `>`.
2. Verifique se o estoque atual é igual a zero usando `==`.
3. Verifique se dois nomes de produtos digitados de formas diferentes ("Caneta" e "caneta") são iguais.
4. Verifique se uma venda é diferente de outra usando `!=`.
5. Verifique se a quantidade em estoque é menor ou igual a um limite mínimo definido.
6. Compare o preço de dois produtos e mostre qual comparação (`>`, `<` ou `==`) é verdadeira.
7. Verifique se um valor de venda está dentro de uma faixa, comparando com `>=` e `<=` separadamente.
8. Compare a quantidade vendida hoje com a quantidade vendida ontem e mostre se houve crescimento.
9. Verifique se dois valores float que deveriam ser "iguais" após um cálculo realmente são iguais com `==` (explore possíveis imprecisões).
10. Escreva comparações que verifiquem, para um produto, se o preço está exatamente igual a um valor de promoção e se o estoque é maior que zero, mostrando os dois resultados separadamente.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
venda_1 = 120.00
venda_2 = 89.90
print(venda_1 > venda_2)
```

**2.**
```python
estoque_atual = 0
print(estoque_atual == 0)
```

**3.**
```python
produto_1 = "Caneta"
produto_2 = "caneta"
print(produto_1 == produto_2)  # False, maiúsculas/minúsculas importam
```

**4.**
```python
venda_1 = 45.90
venda_2 = 60.00
print(venda_1 != venda_2)
```

**5.**
```python
estoque_atual = 3
limite_minimo = 5
print(estoque_atual <= limite_minimo)
```

**6.**
```python
preco_1 = 25.00
preco_2 = 30.00
print(preco_1 < preco_2)
```

**7.**
```python
venda = 150.00
dentro_da_faixa = venda >= 100 and venda <= 200
print(venda >= 100)
print(venda <= 200)
```

**8.**
```python
vendas_hoje = 12
vendas_ontem = 9
print(vendas_hoje > vendas_ontem)
```

**9.**
```python
resultado = 0.1 + 0.2
print(resultado == 0.3)  # False, por causa da imprecisão de ponto flutuante
```

**10.**
```python
preco = 49.90
preco_promocao = 49.90
estoque = 8

print(preco == preco_promocao)
print(estoque > 0)
```

</details>

## 10. Operadores lógicos

1. Verifique se uma venda é maior que 50 **e** a forma de pagamento é `"cartao"`.
2. Verifique se um cliente é novo **ou** tem cadastro de fidelidade.
3. Use `not` para inverter o valor de uma variável booleana que representa `loja_fechada`.
4. Combine três condições com `and` para verificar se uma venda é grande, à vista e sem desconto.
5. Combine `and` e `or` para verificar se um cliente ganha frete grátis (compra acima de R$ 150 **ou** é fidelidade, **e** mora na cidade da loja).
6. Use `not` junto com uma comparação para verificar se um produto **não** está em falta de estoque.
7. Verifique se **nenhuma** das duas condições é verdadeira, usando `not` combinado com `or`.
8. Escreva uma expressão que combine `and`, `or` e `not` para decidir se uma promoção se aplica a uma venda.
9. Dadas três variáveis booleanas (`tem_estoque`, `cliente_pagou`, `endereco_valido`), verifique se a venda pode ser enviada (todas precisam ser verdadeiras).
10. Escreva uma expressão lógica completa que determine se um cliente recebe desconto de aniversário: precisa ter cadastro válido **e** (ser mês de aniversário **ou** ter comprado acima de R$ 300).

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
venda = 80.00
forma_pagamento = "cartao"
resultado = venda > 50 and forma_pagamento == "cartao"
print(resultado)
```

**2.**
```python
cliente_novo = False
tem_fidelidade = True
resultado = cliente_novo or tem_fidelidade
print(resultado)
```

**3.**
```python
loja_fechada = False
print(not loja_fechada)
```

**4.**
```python
venda_grande = True
pagamento_a_vista = True
sem_desconto = True
resultado = venda_grande and pagamento_a_vista and sem_desconto
print(resultado)
```

**5.**
```python
valor_compra = 200.00
tem_fidelidade = False
mora_na_cidade = True
frete_gratis = (valor_compra > 150 or tem_fidelidade) and mora_na_cidade
print(frete_gratis)
```

**6.**
```python
estoque = 5
resultado = not (estoque == 0)
print(resultado)
```

**7.**
```python
promocao_ativa = False
cupom_valido = False
nenhuma_condicao = not (promocao_ativa or cupom_valido)
print(nenhuma_condicao)
```

**8.**
```python
venda = 220.00
cliente_fidelidade = True
produto_em_liquidacao = False

promocao_se_aplica = (venda > 200 or cliente_fidelidade) and not produto_em_liquidacao
print(promocao_se_aplica)
```

**9.**
```python
tem_estoque = True
cliente_pagou = True
endereco_valido = True

pode_enviar = tem_estoque and cliente_pagou and endereco_valido
print(pode_enviar)
```

**10.**
```python
cadastro_valido = True
mes_aniversario = False
valor_compra = 350.00

desconto_aniversario = cadastro_valido and (mes_aniversario or valor_compra > 300)
print(desconto_aniversario)
```

</details>

## 11. Condicionais (if/elif/else)

1. Dado o valor de uma venda, mostre `"Venda grande"` se for maior que 100, senão `"Venda pequena"`.
2. Classifique uma quantidade em estoque como `"Estoque baixo"` (menor que 10) ou `"Estoque ok"`.
3. Dado um preço, use `if/elif/else` para classificar como `"caro"` (acima de 100), `"médio"` (entre 30 e 100) ou `"barato"` (abaixo de 30).
4. Verifique se um cliente pode receber desconto: se a compra for maior que R$ 200, mostre `"Desconto aplicado"`, senão `"Sem desconto"`.
5. Dado um número de vendas do dia, mostre `"Meta batida"` se for maior ou igual a 20, senão `"Meta não batida"`.
6. Combine uma condicional com operador lógico: se a venda for maior que 150 **e** a forma de pagamento for `"pix"`, aplique 10% de desconto (mostre o valor final).
7. Classifique o desempenho de um vendedor com `if/elif/else` em três faixas de vendas totais: `"ótimo"` (>= 5000), `"bom"` (>= 2000) e `"regular"` (abaixo de 2000).
8. Dado o estoque de um produto, mostre uma mensagem diferente para `"esgotado"` (0), `"baixo"` (1 a 5) e `"disponível"` (acima de 5).
9. Escreva uma condicional aninhada (`if` dentro de `if`) que primeiro verifica se a loja está aberta e, se estiver, verifica se há estoque do produto.
10. Dada uma lista de três vendas, use um `for` combinado com `if/elif/else` para classificar cada uma em `"grande"`, `"média"` ou `"pequena"`, mostrando o resultado de cada uma.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
venda = 150.00
if venda > 100:
    print("Venda grande")
else:
    print("Venda pequena")
```

**2.**
```python
estoque = 4
if estoque < 10:
    print("Estoque baixo")
else:
    print("Estoque ok")
```

**3.**
```python
preco = 55.00
if preco > 100:
    print("caro")
elif preco >= 30:
    print("médio")
else:
    print("barato")
```

**4.**
```python
compra = 250.00
if compra > 200:
    print("Desconto aplicado")
else:
    print("Sem desconto")
```

**5.**
```python
vendas_do_dia = 22
if vendas_do_dia >= 20:
    print("Meta batida")
else:
    print("Meta não batida")
```

**6.**
```python
venda = 180.00
forma_pagamento = "pix"

if venda > 150 and forma_pagamento == "pix":
    valor_final = venda * 0.90
    print("Valor com desconto:", valor_final)
else:
    print("Valor final:", venda)
```

**7.**
```python
total_vendido = 3200
if total_vendido >= 5000:
    print("ótimo")
elif total_vendido >= 2000:
    print("bom")
else:
    print("regular")
```

**8.**
```python
estoque = 3
if estoque == 0:
    print("esgotado")
elif estoque <= 5:
    print("baixo")
else:
    print("disponível")
```

**9.**
```python
loja_aberta = True
tem_estoque = True

if loja_aberta:
    if tem_estoque:
        print("Pode vender")
    else:
        print("Loja aberta, mas sem estoque")
else:
    print("Loja fechada")
```

**10.**
```python
vendas = [35.00, 89.90, 300.00]

for venda in vendas:
    if venda >= 200:
        print(venda, "- grande")
    elif venda >= 50:
        print(venda, "- média")
    else:
        print(venda, "- pequena")
```

</details>

## 12. Loops (for/while)

1. Use um `for` para percorrer a lista `[45.90, 120.00, 15.50]` e mostrar cada venda.
2. Use um `for` com `range()` para mostrar os números de 1 a 10.
3. Use um `while` para mostrar uma contagem regressiva de 5 até 1.
4. Some, com um `for`, todos os valores de uma lista de vendas, sem usar `sum()`.
5. Use um `for` para contar quantas vendas de uma lista são maiores que R$ 100.
6. Use `break` para parar um `for` assim que encontrar a primeira venda acima de R$ 200.
7. Use `continue` em um `for` para pular vendas negativas (estornos) e somar apenas as positivas.
8. Use um `while` para simular a adição de vendas a uma lista até ela atingir 5 itens.
9. Use `for` com `range()` e passo (terceiro argumento) para mostrar apenas os números pares de 0 a 20.
10. Combine `for` com `if/elif/else` para percorrer uma lista de vendas e contar, separadamente, quantas são grandes, médias e pequenas (segundo os critérios do tópico de condicionais).

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
vendas = [45.90, 120.00, 15.50]
for venda in vendas:
    print(venda)
```

**2.**
```python
for numero in range(1, 11):
    print(numero)
```

**3.**
```python
contador = 5
while contador >= 1:
    print(contador)
    contador -= 1
```

**4.**
```python
vendas = [45.90, 120.00, 15.50, 33.00]
total = 0
for venda in vendas:
    total += venda
print(total)
```

**5.**
```python
vendas = [45.90, 120.00, 15.50, 200.00]
contador = 0
for venda in vendas:
    if venda > 100:
        contador += 1
print(contador)
```

**6.**
```python
vendas = [45.90, 120.00, 250.00, 89.90]
for venda in vendas:
    if venda > 200:
        print("Primeira venda grande encontrada:", venda)
        break
```

**7.**
```python
vendas = [45.90, -20.00, 120.00, -5.00]
total = 0
for venda in vendas:
    if venda < 0:
        continue
    total += venda
print(total)
```

**8.**
```python
vendas = []
proxima_venda = 10.00
while len(vendas) < 5:
    vendas.append(proxima_venda)
    proxima_venda += 5.00
print(vendas)
```

**9.**
```python
for numero in range(0, 21, 2):
    print(numero)
```

**10.**
```python
vendas = [35.00, 89.90, 300.00, 150.00, 20.00]
grandes = 0
medias = 0
pequenas = 0

for venda in vendas:
    if venda >= 200:
        grandes += 1
    elif venda >= 50:
        medias += 1
    else:
        pequenas += 1

print("Grandes:", grandes)
print("Médias:", medias)
print("Pequenas:", pequenas)
```

</details>

## 13. Strings (fundamentos)

1. Crie uma variável com o nome de um produto e mostre seu tipo com `type()`.
2. Concatene o nome de um produto com sua categoria usando `+`.
3. Acesse o primeiro e o último caractere do nome de um produto usando índices.
4. Use fatiamento (`slicing`) para pegar os três primeiros caracteres do nome de um produto.
5. Descubra o tamanho (quantidade de caracteres) do nome de um produto com `len()`.
6. Crie uma f-string que combine o nome de um produto e seu preço em uma única frase.
7. Concatene três strings (nome do vendedor, produto e forma de pagamento) em uma única frase, separadas por vírgulas.
8. Use fatiamento com passo negativo (`[::-1]`) para inverter o nome de um produto.
9. Verifique, com o operador `in`, se a palavra `"Caneta"` está contida no texto `"Caneta Azul BIC"`.
10. Combine f-string, concatenação e fatiamento em um único bloco de código para montar um "código de produto" a partir das três primeiras letras do nome em maiúsculas mais o preço.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
produto = "Caneta Azul"
print(type(produto))
```

**2.**
```python
nome = "Caneta Azul"
categoria = "Papelaria"
descricao = nome + " - " + categoria
print(descricao)
```

**3.**
```python
produto = "Caneta Azul"
print(produto[0])
print(produto[-1])
```

**4.**
```python
produto = "Caneta Azul"
print(produto[0:3])
```

**5.**
```python
produto = "Caneta Azul"
print(len(produto))
```

**6.**
```python
produto = "Caneta Azul"
preco = 5.90
print(f"{produto} custa R$ {preco}")
```

**7.**
```python
vendedor = "Ana"
produto = "Caderno"
pagamento = "pix"
frase = vendedor + ", " + produto + ", " + pagamento
print(frase)
```

**8.**
```python
produto = "Caneta Azul"
print(produto[::-1])
```

**9.**
```python
texto = "Caneta Azul BIC"
print("Caneta" in texto)
```

**10.**
```python
produto = "caneta azul"
preco = 5.90
codigo = produto[0:3].upper() + f"-{preco}"
print(codigo)
```

</details>

## 14. Trabalhando com strings (métodos gerais)

1. Converta o nome de um produto para letras maiúsculas com `.upper()`.
2. Converta o nome de um produto para letras minúsculas com `.lower()`.
3. Verifique se o texto `"promocao"` começa com `"pro"` usando `.startswith()`.
4. Verifique se o texto `"caneta.txt"` termina com `.txt` usando `.endswith()`.
5. Conte quantas vezes a letra `"a"` aparece no nome de um produto usando `.count()`.
6. Encontre a posição da palavra `"Azul"` dentro do texto `"Caneta Azul BIC"` usando `.find()`.
7. Deixe a primeira letra de cada palavra do nome de um produto maiúscula usando `.title()`.
8. Verifique se um texto digitado por um cliente é composto só por números usando `.isdigit()`.
9. Combine `.lower()` e `in` para verificar se a palavra `"caneta"` aparece em `"CANETA AZUL BIC"`, ignorando maiúsculas/minúsculas.
10. Dada uma lista de nomes de produtos escritos de forma inconsistente (`["caneta azul", "CADERNO", "Mochila Escolar"]`), use `.title()` em cada um (com um `for`) para padronizar a formatação.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
produto = "caneta azul"
print(produto.upper())
```

**2.**
```python
produto = "CANETA AZUL"
print(produto.lower())
```

**3.**
```python
texto = "promocao"
print(texto.startswith("pro"))
```

**4.**
```python
arquivo = "caneta.txt"
print(arquivo.endswith(".txt"))
```

**5.**
```python
produto = "Caneta Azul"
print(produto.count("a"))
```

**6.**
```python
texto = "Caneta Azul BIC"
posicao = texto.find("Azul")
print(posicao)
```

**7.**
```python
produto = "caneta azul"
print(produto.title())
```

**8.**
```python
entrada_cliente = "12345"
print(entrada_cliente.isdigit())
```

**9.**
```python
texto = "CANETA AZUL BIC"
print("caneta" in texto.lower())
```

**10.**
```python
produtos = ["caneta azul", "CADERNO", "Mochila Escolar"]

for produto in produtos:
    print(produto.title())
```

</details>

## 15. strip, replace, split

1. Remova os espaços em branco do início e do fim do texto `"  Caneta Azul  "` usando `.strip()`.
2. Substitua a palavra `"Azul"` por `"Vermelha"` no texto `"Caneta Azul"` usando `.replace()`.
3. Divida o texto `"Caneta,Caderno,Mochila"` em uma lista de produtos usando `.split(",")`.
4. Remova apenas os espaços da esquerda do texto `"   Caneta"` usando `.lstrip()`.
5. Remova apenas os espaços da direita do texto `"Caneta   "` usando `.rstrip()`.
6. Divida a frase `"Ana vendeu 5 canetas"` em palavras usando `.split()` (sem argumento) e mostre a lista resultante.
7. Substitua todas as vírgulas por ponto e vírgula no texto `"45,90"` (simulando conversão de formato numérico) usando `.replace()`.
8. Combine `.strip()` e `.split(",")` para limpar e separar o texto `"  Caneta , Caderno , Mochila  "` em uma lista de produtos sem espaços sobrando.
9. Dada a string `"vendedor:Ana;produto:Caneta;valor:45.90"`, use `.split(";")` para separar os campos e depois `.split(":")` em cada um para separar chave e valor.
10. Escreva uma sequência de operações que receba a string `"  RELATORIO-DE-VENDAS  "`, remova os espaços com `.strip()`, substitua os hífens por espaços com `.replace()` e converta para o formato título com `.title()`.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
texto = "  Caneta Azul  "
print(texto.strip())
```

**2.**
```python
texto = "Caneta Azul"
print(texto.replace("Azul", "Vermelha"))
```

**3.**
```python
texto = "Caneta,Caderno,Mochila"
produtos = texto.split(",")
print(produtos)
```

**4.**
```python
texto = "   Caneta"
print(texto.lstrip())
```

**5.**
```python
texto = "Caneta   "
print(texto.rstrip())
```

**6.**
```python
frase = "Ana vendeu 5 canetas"
palavras = frase.split()
print(palavras)
```

**7.**
```python
texto = "45,90"
texto_corrigido = texto.replace(",", ";")
print(texto_corrigido)
```

**8.**
```python
texto = "  Caneta , Caderno , Mochila  "
produtos = [produto.strip() for produto in texto.strip().split(",")]
print(produtos)
```

**9.**
```python
texto = "vendedor:Ana;produto:Caneta;valor:45.90"
campos = texto.split(";")

for campo in campos:
    chave, valor = campo.split(":")
    print(chave, "->", valor)
```

**10.**
```python
texto = "  RELATORIO-DE-VENDAS  "
texto_limpo = texto.strip().replace("-", " ").title()
print(texto_limpo)
```

</details>

## 16. Listas

1. Crie uma lista `vendas_do_dia` com cinco valores de venda e mostre-a com `print()`.
2. Descubra quantos itens tem a lista `vendas_do_dia` usando `len()`.
3. Acesse a primeira e a última venda da lista usando índices.
4. Use `sum()`, `max()` e `min()` na lista de vendas e mostre os três resultados.
5. Adicione uma nova venda ao final da lista usando `.append()`.
6. Remova uma venda específica da lista usando `.remove()`.
7. Use um `for` para percorrer a lista de vendas e mostrar cada uma marcada como `"grande"` (acima de 100) ou `"pequena"`.
8. Use fatiamento para obter apenas as três primeiras vendas da lista.
9. Crie uma lista de produtos onde cada item é, na verdade, outra lista com `[nome, preço, quantidade]`, e mostre o nome e o preço do segundo produto.
10. Dada a lista `[45.90, 120.00, 15.50, 200.00, 33.00]`, remova a menor venda com `.remove(min(...))` e, em seguida, adicione uma nova venda de R$ 60.00, mostrando a lista final e o novo total com `sum()`.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
vendas_do_dia = [45.90, 120.00, 15.50, 200.00, 33.00]
print(vendas_do_dia)
```

**2.**
```python
vendas_do_dia = [45.90, 120.00, 15.50, 200.00, 33.00]
print(len(vendas_do_dia))
```

**3.**
```python
vendas_do_dia = [45.90, 120.00, 15.50, 200.00, 33.00]
print(vendas_do_dia[0])
print(vendas_do_dia[-1])
```

**4.**
```python
vendas_do_dia = [45.90, 120.00, 15.50, 200.00, 33.00]
print(sum(vendas_do_dia))
print(max(vendas_do_dia))
print(min(vendas_do_dia))
```

**5.**
```python
vendas_do_dia = [45.90, 120.00, 15.50]
vendas_do_dia.append(89.00)
print(vendas_do_dia)
```

**6.**
```python
vendas_do_dia = [45.90, 120.00, 15.50, 200.00]
vendas_do_dia.remove(15.50)
print(vendas_do_dia)
```

**7.**
```python
vendas_do_dia = [45.90, 120.00, 15.50, 200.00]
for venda in vendas_do_dia:
    if venda > 100:
        print(venda, "- grande")
    else:
        print(venda, "- pequena")
```

**8.**
```python
vendas_do_dia = [45.90, 120.00, 15.50, 200.00, 33.00]
tres_primeiras = vendas_do_dia[0:3]
print(tres_primeiras)
```

**9.**
```python
produtos = [
    ["Caneta Azul", 5.90, 10],
    ["Caderno", 12.50, 20],
]
print(produtos[1][0])
print(produtos[1][1])
```

**10.**
```python
vendas_do_dia = [45.90, 120.00, 15.50, 200.00, 33.00]
vendas_do_dia.remove(min(vendas_do_dia))
vendas_do_dia.append(60.00)
print(vendas_do_dia)
print(sum(vendas_do_dia))
```

</details>

## 17. Tuplas

1. Crie uma tupla `coordenadas_loja` com latitude e longitude fictícias e mostre-a com `print()`.
2. Acesse o primeiro item de uma tupla de produto `("Caneta Azul", 5.90, 10)` usando índice.
3. Tente alterar um item de uma tupla e comente, no código, o erro que isso gera.
4. Use "desempacotamento" para atribuir os três valores da tupla `("Caneta Azul", 5.90, 10)` a três variáveis (`nome`, `preco`, `quantidade`).
5. Descubra o tamanho de uma tupla com `len()`.
6. Crie uma lista de tuplas representando três produtos (`nome`, `preco`) e percorra-a com `for`, desempacotando cada tupla.
7. Converta uma lista `[45.90, 120.00, 15.50]` para tupla usando `tuple()`.
8. Verifique se o valor `5.90` está presente na tupla `("Caneta Azul", 5.90, 10)` usando `in`.
9. Concatene duas tuplas de vendas em uma única tupla usando `+`.
10. Dada a lista de tuplas `[("Caneta", 5.90), ("Caderno", 12.50), ("Mochila", 89.90)]`, use um `for` com desempacotamento para calcular e mostrar o total gasto se comprar uma unidade de cada produto.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
coordenadas_loja = (-23.55, -46.63)
print(coordenadas_loja)
```

**2.**
```python
produto = ("Caneta Azul", 5.90, 10)
print(produto[0])
```

**3.**
```python
produto = ("Caneta Azul", 5.90, 10)
# produto[0] = "Caneta Vermelha"
# TypeError: 'tuple' object does not support item assignment -- tuplas são imutáveis
```

**4.**
```python
produto = ("Caneta Azul", 5.90, 10)
nome, preco, quantidade = produto
print(nome, preco, quantidade)
```

**5.**
```python
produto = ("Caneta Azul", 5.90, 10)
print(len(produto))
```

**6.**
```python
produtos = [("Caneta", 5.90), ("Caderno", 12.50), ("Mochila", 89.90)]

for nome, preco in produtos:
    print(nome, "-", preco)
```

**7.**
```python
vendas_lista = [45.90, 120.00, 15.50]
vendas_tupla = tuple(vendas_lista)
print(vendas_tupla)
```

**8.**
```python
produto = ("Caneta Azul", 5.90, 10)
print(5.90 in produto)
```

**9.**
```python
vendas_manha = (45.90, 120.00)
vendas_tarde = (15.50, 200.00)
vendas_do_dia = vendas_manha + vendas_tarde
print(vendas_do_dia)
```

**10.**
```python
produtos = [("Caneta", 5.90), ("Caderno", 12.50), ("Mochila", 89.90)]

total = 0
for nome, preco in produtos:
    total += preco

print(total)
```

</details>

## 18. Dicionários

1. Crie um dicionário `produto` com as chaves `nome`, `preco` e `quantidade` e mostre-o com `print()`.
2. Acesse o valor da chave `preco` do dicionário `produto` usando colchetes.
3. Adicione uma nova chave `categoria` ao dicionário `produto`.
4. Altere o valor da chave `quantidade` do dicionário `produto`.
5. Use `.get()` para acessar a chave `desconto`, que não existe no dicionário, com um valor padrão de `0`.
6. Percorra as chaves de um dicionário de produto usando um `for` com `.keys()`.
7. Percorra os valores de um dicionário de produto usando um `for` com `.values()`.
8. Percorra chaves e valores ao mesmo tempo usando `.items()`.
9. Crie uma lista de dicionários representando três vendas (cada uma com `produto` e `valor`) e some o total com um `for`.
10. Dado o dicionário `estoque = {"Caneta": 10, "Caderno": 5, "Mochila": 0}`, use um `for` com `.items()` para mostrar apenas os produtos com estoque maior que zero, e conte quantos produtos estão esgotados.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
produto = {"nome": "Caneta Azul", "preco": 5.90, "quantidade": 10}
print(produto)
```

**2.**
```python
produto = {"nome": "Caneta Azul", "preco": 5.90, "quantidade": 10}
print(produto["preco"])
```

**3.**
```python
produto = {"nome": "Caneta Azul", "preco": 5.90, "quantidade": 10}
produto["categoria"] = "Papelaria"
print(produto)
```

**4.**
```python
produto = {"nome": "Caneta Azul", "preco": 5.90, "quantidade": 10}
produto["quantidade"] = 15
print(produto)
```

**5.**
```python
produto = {"nome": "Caneta Azul", "preco": 5.90, "quantidade": 10}
desconto = produto.get("desconto", 0)
print(desconto)
```

**6.**
```python
produto = {"nome": "Caneta Azul", "preco": 5.90, "quantidade": 10}
for chave in produto.keys():
    print(chave)
```

**7.**
```python
produto = {"nome": "Caneta Azul", "preco": 5.90, "quantidade": 10}
for valor in produto.values():
    print(valor)
```

**8.**
```python
produto = {"nome": "Caneta Azul", "preco": 5.90, "quantidade": 10}
for chave, valor in produto.items():
    print(chave, "->", valor)
```

**9.**
```python
vendas = [
    {"produto": "Caneta", "valor": 5.90},
    {"produto": "Caderno", "valor": 12.50},
    {"produto": "Mochila", "valor": 89.90},
]

total = 0
for venda in vendas:
    total += venda["valor"]

print(total)
```

**10.**
```python
estoque = {"Caneta": 10, "Caderno": 5, "Mochila": 0}

esgotados = 0
for produto, quantidade in estoque.items():
    if quantidade > 0:
        print(produto, "-", quantidade)
    else:
        esgotados += 1

print("Produtos esgotados:", esgotados)
```

</details>

## 19. Sets

1. Crie um set `categorias` com três categorias de produtos e mostre-o com `print()`.
2. Adicione uma nova categoria ao set usando `.add()`.
3. Crie um set a partir da lista `["Caneta", "Caderno", "Caneta", "Mochila"]` e observe que os itens duplicados desaparecem.
4. Remova um item de um set usando `.remove()`.
5. Verifique se o item `"Caneta"` está presente em um set de produtos usando `in`.
6. Dados dois sets de clientes (`clientes_loja_fisica` e `clientes_loja_online`), use `&` para descobrir os clientes que compraram nos dois canais.
7. Dados os mesmos dois sets, use `|` para descobrir todos os clientes únicos, somando os dois canais.
8. Dados os mesmos dois sets, use `-` para descobrir os clientes que só compraram na loja física.
9. Converta a lista de vendas `[45.90, 120.00, 45.90, 33.00, 120.00]` em um set para descobrir quantos valores de venda únicos existem.
10. Dada a lista de produtos vendidos no dia `["Caneta", "Caderno", "Caneta", "Mochila", "Caderno", "Caneta"]`, use um set para descobrir quantos produtos diferentes foram vendidos e mostre essa lista de produtos únicos ordenada com `sorted()`.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
categorias = {"Papelaria", "Eletrônicos", "Vestuário"}
print(categorias)
```

**2.**
```python
categorias = {"Papelaria", "Eletrônicos"}
categorias.add("Vestuário")
print(categorias)
```

**3.**
```python
produtos = ["Caneta", "Caderno", "Caneta", "Mochila"]
produtos_unicos = set(produtos)
print(produtos_unicos)
```

**4.**
```python
categorias = {"Papelaria", "Eletrônicos", "Vestuário"}
categorias.remove("Eletrônicos")
print(categorias)
```

**5.**
```python
produtos = {"Caneta", "Caderno", "Mochila"}
print("Caneta" in produtos)
```

**6.**
```python
clientes_loja_fisica = {"Ana", "Beto", "Carla"}
clientes_loja_online = {"Beto", "Diego", "Carla"}
clientes_em_ambos = clientes_loja_fisica & clientes_loja_online
print(clientes_em_ambos)
```

**7.**
```python
clientes_loja_fisica = {"Ana", "Beto", "Carla"}
clientes_loja_online = {"Beto", "Diego", "Carla"}
todos_clientes = clientes_loja_fisica | clientes_loja_online
print(todos_clientes)
```

**8.**
```python
clientes_loja_fisica = {"Ana", "Beto", "Carla"}
clientes_loja_online = {"Beto", "Diego", "Carla"}
so_loja_fisica = clientes_loja_fisica - clientes_loja_online
print(so_loja_fisica)
```

**9.**
```python
vendas = [45.90, 120.00, 45.90, 33.00, 120.00]
vendas_unicas = set(vendas)
print(len(vendas_unicas))
```

**10.**
```python
produtos_vendidos = ["Caneta", "Caderno", "Caneta", "Mochila", "Caderno", "Caneta"]
produtos_unicos = set(produtos_vendidos)

print("Quantidade de produtos diferentes:", len(produtos_unicos))
print(sorted(produtos_unicos))
```

</details>

## 20. List comprehensions

1. Crie uma nova lista com o dobro de cada valor da lista `[45.90, 120.00, 15.50]`.
2. Crie uma lista apenas com as vendas maiores que 50, a partir de `[45.90, 120.00, 15.50, 200.00]`.
3. Crie uma lista com o nome de cada produto em maiúsculas, a partir de `["caneta", "caderno", "mochila"]`.
4. Crie uma lista com os quadrados dos números de 1 a 10, usando `range()` dentro da comprehension.
5. Crie uma lista com o resultado de aplicar 5% de acréscimo em cada venda de `[45.90, 120.00, 15.50]`.
6. Crie uma lista apenas com os produtos cujo nome começa com a letra `"C"`, a partir de `["Caneta", "Mochila", "Caderno", "Estojo"]`.
7. Use uma list comprehension com `if/else` embutido para classificar cada venda de `[45.90, 120.00, 15.50, 200.00]` como `"grande"` ou `"pequena"`.
8. Crie uma lista de tuplas `(produto, preco)` a partir de duas listas paralelas, `nomes` e `precos`, usando `zip()` dentro da comprehension.
9. Crie uma lista apenas com os comprimentos (quantidade de caracteres) de cada nome de produto de `["Caneta Azul", "Caderno", "Mochila Escolar"]`.
10. Combine filtro e transformação em uma única list comprehension: a partir de `[45.90, 120.00, 15.50, 200.00, 33.00]`, crie uma lista com 10% de comissão apenas das vendas acima de R$ 50.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
vendas = [45.90, 120.00, 15.50]
dobro = [venda * 2 for venda in vendas]
print(dobro)
```

**2.**
```python
vendas = [45.90, 120.00, 15.50, 200.00]
vendas_grandes = [venda for venda in vendas if venda > 50]
print(vendas_grandes)
```

**3.**
```python
produtos = ["caneta", "caderno", "mochila"]
produtos_maiusculos = [produto.upper() for produto in produtos]
print(produtos_maiusculos)
```

**4.**
```python
quadrados = [numero ** 2 for numero in range(1, 11)]
print(quadrados)
```

**5.**
```python
vendas = [45.90, 120.00, 15.50]
vendas_com_acrescimo = [venda * 1.05 for venda in vendas]
print(vendas_com_acrescimo)
```

**6.**
```python
produtos = ["Caneta", "Mochila", "Caderno", "Estojo"]
produtos_com_c = [produto for produto in produtos if produto.startswith("C")]
print(produtos_com_c)
```

**7.**
```python
vendas = [45.90, 120.00, 15.50, 200.00]
classificacao = ["grande" if venda > 100 else "pequena" for venda in vendas]
print(classificacao)
```

**8.**
```python
nomes = ["Caneta", "Caderno", "Mochila"]
precos = [5.90, 12.50, 89.90]
produtos = [(nome, preco) for nome, preco in zip(nomes, precos)]
print(produtos)
```

**9.**
```python
produtos = ["Caneta Azul", "Caderno", "Mochila Escolar"]
tamanhos = [len(produto) for produto in produtos]
print(tamanhos)
```

**10.**
```python
vendas = [45.90, 120.00, 15.50, 200.00, 33.00]
comissoes = [round(venda * 0.10, 2) for venda in vendas if venda > 50]
print(comissoes)
```

</details>

## 21. Funções e métodos (diferença entre os dois)

1. Use a função `len()` para descobrir o tamanho de uma string de nome de produto.
2. Use o método `.upper()` em uma string de nome de produto e explique, em comentário, por que é um método e não uma função.
3. Use a função `type()` em uma lista de vendas para descobrir seu tipo.
4. Use o método `.append()` em uma lista de vendas e explique, em comentário, por que ele "pertence" à lista.
5. Use a função `sorted()` em uma lista de vendas sem alterar a lista original, e mostre as duas listas (original e ordenada) para provar isso.
6. Use o método `.sort()` na mesma lista de vendas e mostre que, dessa vez, a lista original foi alterada.
7. Encadeie dois métodos de string (`.strip()` e `.lower()`) em um único texto com espaços e letras maiúsculas.
8. Use a função `int()` para converter uma string em número, e o método `.isdigit()` para verificar antes se a conversão é segura.
9. Dado o texto `"  loja da ana  "`, use uma combinação de método (`.strip()`) e função (`len()`) para descobrir quantos caracteres o nome tem sem os espaços.
10. Escreva um pequeno trecho de código que use pelo menos duas funções (`len()`, `type()` ou similar) e dois métodos (`.upper()`, `.append()` ou similar) em conjunto, comentando qual é qual.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
produto = "Caneta Azul"
print(len(produto))
```

**2.**
```python
produto = "caneta azul"
print(produto.upper())
# é um método porque "pertence" à string -- só strings sabem fazer .upper()
```

**3.**
```python
vendas = [45.90, 120.00, 15.50]
print(type(vendas))
```

**4.**
```python
vendas = [45.90, 120.00, 15.50]
vendas.append(89.00)
print(vendas)
# .append() é método porque só listas sabem "adicionar um item a si mesmas"
```

**5.**
```python
vendas = [45.90, 120.00, 15.50, 200.00]
vendas_ordenadas = sorted(vendas)
print("Original:", vendas)
print("Ordenada:", vendas_ordenadas)
```

**6.**
```python
vendas = [45.90, 120.00, 15.50, 200.00]
vendas.sort()
print(vendas)
```

**7.**
```python
texto = "   CANETA AZUL   "
texto_formatado = texto.strip().lower()
print(texto_formatado)
```

**8.**
```python
entrada = "25"
if entrada.isdigit():
    quantidade = int(entrada)
    print(quantidade)
```

**9.**
```python
texto = "  loja da ana  "
tamanho_sem_espacos = len(texto.strip())
print(tamanho_sem_espacos)
```

**10.**
```python
produtos = ["caneta", "caderno"]

# len() e type() são funções
print(len(produtos))
print(type(produtos))

# .append() e .upper() são métodos
produtos.append("mochila")
print(produtos[0].upper())
```

</details>

## 22. Definindo funções (def, parâmetros, return)

1. Defina uma função `saudacao()` sem parâmetros que mostra `"Bem-vindo à Loja da Ana"`.
2. Defina uma função `dobrar(valor)` que recebe um número e retorna o dobro dele.
3. Defina uma função `calcular_desconto(preco, percentual)` que retorna o preço com o desconto aplicado.
4. Defina uma função `classificar_venda(valor)` que retorna `"grande"` se o valor for maior que 100, senão `"pequena"`.
5. Defina uma função `media(lista_valores)` que retorna a média de uma lista de números.
6. Defina uma função `saudacao_personalizada(nome="cliente")` com um parâmetro com valor padrão, e chame-a com e sem argumento.
7. Defina uma função `faturamento_total(vendas)` que recebe uma lista de vendas e retorna a soma total.
8. Defina uma função `aplicar_taxa(preco, taxa=0.05)` que aplica uma taxa padrão de 5%, mas permite outro valor se informado.
9. Defina uma função `resumo_venda(produto, valor)` que retorna uma string formatada como `"Produto: X - Valor: Y"`.
10. Defina uma função `maior_venda(vendas)` que recebe uma lista de vendas e retorna uma tupla com o maior valor e sua posição (índice) na lista.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
def saudacao():
    print("Bem-vindo à Loja da Ana")

saudacao()
```

**2.**
```python
def dobrar(valor):
    return valor * 2

print(dobrar(45))
```

**3.**
```python
def calcular_desconto(preco, percentual):
    return preco - (preco * percentual)

print(calcular_desconto(100, 0.10))
```

**4.**
```python
def classificar_venda(valor):
    if valor > 100:
        return "grande"
    return "pequena"

print(classificar_venda(150))
```

**5.**
```python
def media(lista_valores):
    return sum(lista_valores) / len(lista_valores)

print(media([45.90, 120.00, 15.50]))
```

**6.**
```python
def saudacao_personalizada(nome="cliente"):
    print(f"Bem-vindo, {nome}!")

saudacao_personalizada()
saudacao_personalizada("Ana")
```

**7.**
```python
def faturamento_total(vendas):
    return sum(vendas)

print(faturamento_total([45.90, 120.00, 15.50]))
```

**8.**
```python
def aplicar_taxa(preco, taxa=0.05):
    return preco + (preco * taxa)

print(aplicar_taxa(100))
print(aplicar_taxa(100, 0.10))
```

**9.**
```python
def resumo_venda(produto, valor):
    return f"Produto: {produto} - Valor: {valor}"

print(resumo_venda("Caneta", 5.90))
```

**10.**
```python
def maior_venda(vendas):
    maior = max(vendas)
    posicao = vendas.index(maior)
    return (maior, posicao)

print(maior_venda([45.90, 120.00, 15.50, 200.00]))
```

</details>

## 23. *args e **kwargs

1. Defina uma função `somar_tudo(*valores)` que soma qualquer quantidade de valores recebidos.
2. Chame a função `somar_tudo` com 2 valores e depois com 6 valores, mostrando os dois resultados.
3. Defina uma função `cadastrar_cliente(**dados)` que mostra o dicionário de dados recebidos.
4. Chame `cadastrar_cliente` passando `nome`, `cidade` e `telefone` como argumentos nomeados.
5. Defina uma função `media_vendas(*valores)` que retorna a média dos valores recebidos usando `*args`.
6. Defina uma função `registrar_venda(vendedor, *itens)` que combina um parâmetro fixo com `*args` para listar os itens vendidos por um vendedor.
7. Defina uma função `montar_produto(nome, **detalhes)` que combina um parâmetro fixo com `**kwargs` para montar as informações extras de um produto.
8. Dentro de uma função com `*args`, use um `for` para mostrar cada valor recebido junto de sua posição (use `enumerate()` se preferir, ou percorra normalmente).
9. Defina uma função `maior_valor(*valores)` que retorna o maior entre todos os valores recebidos, usando `max()` sobre a tupla de `*args`.
10. Defina uma função `resumo_completo(vendedor, *vendas, **detalhes)` que mostra o vendedor, a soma das vendas e os detalhes extras (como forma de pagamento e data), e chame-a com pelo menos 3 vendas e 2 detalhes.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
def somar_tudo(*valores):
    return sum(valores)

print(somar_tudo(10, 20))
```

**2.**
```python
def somar_tudo(*valores):
    return sum(valores)

print(somar_tudo(10, 20))
print(somar_tudo(5, 10, 15, 20, 25, 30))
```

**3.**
```python
def cadastrar_cliente(**dados):
    print(dados)

cadastrar_cliente(nome="Ana", cidade="São Paulo")
```

**4.**
```python
def cadastrar_cliente(**dados):
    print(dados)

cadastrar_cliente(nome="Ana", cidade="São Paulo", telefone="11999990000")
```

**5.**
```python
def media_vendas(*valores):
    return sum(valores) / len(valores)

print(media_vendas(45.90, 120.00, 15.50))
```

**6.**
```python
def registrar_venda(vendedor, *itens):
    print(f"Vendedor: {vendedor}")
    print(f"Itens: {itens}")

registrar_venda("Ana", "Caneta", "Caderno", "Mochila")
```

**7.**
```python
def montar_produto(nome, **detalhes):
    print(f"Produto: {nome}")
    print(f"Detalhes: {detalhes}")

montar_produto("Caneta Azul", preco=5.90, categoria="Papelaria")
```

**8.**
```python
def listar_valores(*valores):
    for posicao, valor in enumerate(valores):
        print(f"Posição {posicao}: {valor}")

listar_valores(45.90, 120.00, 15.50)
```

**9.**
```python
def maior_valor(*valores):
    return max(valores)

print(maior_valor(45.90, 120.00, 15.50, 200.00))
```

**10.**
```python
def resumo_completo(vendedor, *vendas, **detalhes):
    print(f"Vendedor: {vendedor}")
    print(f"Total das vendas: {sum(vendas)}")
    print(f"Detalhes: {detalhes}")

resumo_completo("Ana", 45.90, 120.00, 15.50, forma_pagamento="pix", data="01/07/2026")
```

</details>

## 24. Funções lambda

1. Crie uma lambda que recebe um valor e retorna o dobro dele, e chame-a com um valor de teste.
2. Crie uma lambda que recebe dois valores e retorna a soma deles.
3. Use uma lambda diretamente dentro de `sorted()` para ordenar a lista `["Caneta", "AB", "Mochila Escolar"]` por tamanho do texto.
4. Use uma lambda dentro de `sorted()` para ordenar uma lista de tuplas `[(nome, preco), ...]` pelo preço.
5. Use uma lambda dentro de `filter()` para manter apenas as vendas maiores que 50 de uma lista.
6. Use uma lambda dentro de `map()` para aplicar 10% de desconto a cada valor de uma lista de preços.
7. Crie uma lambda que recebe um preço e retorna `True` se ele for maior que 100, `False` caso contrário.
8. Compare, no código, uma função lambda e uma função `def` equivalente que calculam o mesmo resultado (ex: quadrado de um número), mostrando que produzem o mesmo valor.
9. Use uma lambda dentro de `sorted()` com `reverse=True` para ordenar uma lista de vendas da maior para a menor.
10. Combine `filter()` e `map()`, cada um com sua própria lambda, para primeiro filtrar vendas acima de R$ 50 e depois aplicar 5% de comissão sobre elas, mostrando o resultado final como lista.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
dobrar = lambda valor: valor * 2
print(dobrar(10))
```

**2.**
```python
somar = lambda a, b: a + b
print(somar(5, 7))
```

**3.**
```python
produtos = ["Caneta", "AB", "Mochila Escolar"]
produtos_ordenados = sorted(produtos, key=lambda produto: len(produto))
print(produtos_ordenados)
```

**4.**
```python
produtos = [("Caneta", 5.90), ("Mochila", 89.90), ("Caderno", 12.50)]
produtos_ordenados = sorted(produtos, key=lambda produto: produto[1])
print(produtos_ordenados)
```

**5.**
```python
vendas = [45.90, 120.00, 15.50, 200.00]
vendas_grandes = list(filter(lambda venda: venda > 50, vendas))
print(vendas_grandes)
```

**6.**
```python
precos = [45.90, 120.00, 15.50]
precos_com_desconto = list(map(lambda preco: preco * 0.90, precos))
print(precos_com_desconto)
```

**7.**
```python
eh_venda_grande = lambda preco: preco > 100
print(eh_venda_grande(150))
print(eh_venda_grande(50))
```

**8.**
```python
quadrado_lambda = lambda numero: numero ** 2

def quadrado_def(numero):
    return numero ** 2

print(quadrado_lambda(4) == quadrado_def(4))
```

**9.**
```python
vendas = [45.90, 120.00, 15.50, 200.00]
vendas_decrescente = sorted(vendas, key=lambda venda: venda, reverse=True)
print(vendas_decrescente)
```

**10.**
```python
vendas = [45.90, 120.00, 15.50, 200.00, 33.00]
vendas_grandes = list(filter(lambda venda: venda > 50, vendas))
comissoes = list(map(lambda venda: round(venda * 0.05, 2), vendas_grandes))
print(comissoes)
```

</details>

## 25. Funções built-in (len, sum, map, filter, etc.)

1. Use `len()` para descobrir quantas vendas existem em uma lista.
2. Use `sum()` e `len()` juntas para calcular o ticket médio de uma lista de vendas.
3. Use `sorted()` para criar uma nova lista de vendas em ordem crescente, sem alterar a original.
4. Use `max()` e `min()` para descobrir a maior e a menor venda de uma lista.
5. Use `round()` para arredondar o ticket médio calculado no exercício 2 para duas casas decimais.
6. Use `map()` com uma lambda para aplicar 8% de imposto sobre cada valor de uma lista de preços.
7. Use `filter()` com uma lambda para selecionar apenas os produtos cujo preço é menor que R$ 20 de uma lista de tuplas `(nome, preco)`.
8. Use `any()` para verificar se existe alguma venda acima de R$ 500 em uma lista.
9. Use `all()` para verificar se todas as vendas de uma lista são maiores que zero.
10. Combine `sum()`, `len()`, `filter()`, `map()` e `round()` em um único bloco para: calcular o ticket médio de uma lista de vendas, filtrar as vendas acima da média, aplicar 5% de comissão sobre elas com `map()` e mostrar o resultado arredondado.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
vendas = [45.90, 120.00, 15.50, 200.00]
print(len(vendas))
```

**2.**
```python
vendas = [45.90, 120.00, 15.50, 200.00]
ticket_medio = sum(vendas) / len(vendas)
print(ticket_medio)
```

**3.**
```python
vendas = [45.90, 120.00, 15.50, 200.00]
vendas_ordenadas = sorted(vendas)
print("Original:", vendas)
print("Ordenada:", vendas_ordenadas)
```

**4.**
```python
vendas = [45.90, 120.00, 15.50, 200.00]
print(max(vendas))
print(min(vendas))
```

**5.**
```python
vendas = [45.90, 120.00, 15.50, 200.00]
ticket_medio = sum(vendas) / len(vendas)
print(round(ticket_medio, 2))
```

**6.**
```python
precos = [45.90, 120.00, 15.50]
precos_com_imposto = list(map(lambda preco: round(preco * 1.08, 2), precos))
print(precos_com_imposto)
```

**7.**
```python
produtos = [("Caneta", 5.90), ("Mochila", 89.90), ("Borracha", 2.50)]
produtos_baratos = list(filter(lambda produto: produto[1] < 20, produtos))
print(produtos_baratos)
```

**8.**
```python
vendas = [45.90, 120.00, 15.50, 550.00]
tem_venda_acima_de_500 = any(venda > 500 for venda in vendas)
print(tem_venda_acima_de_500)
```

**9.**
```python
vendas = [45.90, 120.00, 15.50, 200.00]
todas_positivas = all(venda > 0 for venda in vendas)
print(todas_positivas)
```

**10.**
```python
vendas = [45.90, 120.00, 15.50, 200.00, 33.00, 89.90, 310.00]

ticket_medio = sum(vendas) / len(vendas)
vendas_acima_da_media = list(filter(lambda venda: venda > ticket_medio, vendas))
comissoes = list(map(lambda venda: round(venda * 0.05, 2), vendas_acima_da_media))

print("Ticket médio:", round(ticket_medio, 2))
print("Vendas acima da média:", vendas_acima_da_media)
print("Comissões:", comissoes)
```

</details>
