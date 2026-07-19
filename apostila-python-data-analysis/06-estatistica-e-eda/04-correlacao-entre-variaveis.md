# Correlação entre variáveis

> Módulo 6 — Estatística e EDA · Tópico 4 de 8

## O que é e por que importa

Correlação mede o quanto duas variáveis numéricas se movem **juntas**: quando
uma aumenta, a outra também aumenta (correlação positiva)? Diminui
(correlação negativa)? Ou não há relação aparente (correlação perto de
zero)? É uma das perguntas mais comuns em EDA — "o preço tem relação com a
avaliação do produto?", "gastos em marketing se relacionam com vendas?" — e
o primeiro passo antes de qualquer modelo preditivo.

O coeficiente mais comum é o de **Pearson**, que varia de -1 a 1:

- **+1**: correlação positiva perfeita (uma sobe exatamente na mesma
  proporção que a outra).
- **-1**: correlação negativa perfeita (uma sobe exatamente na proporção
  inversa da outra).
- **0**: nenhuma correlação linear detectável.

Valores intermediários (0.3, 0.7, -0.5...) indicam correlações mais fracas
ou mais fortes.

## Como funciona (com exemplo comentado)

```python
import pandas as pd

df = pd.DataFrame({
    "horas_estudo": [1, 2, 3, 4, 5, 6, 7, 8],
    "nota_prova": [3.0, 4.2, 5.0, 5.8, 7.1, 7.5, 8.9, 9.5],
    "faltas": [8, 7, 6, 5, 3, 2, 1, 0],
})

# .corr() entre duas colunas -- retorna um único número
correlacao_horas_nota = df["horas_estudo"].corr(df["nota_prova"])
print(correlacao_horas_nota)  # perto de 1 -- forte correlação positiva

correlacao_horas_faltas = df["horas_estudo"].corr(df["faltas"])
print(correlacao_horas_faltas)  # perto de -1 -- forte correlação negativa

# .corr() no DataFrame inteiro -- matriz de correlação entre TODAS as colunas numéricas
matriz_correlacao = df.corr(numeric_only=True)
print(matriz_correlacao)
#                horas_estudo  nota_prova  faltas
# horas_estudo       1.000000    0.992...  -0.994...
# nota_prova         0.992...    1.000000  -0.980...
# faltas            -0.994...   -0.980...   1.000000
# -- a diagonal é sempre 1 (uma coluna tem correlação perfeita com ela mesma);
#    a matriz é simétrica (corr entre A e B é igual à corr entre B e A)

# Interpretação prática de faixas de força (regra geral, não absoluta):
# |r| < 0.3          -> fraca ou nenhuma
# 0.3 <= |r| < 0.7    -> moderada
# |r| >= 0.7          -> forte

# Correlação NÃO implica causalidade -- clássico aviso da estatística.
# Duas variáveis podem se mover juntas por coincidência ou por uma terceira
# causa comum, sem que uma cause a outra diretamente. Exemplo clássico:
# vendas de sorvete e afogamentos sobem juntos no verão -- não é que sorvete
# cause afogamento, o calor do verão influencia os dois.

# Correlação captura relação LINEAR -- duas variáveis podem ter uma relação
# forte, só que não-linear (curva), e o coeficiente de Pearson não detecta
# isso bem. Sempre vale visualizar (Módulo 7) além de calcular o número.
```

## Erros comuns de quem está começando

- Concluir que uma variável **causa** o comportamento da outra só porque a
  correlação é alta — correlação é só um indício estatístico, nunca prova
  de causalidade. Estabelecer causa exige desenho experimental (fora do
  escopo desta apostila), não apenas cálculo de correlação.
- Calcular `.corr()` em colunas de texto/categóricas sem converter antes —
  `numeric_only=True` evita erro ao rodar `.corr()` num DataFrame com
  colunas mistas, ignorando automaticamente as não-numéricas.
- Confiar cegamente no número de correlação sem visualizar os dados —
  relações não-lineares (em forma de U, por exemplo) podem ter correlação de
  Pearson próxima de zero mesmo havendo uma relação forte entre as
  variáveis, só que não-linear.

## Exercício prático

```python
df = pd.DataFrame({
    "temperatura": [15, 18, 22, 25, 28, 30, 32, 20],
    "vendas_sorvete": [50, 80, 120, 180, 250, 300, 320, 100],
    "vendas_casaco": [200, 150, 90, 60, 20, 10, 5, 130],
})
```

1. Calcule a correlação entre `temperatura` e `vendas_sorvete`.
2. Calcule a correlação entre `temperatura` e `vendas_casaco`.
3. Gere a matriz de correlação completa do DataFrame.
4. Com base nos números, escreva (em um comentário) uma frase interpretando
   cada correlação, tomando cuidado para não afirmar causalidade.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
import pandas as pd

df = pd.DataFrame({
    "temperatura": [15, 18, 22, 25, 28, 30, 32, 20],
    "vendas_sorvete": [50, 80, 120, 180, 250, 300, 320, 100],
    "vendas_casaco": [200, 150, 90, 60, 20, 10, 5, 130],
})

print(df["temperatura"].corr(df["vendas_sorvete"]))  # próximo de 1 -- forte positiva
print(df["temperatura"].corr(df["vendas_casaco"]))    # próximo de -1 -- forte negativa

print(df.corr(numeric_only=True))

# Interpretação: temperatura e vendas de sorvete se movem fortemente juntas
# (correlação positiva forte); temperatura e vendas de casaco se movem em
# direções opostas (correlação negativa forte). Isso não prova que a
# temperatura CAUSA essas vendas, apenas que estão fortemente associadas
# nesses dados.
```

</details>

## Checklist antes de avançar

- [ ] Sei calcular correlação entre duas colunas e a matriz de correlação de um DataFrame
- [ ] Sei interpretar o sinal (positivo/negativo) e a força (perto de 0, 0.5, 1) de uma correlação
- [ ] Sei explicar por que correlação não implica causalidade
- [ ] Resolvi o exercício sem olhar a solução
