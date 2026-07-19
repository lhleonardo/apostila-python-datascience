# Operadores aritméticos

> Módulo 1 — Fundamentos de Python · Tópico 8 de 25

## O que é e por que importa

Operadores aritméticos são os símbolos que fazem contas: `+` (soma), `-` (subtração), `*` (multiplicação), `/` (divisão), `//` (divisão inteira), `%` (resto da divisão) e `**` (potência). Se você já usou fórmulas no Excel, é exatamente a mesma ideia, só que escrita direto no código em vez de dentro de uma célula.

Em análise de dados, esses operadores são o motor de praticamente todo cálculo que você vai fazer: somar vendas, calcular o total de uma compra (preço vezes quantidade), achar a média (soma dividida pela quantidade de itens), calcular crescimento percentual. Você já usou alguns deles nos tópicos anteriores sem nomeá-los formalmente — agora vamos consolidar todos.

Dois operadores merecem atenção especial por serem menos intuitivos: `//` (divisão inteira, que descarta a parte decimal) e `%` (o resto que sobra de uma divisão). Eles parecem estranhos no começo, mas são extremamente úteis para tarefas como "descobrir se um número é par" ou "dividir um total em grupos iguais e saber quanto sobra".

## Como funciona (com exemplo comentado)

```python
faturamento_semana = 1250.00
dias_da_semana = 7

# Soma, subtração e multiplicação são diretas
meta_semanal = 1000.00
diferenca_para_meta = faturamento_semana - meta_semanal
print("Quanto passou da meta:", diferenca_para_meta)

# Divisão normal (/) sempre retorna float, mesmo dividindo dois inteiros
media_diaria = faturamento_semana / dias_da_semana
print("Média diária:", round(media_diaria, 2))

# Divisão inteira (//) descarta a parte decimal do resultado
qtd_vendida = 50
tamanho_da_caixa = 8
caixas_completas = qtd_vendida // tamanho_da_caixa
print("Caixas completas:", caixas_completas)  # 6

# % (resto/módulo) mostra o que sobra depois da divisão inteira
itens_avulsos = qtd_vendida % tamanho_da_caixa
print("Itens que sobraram fora de caixa:", itens_avulsos)  # 2

# ** eleva a um expoente -- útil para juros compostos, crescimento etc.
crescimento_anual = 1.10  # 10% de crescimento ao ano
faturamento_projetado_2_anos = faturamento_semana * (crescimento_anual ** 2)
print("Faturamento projetado em 2 anos:", round(faturamento_projetado_2_anos, 2))

# % também é o truque clássico para saber se um número é par
numero_de_vendas = 15
if numero_de_vendas % 2 == 0:
    print("Número par de vendas")
else:
    print("Número ímpar de vendas")
```

## Erros comuns de quem está começando

- Confundir `/` com `//`. `/` sempre dá o resultado "certo" com decimais; `//` corta a parte decimal, mesmo quando isso não faz sentido para o problema.
- Esquecer a ordem das operações (precedência): multiplicação e divisão são calculadas antes de soma e subtração, igual na matemática da escola. Use parênteses `()` para deixar claro, mesmo quando não é obrigatório — ajuda a evitar erro de leitura.
- Achar que `%` é "porcentagem". Em Python, `%` dentro de uma expressão numérica é o operador de resto da divisão, não tem relação direta com porcentagem (para porcentagem, você multiplica por `0.10`, por exemplo, como no exemplo acima).

## Exercício prático

A Loja da Ana tem 37 unidades de um produto em estoque e quer organizá-las em caixas de 5 unidades cada, para transporte.

1. Calcule quantas caixas completas dá para montar.
2. Calcule quantas unidades sobram, fora de caixa.
3. Mostre os dois resultados com `print()`.

**Desafio bônus (opcional):** o faturamento da loja neste mês foi R$ 8400.00 e o objetivo é crescer 15% ao mês. Calcule qual seria o faturamento projetado daqui a 3 meses, usando o operador `**`.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
estoque_total = 37
tamanho_caixa = 5

# Divisão inteira dá o número de caixas completas
caixas_completas = estoque_total // tamanho_caixa
print("Caixas completas:", caixas_completas)

# O resto (%) dá o que sobra fora de caixa
unidades_avulsas = estoque_total % tamanho_caixa
print("Unidades avulsas:", unidades_avulsas)

# Desafio bônus: projeção de crescimento composto
faturamento_atual = 8400.00
crescimento_mensal = 1.15  # 15% de crescimento

faturamento_projetado = faturamento_atual * (crescimento_mensal ** 3)
print("Faturamento projetado em 3 meses:", round(faturamento_projetado, 2))
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar a diferença entre `/`, `//` e `%` com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Sei usar `**` para elevar um número a uma potência
