# strip, replace, split

> Módulo 1 — Fundamentos de Python · Tópico 15 de 25

## O que é e por que importa

Continuando de `14-metodos-de-string.md`, este tópico foca em três métodos de string que você vai usar o tempo todo ao trabalhar com dados reais: `strip()` (remove espaços em branco do início/fim), `replace()` (troca um pedaço de texto por outro) e `split()` (quebra um texto em pedaços, formando uma lista).

Dados de vendas, formulários e planilhas raramente chegam "limpos". É comum ter espaços a mais digitados sem querer (`"Ana Silva  "`), separadores misturados (`"produto;preco;quantidade"`) ou textos que precisam de pequenas correções (trocar `"R$"` por nada, para sobrar só o número). Esses três métodos são o kit básico de limpeza de texto — o primeiro passo de qualquer análise de dados de verdade é "limpar" os dados antes de calcular qualquer coisa.

`split()` merece destaque especial porque devolve uma lista (que veremos formalmente em `16-listas.md`) — é o método que transforma uma linha de texto separada por vírgulas (como um arquivo CSV) em pedaços individuais que dá para processar um a um.

## Como funciona (com exemplo comentado)

```python
# strip(): remove espaços (ou quebras de linha) do início e do fim do texto
nome_com_espacos = "   Ana Silva   "
nome_limpo = nome_com_espacos.strip()
print(f"'{nome_limpo}'")  # 'Ana Silva', sem os espaços nas pontas

# strip() não mexe em espaços no meio do texto
print(f"'{nome_limpo}'")  # o espaço entre "Ana" e "Silva" continua lá

# replace(): troca todas as ocorrências de um pedaço de texto por outro
preco_texto = "R$ 25,90"
preco_sem_simbolo = preco_texto.replace("R$ ", "")
print(preco_sem_simbolo)  # "25,90"

# Um caso muito comum em dados brasileiros: trocar vírgula decimal por ponto
# antes de converter para float (visto em 07-conversao-de-tipos.md)
preco_com_ponto = preco_sem_simbolo.replace(",", ".")
preco_numero = float(preco_com_ponto)
print(preco_numero)  # 25.9

# split(): quebra uma string em uma lista de pedaços, usando um separador
linha_csv = "Caneta Azul,5.90,10"
partes = linha_csv.split(",")
print(partes)  # ['Caneta Azul', '5.90', '10']

# Cada pedaço pode ser acessado por índice (igual visto em 13-strings-fundamentos.md)
nome_produto = partes[0]
preco = float(partes[1])
quantidade = int(partes[2])
print(nome_produto, preco, quantidade)

# split() sem argumento quebra por espaços em branco (útil para separar palavras)
frase = "Caneta esferográfica azul ponta fina"
palavras = frase.split()
print(palavras)  # ['Caneta', 'esferográfica', 'azul', 'ponta', 'fina']
```

## Erros comuns de quem está começando

- Esquecer que `strip()` só remove espaços das pontas, não do meio do texto. Para remover espaços do meio, seria preciso usar `replace(" ", "")`, mas isso raramente é o que você quer (destruiria a separação entre palavras).
- Tentar converter direto para `float` um texto com vírgula decimal (`float("25,90")`), o que gera erro em Python — antes é preciso trocar a vírgula por ponto com `replace(",", ".")`.
- Esquecer que `split()` devolve uma lista, e tentar tratar o resultado como se fosse ainda uma string única.

## Exercício prático

A Loja da Ana recebeu a seguinte linha de um sistema antigo, representando uma venda:

```python
linha = "  Caderno Universitário , 12,90 , 3  "
```

1. Use `split(",")` para separar a linha em três partes: nome do produto, preço e quantidade.
2. Para cada parte, use `strip()` para remover espaços indesejados.
3. Converta o preço (trocando vírgula por ponto com `replace()`) e a quantidade para os tipos numéricos corretos.
4. Calcule e mostre o valor total da venda (preço × quantidade).

**Desafio bônus (opcional):** monte uma mensagem final usando f-string, do tipo: `"Venda de 3x Caderno Universitário - Total: R$ 38.7"`.

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```python
linha = "  Caderno Universitário , 12,90 , 3  "

# Separando pelos separadores ","
partes = linha.split(",")
# partes = ['  Caderno Universitário ', ' 12', '90 , 3  ']  <- cuidado, a vírgula
# decimal do preço também seria cortada se usássemos split(",") direto na linha toda!
# Por isso, neste exercício específico, o mais seguro é tratar preço e quantidade
# separadamente. Vamos refazer de forma mais cuidadosa:

nome_bruto = "  Caderno Universitário "
preco_bruto = " 12,90 "
quantidade_bruta = " 3  "

# Limpando espaços de cada parte
nome_produto = nome_bruto.strip()
preco_texto = preco_bruto.strip().replace(",", ".")
quantidade_texto = quantidade_bruta.strip()

# Convertendo para os tipos corretos
preco = float(preco_texto)
quantidade = int(quantidade_texto)

# Calculando o total
total = preco * quantidade
print(f"Venda de {quantidade}x {nome_produto} - Total: R$ {total}")
```

**Nota:** este exercício mostra, de propósito, uma armadilha real de dados brasileiros: quando o preço usa vírgula decimal, não dá para usar `,` como separador de campos ao mesmo tempo. Em dados reais, o separador de campos costuma ser `;` justamente para evitar esse conflito.

</details>

## Checklist antes de avançar

- [ ] Consigo explicar a diferença entre `strip()`, `replace()` e `split()` com minhas próprias palavras
- [ ] Resolvi o exercício sem olhar a solução
- [ ] Entendo por que separador de campo e vírgula decimal podem conflitar em dados brasileiros
