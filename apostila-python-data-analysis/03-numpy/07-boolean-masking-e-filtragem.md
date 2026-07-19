# Boolean masking e filtragem

> Módulo 3 — NumPy · Tópico 7 de 7 (último do módulo)

## O que é e por que importa

No Tópico 4 você viu que comparar um array com um valor (`precos > 15`)
retorna um array de `True`/`False` — um para cada elemento. Esse array de
booleanos é chamado de **máscara booleana** (*boolean mask*), e é a
ferramenta central para **filtrar** dados em NumPy: "me dê só os elementos
que atendem a essa condição".

Essa técnica é extremamente importante porque é exatamente como Pandas
filtra linhas de uma tabela (Módulo 4) — dominar o conceito aqui, com arrays
simples, torna o Pandas muito mais intuitivo depois.

## Como funciona (com exemplo comentado)

```python
import numpy as np

notas = np.array([7.5, 8.0, 4.5, 9.0, 3.0, 6.0])

# Passo 1: criar a máscara -- um array de booleanos, mesmo tamanho do original
mascara_aprovados = notas >= 6.0
print(mascara_aprovados)  # [ True  True False  True False  True]

# Passo 2: usar a máscara para indexar o array -- retorna só os elementos "True"
aprovados = notas[mascara_aprovados]
print(aprovados)  # [7.5 8.  9.  6. ]

# Você não precisa guardar a máscara numa variável -- pode indexar direto
reprovados = notas[notas < 6.0]
print(reprovados)  # [4.5 3. ]

# Combinando condições: use & (E) e | (OU) -- NÃO use "and"/"or" do Python puro,
# que não funcionam elemento a elemento em arrays. Cada condição precisa de parênteses.
medianos = notas[(notas >= 5.0) & (notas < 8.0)]
print(medianos)  # [7.5 6. ]

extremos = notas[(notas < 5.0) | (notas >= 9.0)]
print(extremos)  # [4.5 9.  3. ]

# np.where: retorna os ÍNDICES onde a condição é True (ou substitui valores)
indices_aprovados = np.where(notas >= 6.0)
print(indices_aprovados)  # (array([0, 1, 3, 5]),) -- tupla com os índices

# np.where também funciona como um "if/else vetorizado":
situacao = np.where(notas >= 6.0, "aprovado", "reprovado")
print(situacao)  # ['aprovado' 'aprovado' 'reprovado' 'aprovado' 'reprovado' 'aprovado']

# Filtragem também funciona em 2D, retornando um array 1D com os valores que batem
vendas = np.array([
    [100, 120, 90, 130],
    [200, 210, 195, 220],
    [50, 60, 55, 58],
])
vendas_altas = vendas[vendas > 150]
print(vendas_altas)  # [200 210 195 220] -- perdeu a estrutura de matriz, virou 1D

# Modificando valores que atendem a uma condição, direto pela máscara
notas_ajustadas = notas.copy()
notas_ajustadas[notas_ajustadas < 5.0] = 5.0  # "arredonda pra cima" quem tirou menos que 5
print(notas_ajustadas)  # [7.5 8.  5.  9.  5.  6. ]
```

## Erros comuns de quem está começando

- Usar `and`/`or` do Python em vez de `&`/`|` ao combinar condições em
  arrays. `and`/`or` esperam um único valor booleano, não um array inteiro
  deles, e geram erro (`The truth value of an array... is ambiguous`).
- Esquecer os parênteses ao redor de cada condição ao combinar com `&`/`|`:
  `notas >= 5.0 & notas < 8.0` (sem parênteses) dá erro de precedência de
  operadores — o correto é `(notas >= 5.0) & (notas < 8.0)`.
- Confundir `np.where(condicao)` (retorna índices) com indexação booleana
  direta `array[condicao]` (retorna os valores) — os dois resolvem
  problemas parecidos mas retornam coisas diferentes.

## Exercício prático

Uma loja registrou o faturamento diário (em reais) de 10 dias:

```python
faturamento = np.array([1200, 850, 2100, 400, 1750, 3000, 620, 990, 1450, 2600])
```

1. Crie uma máscara booleana para os dias em que o faturamento foi maior que
   R$ 1500.
2. Use a máscara para obter um array só com esses valores.
3. Conte quantos dias tiveram faturamento maior que R$ 1500 (dica: `True`
   vale `1` e `False` vale `0` em operações de soma — `np.sum()` numa máscara
   conta os `True`).
4. Use `np.where` para criar um array de textos classificando cada dia como
   `"bom"` (>= 1500) ou `"fraco"` (< 1500).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import numpy as np

faturamento = np.array([1200, 850, 2100, 400, 1750, 3000, 620, 990, 1450, 2600])

mascara = faturamento > 1500
print(mascara)

dias_bons = faturamento[mascara]
print(dias_bons)  # [2100 1750 3000 2600]

quantidade_dias_bons = np.sum(mascara)
print("Dias com faturamento > 1500:", quantidade_dias_bons)  # 4

classificacao = np.where(faturamento >= 1500, "bom", "fraco")
print(classificacao)
```

</details>

## Checklist antes de avançar

- [ ] Sei criar uma máscara booleana comparando um array com uma condição
- [ ] Sei filtrar um array usando a máscara (`array[mascara]`)
- [ ] Uso `&`/`|` com parênteses (nunca `and`/`or`) para combinar condições em arrays
- [ ] Sei a diferença entre `np.where(condicao)` (índices) e `array[condicao]` (valores)
- [ ] Resolvi o exercício sem olhar a solução

## Checklist do Módulo 3

Antes de seguir para o Módulo 4 (Pandas), confirme que você consegue, sem
consultar a apostila:

- [ ] Criar arrays com `np.array`, `np.arange`, `np.zeros`, `np.ones` e `np.linspace`
- [ ] Indexar e fatiar arrays 1D e 2D
- [ ] Aplicar operações matemáticas a um array inteiro sem usar loop
- [ ] Explicar, em uma frase, o que é broadcasting
- [ ] Calcular soma, média, mínimo, máximo e desvio padrão, inclusive por linha/coluna com `axis`
- [ ] Usar `reshape` para reorganizar um array e `.T` para transpor uma matriz
- [ ] Filtrar um array usando uma máscara booleana

Pronto? Siga para o [Módulo 4 — Pandas Essencial](../04-pandas-essencial/00-indice.md).
