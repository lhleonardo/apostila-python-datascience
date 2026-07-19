# Indexação e slicing

> Módulo 3 — NumPy · Tópico 3 de 7

## O que é e por que importa

Você já sabe indexar e fatiar listas Python (`lista[0]`, `lista[1:3]`) — veja
`16-listas.md` do Módulo 1 se precisar relembrar. Arrays NumPy usam a mesma
ideia, mas estendida para múltiplas dimensões, com uma sintaxe que evita
loops aninhados para acessar linhas, colunas ou sub-regiões de uma matriz.

Entender bem indexação é essencial: é como você vai "recortar" pedaços dos
seus dados — pegar só uma coluna, só as primeiras 10 linhas, só os valores
que atendem a uma condição (isso último vem com mais detalhes no Tópico 7).

## Como funciona (com exemplo comentado)

```python
import numpy as np

# Indexação em array 1D -- igual a lista Python
notas = np.array([7.5, 8.0, 6.5, 9.0, 5.5])
print(notas[0])     # 7.5 -- primeiro elemento
print(notas[-1])    # 5.5 -- último elemento
print(notas[1:3])   # [8.  6.5] -- fatia do índice 1 até 3 (exclusivo)

# Indexação em array 2D -- use [linha, coluna], separado por vírgula
# (diferente de lista de listas em Python puro, onde seria lista[linha][coluna])
matriz = np.array([
    [10, 20, 30],
    [40, 50, 60],
    [70, 80, 90],
])

print(matriz[0, 0])    # 10 -- linha 0, coluna 0
print(matriz[1, 2])    # 60 -- linha 1, coluna 2
print(matriz[2])       # [70 80 90] -- linha inteira (índice 2)

# Fatiamento também funciona com vírgula: [linhas, colunas]
print(matriz[:, 0])     # [10 40 70] -- todas as linhas, só a coluna 0
print(matriz[0, :])     # [10 20 30] -- só a linha 0, todas as colunas
print(matriz[0:2, 1:3]) # [[20 30] [50 60]] -- linhas 0-1, colunas 1-2

# Atenção: slicing em NumPy retorna uma "view" (referência), não uma cópia!
fatia = notas[1:3]
fatia[0] = 999
print(notas)  # [7.5 999. 6.5 9. 5.5] -- o array ORIGINAL também mudou!

# Para evitar isso, use .copy() explicitamente quando precisar de uma cópia independente
fatia_segura = notas[1:3].copy()
fatia_segura[0] = -1
print(notas)  # não foi afetado dessa vez
```

Esse comportamento de "view" é diferente de listas Python (onde `lista[1:3]`
sempre cria uma lista nova). É uma decisão de design do NumPy para performance
— copiar dados o tempo todo seria caro para arrays grandes — mas é uma
armadilha comum para quem vem de listas puras.

## Erros comuns de quem está começando

- Usar `matriz[linha][coluna]` em vez de `matriz[linha, coluna]`. O primeiro
  até funciona (primeiro pega a linha, depois indexa nela), mas é mais lento
  e não é a forma idiomática em NumPy — prefira sempre a vírgula.
- Esquecer que slices são "views" e alterar uma fatia achando que o array
  original não seria afetado, causando bugs difíceis de rastrear.
- Trocar a ordem de linha e coluna: `matriz[:, 0]` (coluna 0 inteira) não é o
  mesmo que `matriz[0, :]` (linha 0 inteira) — sempre "linha primeiro, coluna
  depois", igual ao `shape`.

## Exercício prático

Crie a matriz abaixo com NumPy:

```
[[ 1,  2,  3,  4],
 [ 5,  6,  7,  8],
 [ 9, 10, 11, 12]]
```

1. Imprima o elemento da linha 2, coluna 3 (deve ser `11`).
2. Imprima a segunda coluna inteira (deve ser `[2 6 10]`).
3. Imprima a submatriz formada pelas duas primeiras linhas e as duas últimas
   colunas.
4. Faça uma cópia da primeira linha, altere o primeiro valor da cópia para
   `100`, e confirme (imprimindo a matriz original) que ela não foi afetada.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import numpy as np

matriz = np.array([
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12],
])

print(matriz[2, 3])       # 11

print(matriz[:, 1])       # [2 6 10]

print(matriz[0:2, 2:4])   # [[3 4] [7 8]]

copia_linha = matriz[0, :].copy()
copia_linha[0] = 100
print(copia_linha)  # [100 2 3 4]
print(matriz)        # linha 0 continua [1 2 3 4] -- não foi afetada
```

</details>

## Checklist antes de avançar

- [ ] Sei indexar e fatiar arrays 1D e 2D usando a sintaxe `[linha, coluna]`
- [ ] Entendo a diferença entre "view" e cópia, e sei quando usar `.copy()`
- [ ] Consigo pegar uma linha, uma coluna ou uma submatriz específica de uma matriz
- [ ] Resolvi o exercício sem olhar a solução
