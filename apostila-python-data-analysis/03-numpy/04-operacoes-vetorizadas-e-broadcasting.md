# Operações vetorizadas e broadcasting

> Módulo 3 — NumPy · Tópico 4 de 7

## O que é e por que importa

No Tópico 1 você já viu um exemplo de **vetorização**: multiplicar um array
inteiro por um número (`precos_array * 1.10`) sem precisar de loop. Esse é o
recurso mais poderoso do NumPy, e vale entender com mais profundidade — é o
que faz o código de análise de dados ser curto, legível e rápido.

**Broadcasting** é a regra que o NumPy usa para decidir como aplicar uma
operação entre arrays de formatos (shapes) diferentes, "esticando"
mentalmente o menor para combinar com o maior, sem realmente duplicar dados
na memória. Entender broadcasting evita muita confusão (e muitos
`ValueError`) ao operar com arrays de tamanhos diferentes.

## Como funciona (com exemplo comentado)

```python
import numpy as np

# Operações entre um array e um número (escalar) -- o número é aplicado a cada elemento
precos = np.array([10.0, 20.0, 30.0])
print(precos + 5)     # [15. 25. 35.]
print(precos * 2)     # [20. 40. 60.]
print(precos ** 2)    # [100. 400. 900.]

# Operações entre dois arrays de MESMO shape -- elemento a elemento (posição a posição)
quantidades = np.array([3, 1, 2])
print(precos * quantidades)  # [30. 20. 60.] -- preco[0]*qtd[0], preco[1]*qtd[1], ...

# Funções matemáticas do NumPy também são vetorizadas
notas = np.array([7.2, 8.9, 5.5, 9.8])
print(np.round(notas))    # [7. 9. 6. 10.] -- arredonda cada elemento
print(np.sqrt(np.array([4, 9, 16])))  # [2. 3. 4.]

# Broadcasting: operação entre array 2D e array 1D de shape compatível
# Matriz de vendas: 3 produtos (linhas) x 4 meses (colunas)
vendas = np.array([
    [100, 120, 90, 130],
    [200, 210, 195, 220],
    [50, 60, 55, 58],
])

# Um array 1D com 4 valores (um por mês) é "esticado" para combinar com cada linha
ajuste_mensal = np.array([1.0, 1.05, 0.95, 1.10])  # shape (4,) -- combina com colunas
vendas_ajustadas = vendas * ajuste_mensal
print(vendas_ajustadas)
# cada COLUNA da matriz foi multiplicada pelo valor correspondente em ajuste_mensal

# Comparação (operadores de comparação também são vetorizados)
print(precos > 15)  # [False  True  True] -- array de booleanos, usado no Tópico 7
```

A regra de broadcasting, resumida: o NumPy compara os `shape`s dos dois
arrays "de trás para frente" (da última dimensão para a primeira). Duas
dimensões são compatíveis se forem iguais, ou se uma delas for 1 (nesse
caso, o NumPy "repete" o valor). Se nenhuma condição valer, dá erro.

```python
a = np.zeros((3, 4))  # shape (3, 4)
b = np.array([1, 2, 3, 4])  # shape (4,)
c = a + b  # funciona: (4,) combina com a última dimensão de (3, 4)

d = np.array([1, 2, 3])  # shape (3,)
# e = a + d  # ERRO: (3,) não combina com a última dimensão (4) de (3, 4)
```

## Erros comuns de quem está começando

- Tentar somar/multiplicar dois arrays de shapes incompatíveis e não entender
  a mensagem de erro (`ValueError: operands could not be broadcast together`)
  — o primeiro passo para debugar é sempre imprimir o `.shape` dos dois
  arrays envolvidos.
- Usar loop `for` para aplicar uma operação matemática simples a um array,
  quando a versão vetorizada (`array * 2`, `np.sqrt(array)`, etc.) já resolve
  — além de mais lento, é um sinal de que "pensamento NumPy" ainda não
  aconteceu. Se você se pegar escrevendo `for i in range(len(array))` para
  fazer conta, pare e pergunte: "dá pra vetorizar isso?".
- Achar que `array1 * array2` faz multiplicação de matrizes (álgebra linear).
  Em NumPy, `*` é sempre elemento a elemento; multiplicação de matrizes usa
  `@` ou `np.matmul()` — fora do escopo desta apostila, mas bom saber que
  existe essa diferença.

## Exercício prático

Uma loja tem os preços de 4 produtos: `[50.0, 120.0, 15.5, 300.0]`. Ela vai
aplicar um reajuste diferente para cada produto:
`[1.10, 1.05, 1.20, 0.95]` (10% de aumento no primeiro, 5% no segundo, 20% no
terceiro, 5% de desconto no quarto).

1. Calcule os novos preços com uma operação vetorizada (sem loop).
2. Calcule quanto cada produto aumentou ou diminuiu em valor absoluto
   (novo preço menos preço antigo).
3. Descubra quais produtos ficaram mais caros que R$ 100,00 usando um
   operador de comparação (deve retornar um array de booleanos).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import numpy as np

precos = np.array([50.0, 120.0, 15.5, 300.0])
reajustes = np.array([1.10, 1.05, 1.20, 0.95])

novos_precos = precos * reajustes
print(novos_precos)  # [55. 126. 18.6 285.]

diferenca = novos_precos - precos
print(diferenca)  # [5. 6. 3.1 -15.]

mais_caros_que_100 = novos_precos > 100
print(mais_caros_que_100)  # [False  True False  True]
```

</details>

## Checklist antes de avançar

- [ ] Sei aplicar operações matemáticas a um array inteiro sem usar loop
- [ ] Entendo a regra básica de broadcasting (comparar shapes de trás para frente)
- [ ] Sei que `*` entre arrays é elemento a elemento, não multiplicação de matrizes
- [ ] Resolvi o exercício sem olhar a solução
