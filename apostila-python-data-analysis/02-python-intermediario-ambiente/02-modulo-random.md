# Módulo random

> Módulo 2 — Python Intermediário e Ambiente · Tópico 2 de 11

## O que é e por que importa

O Python vem com uma biblioteca embutida chamada `random`, que gera valores aleatórios: números sorteados, escolhas aleatórias dentro de uma lista, embaralhamento de itens. Um "módulo", nesse contexto, é só um arquivo com funções prontas que você importa e passa a usar — pensa nele como uma "caixa de ferramentas extra" que você abre quando precisa.

Em análise de dados, `random` é extremamente útil para **simular dados** quando você ainda não tem uma base real (ou quer testar seu código antes de plugar dados de verdade), e também para tarefas como sortear uma amostra de clientes para uma pesquisa, embaralhar uma lista antes de dividir em grupos, ou simular cenários ("e se as vendas variassem entre R$ 10 e R$ 500 por dia?").

Vamos usar `random` bastante daqui para frente para gerar bases de dados fictícias da Loja da Ana maiores do que seria prático digitar à mão.

## Como funciona (com exemplo comentado)

```python
import random  # "import" carrega o módulo para você poder usar suas funções

produtos = ["Caneta Azul", "Caderno Capa Dura", "Lapis HB", "Borracha", "Mochila"]

# random.choice escolhe UM item aleatório de uma sequência (lista, tupla etc.)
produto_sorteado = random.choice(produtos)
print("Produto sorteado:", produto_sorteado)

# random.randint(a, b) sorteia um número inteiro entre a e b, incluindo os dois extremos
quantidade_vendida = random.randint(1, 10)
print("Quantidade vendida:", quantidade_vendida)

# random.sample escolhe VÁRIOS itens diferentes, sem repetir nenhum
clientes = ["Ana", "Beto", "Carla", "Diego", "Elisa", "Fabio"]
sorteados_para_pesquisa = random.sample(clientes, 3)
print("Clientes sorteados para a pesquisa:", sorteados_para_pesquisa)

# random.seed "trava" a sequência de sorteios -- útil para que o resultado
# aleatório seja sempre o mesmo quando você roda o código de novo (bom para
# testar e para reproduzir um exemplo em uma aula ou apostila)
random.seed(42)
print(random.randint(1, 100))  # sempre vai dar o mesmo número, pois a seed é fixa
print(random.randint(1, 100))  # o segundo sorteio também é sempre igual, na mesma ordem

# Simulando uma pequena base de vendas da Loja da Ana
random.seed(7)
vendas_simuladas = []
for _ in range(5):
    venda = {
        "produto": random.choice(produtos),
        "quantidade": random.randint(1, 5),
        "preco_unitario": round(random.uniform(2.0, 50.0), 2),  # uniform sorteia um decimal
    }
    vendas_simuladas.append(venda)

for venda in vendas_simuladas:
    print(venda)
```

## Erros comuns de quem está começando

- Confundir `random.choice` (escolhe um item, pode repetir se você chamar de novo) com `random.sample` (escolhe vários itens diferentes de uma vez, sem repetição entre eles).
- Esquecer que `random.randint(a, b)` inclui o `b` no sorteio (diferente de outras funções em Python que costumam excluir o último valor, como o `range`).
- Achar que `random.seed()` faz o número "parar de ser aleatório" para sempre. Na verdade, ela só garante que, a partir daquele ponto, a sequência de sorteios será sempre a mesma — se você mudar a seed ou tirar a linha, os valores voltam a variar a cada execução.

## Exercício prático

Usando `random.seed(10)` no início do script (para o resultado ser sempre igual), simule 8 vendas da Loja da Ana. Cada venda deve ser um dicionário com `"produto"` (sorteado de uma lista com pelo menos 4 produtos que você escolher) e `"quantidade"` (um inteiro entre 1 e 6). Guarde tudo em uma lista chamada `vendas` e imprima cada venda com um `for`.

**Desafio bônus (opcional):** depois de gerar a lista `vendas`, use `random.sample` para sortear 2 vendas dessa lista como se fossem selecionadas para uma "auditoria" e imprima só essas duas.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import random

random.seed(10)

produtos = ["Caneta Azul", "Caderno Capa Dura", "Lapis HB", "Mochila"]

vendas = []
for _ in range(8):
    venda = {
        "produto": random.choice(produtos),
        "quantidade": random.randint(1, 6),
    }
    vendas.append(venda)

for venda in vendas:
    print(venda)

# Desafio bônus
auditadas = random.sample(vendas, 2)
print("Vendas selecionadas para auditoria:")
for venda in auditadas:
    print(venda)
```

</details>

## Checklist antes de avançar

- [ ] Consigo explicar com minhas próprias palavras a diferença entre `choice` e `sample`
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Entendo para que serve `random.seed`
