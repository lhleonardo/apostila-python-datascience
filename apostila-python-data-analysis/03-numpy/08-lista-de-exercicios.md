# Lista de exercícios — Módulo 3

> Módulo 3 — NumPy · Lista de exercícios de revisão

Esta lista reúne 10 exercícios práticos para cada tópico do módulo, para
consolidar o que foi aprendido antes de avançar. Tente resolver cada
exercício sem consultar o tópico original primeiro — as soluções vêm logo
depois de cada bloco, dentro de um "clique para ver".

## 1. Introdução ao NumPy

1. Crie a lista Python `[3, 6, 9, 12]` e converta-a para um array NumPy chamado `numeros`.
2. Imprima o `type()` do array `numeros` para confirmar que é um `ndarray`.
3. Imprima o `dtype` de `numeros`.
4. Crie um array a partir da lista mista `[1, 2, 3.5, 4]` e imprima seu `dtype`, explicando (no comentário) por que o resultado é esse tipo.
5. Dado o array `precos = np.array([9.9, 19.9, 29.9])`, multiplique todos os valores por `1.20` (aumento de 20%) sem usar loop.
6. Compare o resultado de `[1, 2, 3] * 3` (lista Python) com `np.array([1, 2, 3]) * 3` (array NumPy) e imprima os dois, comentando a diferença.
7. Crie o array `salarios = np.array([2500, 3200, 4100, 2800])` e imprima seu `shape` e `ndim`.
8. Aplique um desconto de 5% a todos os elementos de `salarios` numa única operação vetorizada e imprima o resultado.
9. Crie um array com as notas `[10, 7, 8, 9, 6]` e some `1` ponto a todas as notas de uma vez, sem loop.
10. Explique com código (usando `.shape` e `.dtype`) por que `np.array([True, False, True])` tem `dtype` `bool`, e some esse array com `np.sum()` para mostrar quantos `True` existem.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import numpy as np

numeros_lista = [3, 6, 9, 12]
numeros = np.array(numeros_lista)
print(numeros)
```

**2.**
```python
print(type(numeros))  # <class 'numpy.ndarray'>
```

**3.**
```python
print(numeros.dtype)  # int64 (ou int32, dependendo do sistema)
```

**4.**
```python
misto = np.array([1, 2, 3.5, 4])
print(misto.dtype)  # float64 -- como há um float na lista, todos os valores viram float
```

**5.**
```python
precos = np.array([9.9, 19.9, 29.9])
novos_precos = precos * 1.20
print(novos_precos)
```

**6.**
```python
lista_triplicada = [1, 2, 3] * 3
array_triplicado = np.array([1, 2, 3]) * 3
print(lista_triplicada)   # [1, 2, 3, 1, 2, 3, 1, 2, 3] -- repete a lista 3 vezes
print(array_triplicado)   # [3 6 9] -- multiplica cada elemento por 3
```

**7.**
```python
salarios = np.array([2500, 3200, 4100, 2800])
print(salarios.shape)  # (4,)
print(salarios.ndim)   # 1
```

**8.**
```python
salarios_com_desconto = salarios * 0.95
print(salarios_com_desconto)
```

**9.**
```python
notas = np.array([10, 7, 8, 9, 6])
notas_novas = notas + 1
print(notas_novas)
```

**10.**
```python
booleanos = np.array([True, False, True])
print(booleanos.shape)  # (3,)
print(booleanos.dtype)  # bool
print(np.sum(booleanos))  # 2 -- True conta como 1, False como 0
```

</details>

## 2. Criando arrays

1. Crie um array com os números de 1 a 10 (inclusive) usando `np.arange`.
2. Crie um array com os múltiplos de 5 de 0 a 50 usando `np.arange`.
3. Crie um array 1D de 6 zeros usando `np.zeros`.
4. Crie uma matriz 4x2 cheia de zeros usando `np.zeros`.
5. Crie uma matriz 3x3 cheia de uns usando `np.ones`.
6. Crie uma matriz 2x4 cheia do valor `9` usando `np.full`.
7. Crie um array com 4 valores igualmente espaçados entre 0 e 100 (incluindo os extremos) usando `np.linspace`.
8. Crie um array 1D com 10 números inteiros aleatórios entre 1 e 6 (simulando lançamentos de um dado) usando `np.random.randint`.
9. Crie uma matriz 2D a partir da lista de listas `[[1, 1], [2, 4], [3, 9]]` e imprima seu `shape` e `ndim`.
10. Crie um array com os números de 1 a 5 especificando explicitamente `dtype=np.float64`, e imprima o `dtype` para confirmar.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import numpy as np

numeros = np.arange(1, 11)
print(numeros)
```

**2.**
```python
multiplos_de_5 = np.arange(0, 51, 5)
print(multiplos_de_5)
```

**3.**
```python
zeros_1d = np.zeros(6)
print(zeros_1d)
```

**4.**
```python
zeros_4x2 = np.zeros((4, 2))
print(zeros_4x2)
```

**5.**
```python
uns_3x3 = np.ones((3, 3))
print(uns_3x3)
```

**6.**
```python
cheio_de_9 = np.full((2, 4), 9)
print(cheio_de_9)
```

**7.**
```python
espacados = np.linspace(0, 100, 4)
print(espacados)  # [  0.  33.33333333  66.66666667 100.]
```

**8.**
```python
dado = np.random.randint(1, 7, size=10)
print(dado)
```

**9.**
```python
matriz = np.array([[1, 1], [2, 4], [3, 9]])
print(matriz.shape)  # (3, 2)
print(matriz.ndim)   # 2
```

**10.**
```python
numeros_float = np.array([1, 2, 3, 4, 5], dtype=np.float64)
print(numeros_float.dtype)  # float64
```

</details>

## 3. Indexação e slicing

1. Dado `alturas = np.array([1.65, 1.80, 1.72, 1.58, 1.90])`, imprima o primeiro e o último elemento.
2. Imprima os elementos do índice 1 ao 3 (exclusivo) de `alturas`.
3. Dada `notas_turma = np.array([[8, 7, 9], [6, 5, 7], [9, 10, 8], [7, 6, 6]])`, imprima o elemento da linha 2, coluna 1.
4. Imprima a linha 0 inteira de `notas_turma`.
5. Imprima a coluna 2 inteira de `notas_turma`.
6. Imprima a submatriz formada pelas linhas 1 e 2 e pelas colunas 0 e 1 de `notas_turma`.
7. Pegue uma fatia (`view`, sem `.copy()`) das duas primeiras notas de `alturas`, altere o primeiro valor da fatia para `2.0`, e imprima `alturas` para confirmar que o array original também mudou.
8. Repita o exercício anterior, mas usando `.copy()` na fatia, e confirme que dessa vez `alturas` não é afetado.
9. Dada `matriz = np.arange(1, 17).reshape(4, 4)` (pode usar diretamente, mesmo sem ainda ter visto reshape em detalhe — é só para montar a matriz do exercício), imprima a diagonal usando índices individuais `matriz[0,0]`, `matriz[1,1]`, `matriz[2,2]`, `matriz[3,3]`.
10. Da mesma `matriz` do exercício 9, imprima a última linha e a última coluna usando índices negativos.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import numpy as np

alturas = np.array([1.65, 1.80, 1.72, 1.58, 1.90])
print(alturas[0])   # 1.65
print(alturas[-1])  # 1.9
```

**2.**
```python
print(alturas[1:3])  # [1.8  1.72]
```

**3.**
```python
notas_turma = np.array([[8, 7, 9], [6, 5, 7], [9, 10, 8], [7, 6, 6]])
print(notas_turma[2, 1])  # 10
```

**4.**
```python
print(notas_turma[0])  # [8 7 9]
```

**5.**
```python
print(notas_turma[:, 2])  # [9 7 8 6]
```

**6.**
```python
print(notas_turma[1:3, 0:2])  # [[6 5] [9 10]]
```

**7.**
```python
fatia = alturas[0:2]
fatia[0] = 2.0
print(alturas)  # [2.   1.8  1.72 1.58 1.9 ] -- original foi afetado
```

**8.**
```python
alturas = np.array([1.65, 1.80, 1.72, 1.58, 1.90])  # recriando para o exemplo
fatia_segura = alturas[0:2].copy()
fatia_segura[0] = 2.0
print(alturas)  # [1.65 1.8  1.72 1.58 1.9 ] -- original não foi afetado
```

**9.**
```python
matriz = np.arange(1, 17).reshape(4, 4)
print(matriz[0, 0], matriz[1, 1], matriz[2, 2], matriz[3, 3])  # 1 6 11 16
```

**10.**
```python
print(matriz[-1])     # [13 14 15 16] -- última linha
print(matriz[:, -1])  # [4 8 12 16] -- última coluna
```

</details>

## 4. Operações vetorizadas e broadcasting

1. Dado `temperaturas = np.array([20.0, 22.5, 19.0, 25.0])`, some `3` graus a todas as temperaturas numa operação vetorizada.
2. Dado `distancias_km = np.array([5, 12, 3, 20])`, converta todos os valores para metros (multiplique por `1000`).
3. Dados `horas_trabalhadas = np.array([8, 6, 7.5, 9])` e `valor_hora = np.array([25, 30, 28, 22])`, calcule o total ganho em cada dia (multiplicação elemento a elemento).
4. Use `np.sqrt` para calcular a raiz quadrada de cada elemento de `np.array([1, 4, 9, 16, 25])`.
5. Use `np.round` para arredondar os valores de `np.array([3.14159, 2.71828, 1.41421])` para 2 casas decimais (dica: `np.round` aceita um segundo argumento).
6. Dada a matriz `estoque = np.array([[10, 20], [30, 40], [50, 60]])` (3 produtos, 2 lojas) e o array `fator_loja = np.array([1.1, 0.9])`, aplique o fator a cada loja usando broadcasting e imprima o resultado.
7. Dado `precos = np.array([12.0, 45.0, 8.0, 100.0])`, crie um array booleano indicando quais preços são maiores que `20.0`.
8. Dados `vendas_janeiro = np.array([100, 200, 150])` e `vendas_fevereiro = np.array([120, 180, 160])`, calcule a diferença (fevereiro menos janeiro) elemento a elemento.
9. Tente somar um array de shape `(3,)` com um array de shape `(2,)` e explique (em comentário) por que dá erro, sem realmente rodar a soma incompatível — em vez disso, imprima os dois `.shape` para mostrar por que não são compatíveis.
10. Dada a matriz `notas_por_disciplina = np.array([[7, 8], [6, 9], [5, 7], [10, 8]])` (4 alunos, 2 disciplinas) e os pesos `pesos = np.array([0.4, 0.6])`, calcule a nota ponderada de cada disciplina multiplicando a matriz pelos pesos usando broadcasting.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import numpy as np

temperaturas = np.array([20.0, 22.5, 19.0, 25.0])
print(temperaturas + 3)
```

**2.**
```python
distancias_km = np.array([5, 12, 3, 20])
distancias_m = distancias_km * 1000
print(distancias_m)
```

**3.**
```python
horas_trabalhadas = np.array([8, 6, 7.5, 9])
valor_hora = np.array([25, 30, 28, 22])
total_dia = horas_trabalhadas * valor_hora
print(total_dia)
```

**4.**
```python
print(np.sqrt(np.array([1, 4, 9, 16, 25])))  # [1. 2. 3. 4. 5.]
```

**5.**
```python
print(np.round(np.array([3.14159, 2.71828, 1.41421]), 2))  # [3.14 2.72 1.41]
```

**6.**
```python
estoque = np.array([[10, 20], [30, 40], [50, 60]])
fator_loja = np.array([1.1, 0.9])
print(estoque * fator_loja)
```

**7.**
```python
precos = np.array([12.0, 45.0, 8.0, 100.0])
maiores_que_20 = precos > 20.0
print(maiores_que_20)  # [False  True False  True]
```

**8.**
```python
vendas_janeiro = np.array([100, 200, 150])
vendas_fevereiro = np.array([120, 180, 160])
diferenca = vendas_fevereiro - vendas_janeiro
print(diferenca)  # [20 -20 10]
```

**9.**
```python
a = np.zeros(3)
b = np.zeros(2)
print(a.shape, b.shape)  # (3,) (2,)
# a + b daria ValueError: shapes (3,) e (2,) não são compatíveis --
# nenhuma das dimensões é igual, nem uma delas é 1
```

**10.**
```python
notas_por_disciplina = np.array([[7, 8], [6, 9], [5, 7], [10, 8]])
pesos = np.array([0.4, 0.6])
notas_ponderadas = notas_por_disciplina * pesos
print(notas_ponderadas)
```

</details>

## 5. Funções estatísticas e agregações

1. Dado `idades = np.array([23, 45, 31, 29, 52, 38])`, calcule a média, o mínimo e o máximo.
2. Calcule o desvio padrão e a mediana de `idades`.
3. Descubra o índice da menor idade e o índice da maior idade usando `argmin`/`argmax`.
4. Dado `gastos = np.array([120.50, 89.90, 340.00, 15.75, 200.00])`, calcule o total gasto usando `np.sum` e usando o método `.sum()`, confirmando que dão o mesmo resultado.
5. Dada a matriz `vendas = np.array([[80, 90, 100], [60, 70, 65], [120, 110, 130]])` (3 vendedores, 3 meses), calcule a soma total de todas as vendas.
6. Calcule a soma de vendas por mês (por coluna, `axis=0`) da matriz `vendas`.
7. Calcule a média de vendas por vendedor (por linha, `axis=1`) da matriz `vendas`.
8. Descubra qual vendedor teve a maior média de vendas, usando `argmax` sobre o resultado do exercício anterior.
9. Descubra o mês com a maior venda total (dica: use `np.sum(vendas, axis=0)` e depois `argmax`).
10. Dado `precos_produtos = np.array([15.0, 220.0, 8.5, 99.9, 45.0])`, calcule quanto o preço máximo é maior que o preço mínimo (amplitude), usando `np.max` e `np.min`.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import numpy as np

idades = np.array([23, 45, 31, 29, 52, 38])
print(np.mean(idades))  # 36.333...
print(np.min(idades))   # 23
print(np.max(idades))   # 52
```

**2.**
```python
print(np.std(idades))     # desvio padrão
print(np.median(idades))  # 34.5
```

**3.**
```python
print(np.argmin(idades))  # 0 -- índice da idade 23
print(np.argmax(idades))  # 4 -- índice da idade 52
```

**4.**
```python
gastos = np.array([120.50, 89.90, 340.00, 15.75, 200.00])
print(np.sum(gastos))  # 766.15
print(gastos.sum())    # 766.15
```

**5.**
```python
vendas = np.array([[80, 90, 100], [60, 70, 65], [120, 110, 130]])
print(np.sum(vendas))  # 825
```

**6.**
```python
print(np.sum(vendas, axis=0))  # [260 270 295] -- soma por mês
```

**7.**
```python
media_por_vendedor = np.mean(vendas, axis=1)
print(media_por_vendedor)  # [90. 65. 120.]
```

**8.**
```python
print(np.argmax(media_por_vendedor))  # 2 -- terceiro vendedor
```

**9.**
```python
soma_por_mes = np.sum(vendas, axis=0)
print(np.argmax(soma_por_mes))  # 2 -- terceiro mês
```

**10.**
```python
precos_produtos = np.array([15.0, 220.0, 8.5, 99.9, 45.0])
amplitude = np.max(precos_produtos) - np.min(precos_produtos)
print(amplitude)  # 211.5
```

</details>

## 6. Reshape e dimensões

1. Crie um array 1D com os números de 1 a 12 usando `np.arange` e imprima seu `shape`.
2. Transforme esse array em uma matriz 3x4 usando `.reshape()`.
3. Transforme o mesmo array 1D em uma matriz 2x6 usando `.reshape()`.
4. Tente descobrir (sem rodar o reshape errado) se é possível transformar o array de 12 elementos em uma matriz 5x3, explicando por que sim ou por que não em um comentário.
5. Use `.reshape(6, -1)` no array de 12 elementos e imprima o `shape` resultante, para confirmar que o NumPy calculou a segunda dimensão automaticamente.
6. Transponha a matriz `matriz = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])` usando `.T` e imprima o `shape` antes e depois.
7. Dada `matriz_3x3 = np.arange(9).reshape(3, 3)`, use `.flatten()` para transformá-la de volta em um array 1D e imprima o resultado.
8. Crie uma view com `.reshape()` de um array de 6 elementos, altere um valor da view, e confirme que o array original também foi alterado.
9. Repita o exercício anterior, mas usando `.reshape(...).copy()`, e confirme que dessa vez o array original não é afetado.
10. Dada a matriz `dados = np.arange(1, 25).reshape(4, 6)`, calcule quantos elementos ela tem com `.size` e confirme que bate com `4 * 6`; depois, transforme-a em uma matriz `2x12` usando `.reshape()`.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import numpy as np

numeros = np.arange(1, 13)
print(numeros.shape)  # (12,)
```

**2.**
```python
matriz_3x4 = numeros.reshape(3, 4)
print(matriz_3x4)
```

**3.**
```python
matriz_2x6 = numeros.reshape(2, 6)
print(matriz_2x6)
```

**4.**
```python
# 5 * 3 = 15, mas o array tem 12 elementos -- 15 != 12, então NÃO é possível
# fazer reshape(5, 3); o total de elementos precisa bater exatamente.
```

**5.**
```python
auto = numeros.reshape(6, -1)
print(auto.shape)  # (6, 2)
```

**6.**
```python
matriz = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])
print(matriz.shape)    # (2, 4)
print(matriz.T.shape)  # (4, 2)
```

**7.**
```python
matriz_3x3 = np.arange(9).reshape(3, 3)
de_volta = matriz_3x3.flatten()
print(de_volta)  # [0 1 2 3 4 5 6 7 8]
```

**8.**
```python
original = np.arange(6)
vista = original.reshape(2, 3)
vista[0, 0] = 999
print(original)  # [999 1 2 3 4 5] -- original foi afetado
```

**9.**
```python
original = np.arange(6)
copia = original.reshape(2, 3).copy()
copia[0, 0] = 999
print(original)  # [0 1 2 3 4 5] -- original não foi afetado
```

**10.**
```python
dados = np.arange(1, 25).reshape(4, 6)
print(dados.size)  # 24 -- bate com 4 * 6
matriz_2x12 = dados.reshape(2, 12)
print(matriz_2x12)
```

</details>

## 7. Boolean masking e filtragem

1. Dado `salarios = np.array([1800, 3200, 5400, 2100, 4700, 2900])`, crie uma máscara booleana para os salários maiores que `3000`.
2. Use a máscara do exercício anterior para obter um array só com os salários maiores que `3000`.
3. Filtre diretamente (sem guardar a máscara em variável) os salários menores ou iguais a `2500`.
4. Dado `idades = np.array([16, 22, 45, 17, 30, 15, 19])`, filtre as idades que representam maiores de idade (`>= 18`) e as menores de idade, em duas linhas separadas.
5. Combine condições para filtrar, em `salarios`, os valores entre `2000` e `5000` (inclusive nas duas pontas), usando `&` com parênteses.
6. Combine condições com `|` para filtrar, em `salarios`, os valores menores que `2000` ou maiores que `5000`.
7. Use `np.where` para descobrir os índices de `salarios` onde o valor é maior que `3000`.
8. Use `np.where` como "if/else vetorizado" para classificar cada valor de `salarios` como `"alto"` (>= 3000) ou `"baixo"` (< 3000).
9. Conte quantos salários em `salarios` são maiores que `3000` usando `np.sum()` sobre a máscara booleana.
10. Dada a matriz `notas = np.array([[5, 8, 9], [4, 6, 7], [9, 9, 3]])`, filtre e imprima todos os valores menores que `6` (o resultado vira um array 1D); depois, faça uma cópia da matriz e substitua todos os valores menores que `6` por `6` diretamente pela máscara.

<details>
<summary>Clique para ver as soluções</summary>

**1.**
```python
import numpy as np

salarios = np.array([1800, 3200, 5400, 2100, 4700, 2900])
mascara_altos = salarios > 3000
print(mascara_altos)
```

**2.**
```python
salarios_altos = salarios[mascara_altos]
print(salarios_altos)  # [3200 5400 4700]
```

**3.**
```python
print(salarios[salarios <= 2500])  # [1800 2100]
```

**4.**
```python
idades = np.array([16, 22, 45, 17, 30, 15, 19])
maiores_de_idade = idades[idades >= 18]
menores_de_idade = idades[idades < 18]
print(maiores_de_idade)  # [22 45 30 19]
print(menores_de_idade)  # [16 17 15]
```

**5.**
```python
entre_2000_e_5000 = salarios[(salarios >= 2000) & (salarios <= 5000)]
print(entre_2000_e_5000)  # [3200 2100 4700 2900]
```

**6.**
```python
fora_da_faixa = salarios[(salarios < 2000) | (salarios > 5000)]
print(fora_da_faixa)  # [1800 5400]
```

**7.**
```python
indices_altos = np.where(salarios > 3000)
print(indices_altos)  # (array([2, 4]),)
```

**8.**
```python
classificacao = np.where(salarios >= 3000, "alto", "baixo")
print(classificacao)
```

**9.**
```python
quantidade_altos = np.sum(salarios > 3000)
print(quantidade_altos)  # 3
```

**10.**
```python
notas = np.array([[5, 8, 9], [4, 6, 7], [9, 9, 3]])
print(notas[notas < 6])  # [5 4 3]

notas_ajustadas = notas.copy()
notas_ajustadas[notas_ajustadas < 6] = 6
print(notas_ajustadas)
```

</details>
