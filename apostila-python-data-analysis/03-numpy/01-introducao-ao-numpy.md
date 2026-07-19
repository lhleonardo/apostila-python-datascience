# Introdução ao NumPy

> Módulo 3 — NumPy · Tópico 1 de 7

## O que é e por que importa

NumPy (*Numerical Python*) é uma biblioteca para trabalhar com **arrays**:
coleções de números organizadas em linhas e colunas (ou mais dimensões), com
operações matemáticas muito rápidas. É a fundação de quase tudo em ciência de
dados com Python — Pandas, Matplotlib, scikit-learn e várias outras
bibliotecas usam NumPy por baixo dos panos.

A pergunta óbvia é: por que não usar listas do Python, que você já conhece?
Duas razões:

- **Velocidade.** Uma lista Python guarda referências para objetos espalhados
  na memória; um array NumPy guarda números "colados" uns nos outros, em
  blocos contíguos. Isso permite que o NumPy delegue as operações para código
  C otimizado, muito mais rápido que um loop Python percorrendo uma lista.
- **Conveniência.** Com listas, somar dois "vetores" elemento a elemento
  exige um loop ou uma list comprehension. Com arrays NumPy, você escreve
  `array1 + array2` e pronto — a operação é aplicada a todos os elementos de
  uma vez (isso se chama **vetorização**, e volta com mais detalhes no
  Tópico 4).

Instalação (caso ainda não tenha, veja `06-pip.md` do Módulo 2 para relembrar):

```bash
pip install numpy
```

A convenção universal é importar NumPy com o apelido `np`:

```python
import numpy as np
```

Praticamente todo código NumPy que você vai ver (em tutoriais, documentação,
Stack Overflow) usa esse apelido — vale a pena adotar desde já.

## Como funciona (com exemplo comentado)

```python
import numpy as np

# Uma lista Python comum
precos_lista = [10.0, 25.5, 8.75, 42.0]

# Um array NumPy criado a partir da lista
precos_array = np.array(precos_lista)

print(precos_array)        # [10.   25.5   8.75 42.  ]
print(type(precos_array))  # <class 'numpy.ndarray'> -- "ndarray" = N-dimensional array

# Diferença prática: aplicar um aumento de 10% em todos os preços

# Com lista, precisa de loop ou list comprehension:
precos_lista_novos = [p * 1.10 for p in precos_lista]

# Com array, a operação é aplicada direto, sem loop explícito:
precos_array_novos = precos_array * 1.10

print(precos_lista_novos)  # [11.0, 28.05, 9.625, 46.2]
print(precos_array_novos)  # [11.    28.05   9.625 46.2  ]

# Arrays NumPy também têm atributos úteis
print(precos_array.shape)  # (4,) -- formato do array: 4 elementos, uma dimensão
print(precos_array.dtype)  # float64 -- tipo dos dados guardados no array
print(precos_array.ndim)   # 1 -- número de dimensões (1D, como uma lista simples)
```

Um ponto importante: **um array NumPy só guarda um tipo de dado por vez**
(todos `int`, todos `float`, etc.), diferente de uma lista Python, que pode
misturar tipos livremente. Se você criar um array com valores mistos, o
NumPy converte tudo para um tipo comum:

```python
misto = np.array([1, 2.5, 3])
print(misto)        # [1.  2.5 3. ]  -- o inteiro 1 virou 1.0
print(misto.dtype)  # float64
```

## Erros comuns de quem está começando

- Confundir array NumPy com lista Python e tentar usar métodos de lista
  (como `.append()`) que não existem (ou funcionam diferente) em arrays —
  arrays têm tamanho fixo por padrão; "crescer" um array repetidamente é
  caro e normalmente sinal de que uma lista comum seria mais apropriada até
  o momento de converter para array.
- Esquecer o `import numpy as np` e tentar usar `numpy.array(...)` direto, ou
  usar um apelido diferente do padrão `np` — funciona, mas quebra a
  convenção que todo mundo espera ao ler seu código.
- Achar que `np.array([1, 2, 3])` e `[1, 2, 3]` se comportam igual em
  operações matemáticas. `[1, 2, 3] * 2` duplica a lista (`[1, 2, 3, 1, 2, 3]`);
  `np.array([1, 2, 3]) * 2` multiplica cada elemento por 2
  (`[2, 4, 6]`) — comportamentos completamente diferentes para o mesmo
  operador.

## Exercício prático

Crie uma lista Python com as temperaturas (em Celsius) de 5 dias:
`[21.5, 19.0, 23.2, 18.7, 25.1]`. Converta essa lista para um array NumPy.
Depois:

1. Imprima o `shape`, o `dtype` e o `ndim` do array.
2. Converta todas as temperaturas para Fahrenheit usando a fórmula
   `F = C * 9/5 + 32`, aplicando a operação direto no array (sem loop).
3. Imprima o resultado.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import numpy as np

temperaturas_c = [21.5, 19.0, 23.2, 18.7, 25.1]
temperaturas_array = np.array(temperaturas_c)

print("shape:", temperaturas_array.shape)
print("dtype:", temperaturas_array.dtype)
print("ndim:", temperaturas_array.ndim)

temperaturas_f = temperaturas_array * 9 / 5 + 32
print(temperaturas_f)
```

</details>

## Checklist antes de avançar

- [ ] Entendo por que arrays NumPy são mais rápidos que listas para cálculos numéricos
- [ ] Sei importar NumPy com o apelido convencional `np`
- [ ] Consigo explicar a diferença entre `lista * 2` e `array * 2`
- [ ] Resolvi o exercício sem olhar a solução
