# Conversão de tipos (type casting)

> Módulo 1 — Fundamentos de Python · Tópico 7 de 25

## O que é e por que importa

Conversão de tipos (em inglês, "type casting") é o processo de transformar um valor de um tipo em outro — por exemplo, transformar o texto `"25"` no número `25`. Pense nisso como converter uma medida: 1 metro e 25 centímetros escrito por extenso vira o número 1.25 quando você precisa fazer conta com ele.

Isso importa demais em análise de dados porque, na vida real, dados quase nunca chegam já no tipo certo. Um formulário preenchido por um cliente pode salvar a idade como texto (`"32"`), uma planilha pode exportar preços como texto (`"19.90"`), e você precisa converter esses valores para número antes de somar, comparar ou calcular qualquer coisa.

Em Python, você já viu os tipos `int` (`04-inteiros.md`), `float` (`05-floats.md`) e `bool` (`06-booleanos.md`), além de `str` (texto). As funções `int()`, `float()`, `str()` e `bool()` fazem a conversão entre eles. Sem esse passo, tentar somar um número com um texto trava o programa com um erro.

## Como funciona (com exemplo comentado)

```python
# Simulando um dado que "chegou" como texto (ex: de um formulário preenchido)
quantidade_texto = "10"
preco_texto = "5.50"

# Tentar somar direto daria erro, porque são strings, não números.
# Por isso convertemos primeiro:
quantidade = int(quantidade_texto)   # texto -> inteiro
preco = float(preco_texto)           # texto -> float

total = quantidade * preco
print("Total da venda:", total)  # 55.0

# O caminho inverso também é comum: transformar número em texto para montar uma mensagem
mensagem = "O total foi de R$ " + str(total)
print(mensagem)

# int() também "trunca" (corta) a parte decimal de um float, sem arredondar
avaliacao_media = 4.8
avaliacao_inteira = int(avaliacao_media)
print(avaliacao_inteira)  # 4, não 5 -- int() corta, não arredonda

# bool() converte outros tipos considerando "vazio/zero" como False
print(bool(0))       # False
print(bool(150))     # True
print(bool(""))      # False (texto vazio)
print(bool("Ana"))   # True (texto não vazio)
```

## Erros comuns de quem está começando

- Tentar fazer conta direto com números que na verdade são texto (ex: `"10" + "5"` resulta em `"105"`, concatenação de texto, não soma). É preciso converter com `int()` ou `float()` antes.
- Usar `int()` em um texto que não é um número puro, como `int("10 unidades")` — isso gera erro. `int()` só converte textos que sejam exatamente um número.
- Achar que `int()` arredonda floats. Na verdade ele trunca (corta a casa decimal), então `int(4.9)` vira `4`, não `5`. Para arredondar de verdade, use `round()`.

## Exercício prático

Imagine que a Loja da Ana recebeu os seguintes dados de uma venda, digitados por um sistema que salva tudo como texto:

```python
quantidade_texto = "4"
preco_unitario_texto = "7.25"
```

1. Converta as duas variáveis para os tipos numéricos corretos.
2. Calcule o valor total da venda.
3. Monte e mostre uma mensagem de texto, tipo: `"Total da venda: R$ 29.0"`, usando `str()` para juntar texto com número.

**Desafio bônus (opcional):** o sistema também informou `"em_promocao_texto = "1""` (1 significa sim, 0 significa não). Converta esse valor para `bool` usando o que você aprendeu, e mostre se a venda foi de um produto em promoção. Dica: primeiro converta para `int`, depois para `bool`.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
# Dados "brutos" recebidos como texto
quantidade_texto = "4"
preco_unitario_texto = "7.25"

# Convertendo para os tipos certos antes de fazer conta
quantidade = int(quantidade_texto)
preco_unitario = float(preco_unitario_texto)

total = quantidade * preco_unitario
print("Total da venda: R$", total)

# Montando mensagem juntando texto com número (precisa converter o número para str)
mensagem = "Total da venda: R$ " + str(total)
print(mensagem)

# Desafio bônus
em_promocao_texto = "1"
em_promocao = bool(int(em_promocao_texto))  # "1" -> 1 -> True
print("Produto em promoção?", em_promocao)
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar o que é conversão de tipos com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Entendo a diferença entre `int()` truncar e `round()` arredondar
