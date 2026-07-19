# Reshape e dimensões

> Módulo 3 — NumPy · Tópico 6 de 7

## O que é e por que importa

Às vezes os dados chegam num formato (shape) diferente do que você precisa
para trabalhar: uma lista "achatada" de 12 números que na verdade representa
uma tabela de 3 linhas por 4 colunas, ou uma matriz que você precisa
transpor (trocar linhas por colunas) para combinar com outra. **Reshape** é a
operação de reorganizar os mesmos dados em um novo formato, sem alterar os
valores nem precisar recriá-los.

Isso é puramente sobre **organização** dos dados na memória — nenhum número é
criado ou perdido, só a "forma" como eles são agrupados muda.

## Como funciona (com exemplo comentado)

```python
import numpy as np

# Um array "achatado" (1D) com 12 elementos
dados = np.arange(12)
print(dados)        # [ 0  1  2  3  4  5  6  7  8  9 10 11]
print(dados.shape)  # (12,)

# reshape reorganiza os mesmos 12 valores em outro formato
matriz_3x4 = dados.reshape(3, 4)
print(matriz_3x4)
# [[ 0  1  2  3]
#  [ 4  5  6  7]
#  [ 8  9 10 11]]

matriz_4x3 = dados.reshape(4, 3)
print(matriz_4x3)
# [[ 0  1  2]
#  [ 3  4  5]
#  [ 6  7  8]
#  [ 9 10 11]]

# O total de elementos precisa "fechar a conta": 3*4 = 12, 4*3 = 12, ok.
# dados.reshape(3, 5)  # ERRO: 3*5 = 15, não bate com os 12 elementos originais

# Truque útil: usar -1 em uma das dimensões para o NumPy calcular automaticamente
auto = dados.reshape(3, -1)  # "3 linhas, quantas colunas precisar" -> vira (3, 4)
print(auto.shape)  # (3, 4)

# flatten / ravel: o caminho inverso, transforma um array de várias dimensões em 1D
de_volta = matriz_3x4.flatten()
print(de_volta)  # [ 0  1  2  3  4  5  6  7  8  9 10 11]

# .T (transposta): troca linhas por colunas
matriz = np.array([
    [1, 2, 3],
    [4, 5, 6],
])
print(matriz.shape)    # (2, 3)
print(matriz.T)
# [[1 4]
#  [2 5]
#  [3 6]]
print(matriz.T.shape)  # (3, 2)

# Assim como slicing, reshape geralmente retorna uma VIEW (referência aos
# mesmos dados), não uma cópia -- alterar o resultado pode afetar o original
vista = dados.reshape(3, 4)
vista[0, 0] = 999
print(dados[0])  # 999 -- o array original também mudou
```

## Erros comuns de quem está começando

- Tentar dar reshape para um formato cujo total de elementos não bate com o
  original (`3*4 ≠ 3*5`), gerando `ValueError`. Antes de chamar `.reshape()`,
  vale conferir: `linhas * colunas` precisa ser igual ao número de elementos
  do array original (`.size`).
- Confundir `reshape` (reorganiza os dados existentes) com criar um array
  novo do zero com `np.zeros`/`np.array` — reshape não adiciona nem remove
  dados, só rearranja o que já existe.
- Esquecer que reshape (como slicing) costuma retornar uma view, e se
  surpreender quando alterar o array "remodelado" afeta o original. Use
  `.copy()` quando precisar de independência total, igual visto no Tópico 3.

## Exercício prático

1. Crie um array 1D com os números de 1 a 20 usando `np.arange`.
2. Transforme esse array em uma matriz 4x5 usando `.reshape()`.
3. Transponha essa matriz (deve virar 5x4) e imprima o resultado.
4. Volte a matriz original (4x5) para o formato 1D usando `.flatten()` e
   confirme que os valores estão na ordem original (1 a 20).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import numpy as np

numeros = np.arange(1, 21)
print(numeros.shape)  # (20,)

matriz_4x5 = numeros.reshape(4, 5)
print(matriz_4x5)

matriz_5x4 = matriz_4x5.T
print(matriz_5x4)
print(matriz_5x4.shape)  # (5, 4)

de_volta = matriz_4x5.flatten()
print(de_volta)  # [ 1  2 ... 20]
```

</details>

## Checklist antes de avançar

- [ ] Sei calcular se um reshape é possível (total de elementos precisa bater)
- [ ] Sei usar `-1` para deixar o NumPy calcular uma dimensão automaticamente
- [ ] Entendo o que `.T` (transposta) faz e sei quando `reshape` retorna uma view
- [ ] Resolvi o exercício sem olhar a solução
