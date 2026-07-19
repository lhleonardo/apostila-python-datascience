# Definindo funções (def, parâmetros, return)

> Módulo 1 — Fundamentos de Python · Tópico 22 de 25

## O que é e por que importa

Até agora você usou funções prontas do Python, como `print()`, `len()` e `sum()` (formalizadas em `21-funcoes-e-metodos.md`). Chegou a hora de criar as suas próprias. Uma função definida por você é um pedaço de código nomeado e reutilizável — você escreve a lógica uma vez, e depois só "chama" a função sempre que precisar daquele cálculo, sem copiar e colar o código de novo.

Pensa em uma função como uma receita de bolo escrita uma vez: a receita recebe ingredientes (os "parâmetros", os dados de entrada) e produz um bolo (o "retorno", o resultado). Você não reescreve a receita toda vez que quer fazer um bolo — só segue os passos de novo, trocando os ingredientes se quiser.

Em análise de dados, funções evitam repetição e reduzem erro: se você precisa calcular "valor total com desconto" em quinze lugares diferentes do seu código, é melhor escrever essa regra uma vez, em uma função, do que repetir a fórmula quinze vezes (e correr o risco de errar em uma delas, ou esquecer de atualizar todas se a regra mudar).

## Como funciona (com exemplo comentado)

```python
# def define uma função. Os nomes entre parênteses são os "parâmetros" -- 
# os dados que a função espera receber para funcionar
def calcular_total_venda(preco_unitario, quantidade):
    total = preco_unitario * quantidade
    return total  # return devolve o resultado para quem chamou a função

# Chamando a função, passando os "argumentos" (os valores reais para os parâmetros)
total_venda_1 = calcular_total_venda(5.90, 3)
print("Total da venda 1:", total_venda_1)

total_venda_2 = calcular_total_venda(12.50, 2)
print("Total da venda 2:", total_venda_2)

# Uma função pode ter um valor padrão para um parâmetro, usado quando não é informado
def calcular_total_com_desconto(preco_unitario, quantidade, desconto=0):
    total = preco_unitario * quantidade
    total_com_desconto = total * (1 - desconto)
    return total_com_desconto

print(calcular_total_com_desconto(10.00, 2))          # sem desconto, usa o padrão 0
print(calcular_total_com_desconto(10.00, 2, 0.10))     # com 10% de desconto

# Uma função pode ter várias linhas de lógica antes do return, inclusive if/for
def classificar_venda(valor):
    if valor >= 200:
        return "grande"
    elif valor >= 50:
        return "media"
    else:
        return "pequena"

print(classificar_venda(35.00))   # pequena
print(classificar_venda(89.90))   # media

# Uma função sem return explícito devolve None (o "vazio" do Python)
def mostrar_recibo(produto, total):
    print(f"Recibo: {produto} - Total: R$ {total}")
    # sem return aqui -- essa função só imprime, não devolve valor útil

resultado = mostrar_recibo("Caneta Azul", 17.70)
print(resultado)  # None
```

## Erros comuns de quem está começando

- Esquecer o `return`, e depois se surpreender que a função "não funciona" quando na verdade ela só não devolve nada (`None`) para ser usado depois. `print()` dentro da função mostra algo na tela, mas não é o mesmo que devolver um valor com `return`.
- Confundir "parâmetro" (o nome usado dentro da definição da função, como `preco_unitario`) com "argumento" (o valor real passado na hora de chamar, como `5.90`). Na prática os termos são usados de forma intercambiável no dia a dia, mas vale saber a distinção.
- Esquecer que uma variável criada dentro da função (como `total` no primeiro exemplo) só existe dentro dela — tentar usar `total` fora da função gera erro, porque o "escopo" da variável é local à função.

## Exercício prático

Crie uma função chamada `calcular_ticket_medio` que recebe dois parâmetros: `faturamento_total` e `numero_de_vendas`, e devolve o ticket médio (faturamento dividido pelo número de vendas).

1. Defina a função com `def`, usando `return` para devolver o resultado.
2. Chame a função com os dados: faturamento de R$ 850.00 e 10 vendas.
3. Mostre o resultado com `print()`.

**Desafio bônus (opcional):** crie uma função `classificar_ticket_medio` que recebe o ticket médio calculado e devolve `"alto"` se for maior que R$ 100, `"médio"` se estiver entre R$ 50 e R$ 100, e `"baixo"` caso contrário. Use a saída da primeira função como entrada da segunda.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
def calcular_ticket_medio(faturamento_total, numero_de_vendas):
    ticket_medio = faturamento_total / numero_de_vendas
    return ticket_medio

ticket = calcular_ticket_medio(850.00, 10)
print("Ticket médio:", ticket)

# Desafio bônus: uma função usando o resultado da outra
def classificar_ticket_medio(ticket_medio):
    if ticket_medio > 100:
        return "alto"
    elif ticket_medio >= 50:
        return "médio"
    else:
        return "baixo"

classificacao = classificar_ticket_medio(ticket)
print("Classificação do ticket médio:", classificacao)
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar o que são parâmetros e `return` com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Entendo que uma variável criada dentro de uma função não existe fora dela
