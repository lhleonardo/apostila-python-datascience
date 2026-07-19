# Funções estatísticas e agregações

> Módulo 3 — NumPy · Tópico 5 de 7

## O que é e por que importa

**Agregação** é reduzir um array a um único número (ou a um array menor) que
resume seus dados: a soma, a média, o máximo, o desvio padrão. É uma das
operações mais usadas em análise de dados — quase toda pergunta de negócio
("qual o faturamento total?", "qual o produto mais vendido em média?") vira,
no código, uma chamada de função de agregação.

NumPy traz essas funções prontas e otimizadas, evitando que você reimplemente
soma ou média com loops. E quando os dados são 2D (matriz), você escolhe se
quer agregar a matriz inteira, só as linhas, ou só as colunas — usando o
parâmetro `axis`, que costuma confundir no início mas é simples uma vez que
"clica".

## Como funciona (com exemplo comentado)

```python
import numpy as np

notas = np.array([7.5, 8.0, 6.5, 9.0, 5.5])

print(np.sum(notas))    # 36.5 -- soma de tudo
print(np.mean(notas))   # 7.3 -- média
print(np.min(notas))    # 5.5
print(np.max(notas))    # 9.0
print(np.std(notas))    # ~1.19 -- desvio padrão (dispersão dos dados)
print(np.median(notas)) # 7.5 -- mediana

# Essas funções também existem como MÉTODO do array, forma equivalente e comum:
print(notas.sum())   # 36.5
print(notas.mean())  # 7.3

# argmin/argmax: retornam o ÍNDICE do menor/maior valor, não o valor em si
print(np.argmax(notas))  # 3 -- índice do maior valor (9.0 está na posição 3)
print(np.argmin(notas))  # 4 -- índice do menor valor (5.5 está na posição 4)

# Agregações em matrizes 2D -- aqui entra o parâmetro axis
vendas = np.array([
    [100, 120, 90, 130],   # produto A, vendas em 4 meses
    [200, 210, 195, 220],  # produto B
    [50, 60, 55, 58],      # produto C
])

print(np.sum(vendas))          # 1488 -- soma TUDO, vira um único número
print(np.sum(vendas, axis=0))  # [350 390 340 408] -- soma por COLUNA (soma cada mês, todos produtos)
print(np.sum(vendas, axis=1))  # [440 825 223] -- soma por LINHA (soma cada produto, todos meses)

# Truque para lembrar o axis: axis=0 "colapsa" as linhas (anda na vertical),
# resultando em um valor por coluna. axis=1 "colapsa" as colunas (anda na
# horizontal), resultando em um valor por linha.

print(np.mean(vendas, axis=1))  # [110. 206.25 55.75] -- média de vendas por produto
print(np.max(vendas, axis=0))   # [200 210 195 220] -- maior venda em cada mês
```

## Erros comuns de quem está começando

- Trocar `axis=0` com `axis=1` e obter um resultado com o número errado de
  elementos, sem entender por quê. Se a dúvida bater, teste com uma matriz
  pequena e confira o `shape` do resultado: agregação com `axis=0` numa
  matriz `(3, 4)` retorna algo de shape `(4,)`; com `axis=1`, shape `(3,)`.
- Confundir `np.argmax`/`np.argmin` (que retornam o **índice**) com
  `np.max`/`np.min` (que retornam o **valor**) — usar um no lugar do outro é
  um erro sutil que não quebra o código, só dá resultado errado.
- Esquecer que `np.std` (desvio padrão) e `np.median` (mediana) já existem
  prontas e tentar calcular na mão — vale sempre checar se o NumPy já resolve
  antes de implementar algo do zero.

## Exercício prático

Uma matriz representa notas de 3 alunos (linhas) em 4 provas (colunas):

```python
notas = np.array([
    [7.0, 8.5, 6.0, 9.0],
    [5.5, 6.0, 7.5, 8.0],
    [9.0, 9.5, 8.5, 10.0],
])
```

1. Calcule a média geral de todas as notas (um único número).
2. Calcule a média de cada aluno (média por linha).
3. Calcule a média de cada prova (média por coluna).
4. Descubra o índice do aluno com a maior média (dica: primeiro calcule as
   médias por aluno, depois use `np.argmax` nesse resultado).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import numpy as np

notas = np.array([
    [7.0, 8.5, 6.0, 9.0],
    [5.5, 6.0, 7.5, 8.0],
    [9.0, 9.5, 8.5, 10.0],
])

media_geral = np.mean(notas)
print("Média geral:", media_geral)

media_por_aluno = np.mean(notas, axis=1)
print("Média por aluno:", media_por_aluno)

media_por_prova = np.mean(notas, axis=0)
print("Média por prova:", media_por_prova)

aluno_com_maior_media = np.argmax(media_por_aluno)
print("Índice do aluno com maior média:", aluno_com_maior_media)  # 2
```

</details>

## Checklist antes de avançar

- [ ] Conheço as principais funções de agregação: sum, mean, min, max, std, median
- [ ] Entendo a diferença entre `argmax`/`argmin` e `max`/`min`
- [ ] Sei usar `axis=0` e `axis=1` para agregar por coluna ou por linha em matrizes
- [ ] Resolvi o exercício sem olhar a solução
