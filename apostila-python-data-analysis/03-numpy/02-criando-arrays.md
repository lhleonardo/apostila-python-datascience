# Criando arrays

> Módulo 3 — NumPy · Tópico 2 de 7

## O que é e por que importa

No tópico anterior você criou um array a partir de uma lista já pronta com
`np.array()`. Mas na prática, muitas vezes você precisa **gerar** dados —
sequências de números, arrays cheios de zeros para inicializar algo, valores
igualmente espaçados para um gráfico. NumPy tem funções prontas para cada uma
dessas situações, e usá-las é bem mais rápido (e menos propenso a erro) do
que escrever loops para montar as listas na mão.

Também é comum trabalhar com arrays de mais de uma dimensão — pense numa
planilha, com linhas e colunas: isso é um array **2D** em NumPy. Uma imagem
em preto e branco, uma tabela de vendas por mês e por produto, uma matriz de
distâncias entre cidades: tudo isso é naturalmente representado como array
2D (ou até 3D, 4D...).

## Como funciona (com exemplo comentado)

```python
import numpy as np

# np.arange: como o range() do Python, mas retorna um array
sequencia = np.arange(0, 10)          # [0 1 2 3 4 5 6 7 8 9]
sequencia_pares = np.arange(0, 20, 2) # [0 2 4 6 8 10 12 14 16 18] -- (início, fim, passo)

# np.zeros: array cheio de zeros -- útil para "reservar espaço" antes de preencher
zeros_1d = np.zeros(5)         # [0. 0. 0. 0. 0.]
zeros_2d = np.zeros((3, 4))    # matriz 3 linhas x 4 colunas, tudo zero

# np.ones: mesma ideia, mas cheio de 1
uns = np.ones((2, 3))          # matriz 2x3 cheia de 1.0

# np.full: array cheio de um valor qualquer escolhido por você
cheio = np.full((2, 2), 7)     # matriz 2x2 cheia de 7

# np.linspace: N valores igualmente espaçados entre um início e um fim (inclusive)
# muito usado para gerar eixos de gráficos
espacados = np.linspace(0, 1, 5)  # [0.   0.25 0.5  0.75 1.  ] -- 5 valores entre 0 e 1

# np.random: números aleatórios (veremos mais no contexto de amostragem/simulação)
aleatorios = np.random.rand(3)         # 3 números aleatórios entre 0 e 1
inteiros_aleatorios = np.random.randint(1, 100, size=5)  # 5 inteiros entre 1 e 99

# Criando um array 2D direto de uma lista de listas
matriz = np.array([
    [1, 2, 3],
    [4, 5, 6],
])
print(matriz.shape)  # (2, 3) -- 2 linhas, 3 colunas
print(matriz.ndim)   # 2

# Especificando o dtype explicitamente (útil para controlar memória/precisão)
inteiros = np.array([1, 2, 3], dtype=np.int32)
print(inteiros.dtype)  # int32
```

Repare no padrão do `shape` para arrays 2D: `(linhas, colunas)`. É fácil
confundir a ordem no começo — sempre "linhas primeiro, colunas depois", igual
a como lemos uma tabela (primeiro em qual linha, depois em qual coluna).

## Erros comuns de quem está começando

- Confundir a ordem dos argumentos em `np.arange(inicio, fim, passo)` com
  `np.linspace(inicio, fim, quantidade)` — no `arange` o terceiro argumento é
  o "pulo" entre os números; no `linspace` é **quantos números** você quer no
  total, não o espaçamento entre eles.
- Esquecer que `np.arange` (assim como `range()`) **não inclui** o valor
  final, enquanto `np.linspace` **inclui** por padrão. `np.arange(0, 5)` vai
  até 4; `np.linspace(0, 5, 6)` vai até 5.
- Passar o `shape` de `zeros`/`ones`/`full` sem parênteses quando é mais de
  uma dimensão: `np.zeros(3, 4)` dá erro — o correto é `np.zeros((3, 4))`,
  com o formato como uma única tupla.

## Exercício prático

1. Crie um array com os números pares de 0 a 30 usando `np.arange`.
2. Crie uma matriz 3x3 cheia de zeros usando `np.zeros`.
3. Crie um array com 6 valores igualmente espaçados entre 10 e 20 (incluindo
   os dois extremos) usando `np.linspace`.
4. Para cada array criado, imprima o `shape`.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import numpy as np

pares = np.arange(0, 31, 2)
print(pares)
print(pares.shape)

matriz_zeros = np.zeros((3, 3))
print(matriz_zeros)
print(matriz_zeros.shape)

espacados = np.linspace(10, 20, 6)
print(espacados)
print(espacados.shape)
```

</details>

## Checklist antes de avançar

- [ ] Sei a diferença entre `np.arange` e `np.linspace` (e qual usar em cada caso)
- [ ] Consigo criar arrays 2D e sei ler o `shape` como (linhas, colunas)
- [ ] Sei criar arrays preenchidos com zeros, uns ou um valor fixo
- [ ] Resolvi o exercício sem olhar a solução
