# Google Colab

> Módulo 2 — Python Intermediário e Ambiente · Tópico 11 de 11

## O que é e por que importa

Google Colab (ou "Colaboratory") é um serviço do Google que roda notebooks Jupyter (o mesmo formato de células de código e markdown visto em `10-jupyterlab.md`) inteiramente na nuvem, direto no navegador — sem precisar instalar Python, JupyterLab, nem nenhuma biblioteca no seu computador.

Pensa no Colab como o Google Docs dos notebooks: assim como você abre o Google Docs no navegador e escreve um documento sem instalar o Word, você abre o Colab no navegador e escreve/roda código Python sem instalar nada. O Google mantém, "do outro lado", um computador (o servidor) rodando o Python e as bibliotecas para você — inclusive já vem com pandas, numpy, matplotlib e várias outras bibliotecas de dados pré-instaladas, prontas para usar.

Isso torna o Colab uma porta de entrada excelente para quem está aprendendo (ou para testar uma ideia rapidamente): não existe barreira de instalação, funciona em qualquer computador com navegador e internet, é gratuito para uso básico, e os notebooks ficam salvos no seu Google Drive, acessíveis de qualquer lugar. A limitação principal é justamente a dependência da nuvem: sem internet, não tem Colab, e as sessões gratuitas **expiram** depois de um tempo de inatividade (ou depois de várias horas seguidas rodando) — quando isso acontece, você perde tudo que estava na memória (as variáveis calculadas), embora o texto do notebook em si continue salvo.

## Como funciona (com exemplo comentado)

Passo a passo para começar a usar:

```text
1. Acesse colab.research.google.com no navegador (é necessário ter uma conta Google).
2. Clique em "New Notebook" (Novo notebook) para criar um notebook em branco.
3. O notebook já abre com uma célula de código vazia -- funciona exatamente
   como no JupyterLab: Shift+Enter roda a célula atual.
4. Para adicionar uma célula de markdown, use o botão "+ Texto" na barra
   superior (ou "+ Code" para adicionar mais uma célula de código).
5. O notebook salva automaticamente no seu Google Drive, na pasta
   "Colab Notebooks", conforme você trabalha -- não é preciso "salvar"
   manualmente com frequência, mas vale conferir de vez em quando.
```

O código dentro das células funciona igual ao que você já viu:

```python
# Célula de código -- já roda direto, sem precisar instalar pandas antes,
# pois o Colab já vem com as principais bibliotecas de dados pré-instaladas
import random

produtos = ["Caneta Azul", "Caderno", "Mochila", "Lapis HB"]
random.seed(1)

vendas_simuladas = []
for _ in range(5):
    venda = {
        "produto": random.choice(produtos),
        "quantidade": random.randint(1, 5),
    }
    vendas_simuladas.append(venda)

for venda in vendas_simuladas:
    print(venda)
```

```text
# Se, mesmo assim, precisar de uma biblioteca que NÃO vem pré-instalada,
# funciona igual ao pip normal -- só rodar num célula de código com um "!" na frente,
# indicando que aquela linha é um comando de terminal, não Python:
!pip install nome-da-biblioteca
```

Vantagens principais: gratuito (com limites de uso), zero instalação, acesso de qualquer computador com navegador, ótimo para compartilhar um notebook com outra pessoa (parecido com compartilhar um link do Google Docs) e ótimo para quem está começando e não quer lidar com configuração de ambiente ainda.

Limitações principais: precisa de internet o tempo todo, sessões gratuitas têm limite de tempo de uso contínuo e expiram por inatividade (perdendo o que estava na memória, precisando rodar as células de novo), e o poder de processamento das máquinas gratuitas é limitado comparado a rodar localmente em um computador potente.

## Erros comuns de quem está começando

- Achar que, depois que a sessão expira, o notebook "perdeu tudo". Só a **memória** (variáveis calculadas) se perde — o texto e código do notebook continuam salvos no Drive. Basta rodar as células de novo, na ordem certa, para recalcular tudo.
- Fazer upload de arquivos de dados (CSV, JSON) direto na sessão do Colab e depois perder esses arquivos quando a sessão expira — arquivos enviados diretamente para a sessão não ficam salvos permanentemente. Para dados que você quer manter entre sessões, é melhor guardá-los no Google Drive e conectar o Drive ao notebook.
- Confundir Colab com JupyterLab achando que são coisas totalmente diferentes. Na prática, o formato do notebook (`.ipynb`, células de código e markdown, ordem de execução) é o mesmo — a diferença é só **onde** ele roda: no seu computador (JupyterLab) ou na nuvem do Google (Colab).

## Exercício prático

Acesse o Google Colab (colab.research.google.com) e crie um notebook novo. Nele:

1. Em uma célula de markdown, escreva um título `## Simulação de vendas — Loja da Ana`.
2. Em uma célula de código, importe o módulo `random`, defina uma seed com `random.seed(5)`, e crie uma lista de 6 vendas simuladas (cada uma um dicionário com `"produto"` e `"quantidade"`, reaproveitando a lógica de `02-modulo-random.md`).
3. Em outra célula, calcule a quantidade total vendida somando o campo `"quantidade"` de todas as vendas simuladas.

**Desafio bônus (opcional):** feche a aba do navegador, espere alguns minutos, e reabra o notebook pelo seu Google Drive. Rode as células de novo, na ordem, e confirme que o resultado é o mesmo de antes (graças à `seed` fixa).

## Solução comentada

<details>
<summary>Clique para ver a solução</summary>

```text
Célula 1 (markdown):
## Simulação de vendas — Loja da Ana
```

```python
# Célula 2 (código)
import random

random.seed(5)
produtos = ["Caneta Azul", "Caderno", "Mochila", "Lapis HB"]

vendas_simuladas = []
for _ in range(6):
    venda = {
        "produto": random.choice(produtos),
        "quantidade": random.randint(1, 5),
    }
    vendas_simuladas.append(venda)

for venda in vendas_simuladas:
    print(venda)
```

```python
# Célula 3 (código)
quantidade_total = sum(venda["quantidade"] for venda in vendas_simuladas)
print("Quantidade total vendida:", quantidade_total)
```

Desafio bônus: como usamos `random.seed(5)`, rodar as células de novo (na mesma ordem) sempre gera exatamente a mesma sequência de vendas simuladas — por isso o resultado bate, mesmo depois da sessão reiniciar.

</details>

## Checklist antes de avançar

- [ ] Consigo explicar a diferença entre Colab e JupyterLab
- [ ] Entendo o que se perde (e o que não se perde) quando uma sessão do Colab expira
- [ ] Resolvi o exercício sem olhar a solução
