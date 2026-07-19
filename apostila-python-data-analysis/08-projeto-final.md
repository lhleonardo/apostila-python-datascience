# Projeto Final — Case Olist: Análise de Vendas de E-commerce

> 5–7 dias

## O contexto

Este projeto é modelado como um **case de contratação real**, do tipo que
empresas de tecnologia aplicam em processos seletivos para analista de
dados júnior/pleno. Não é um exercício aberto de "escolha um dataset que
você goste" — é um problema fechado, com pedido específico de um
stakeholder fictício, perguntas de negócio definidas e critérios de entrega
claros. A ideia é simular a experiência de um teste técnico de verdade.

**O brief:**

> Você acabou de ser contratado(a) como Analista de Dados Júnior na Olist,
> uma plataforma brasileira que conecta pequenos e médios vendedores a
> grandes marketplaces (como Americanas, Mercado Livre e outros). Seu
> primeiro projeto: a diretoria comercial quer entender o desempenho da
> plataforma entre 2017 e 2018 antes de definir a estratégia do próximo
> trimestre. Você tem uma semana para entregar uma análise completa, com
> um relatório executivo respondendo às perguntas abaixo.

## O dataset

Este projeto usa o **Brazilian E-Commerce Public Dataset by Olist**, um
dataset público real, disponível no Kaggle:
`https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce`

São ~100 mil pedidos reais e anonimizados, feitos na plataforma entre 2016 e
2018, espalhados em várias tabelas relacionadas por `order_id`,
`customer_id`, `product_id` e `seller_id`:

| Arquivo | Conteúdo |
|---|---|
| `olist_orders_dataset.csv` | Pedidos: status, datas de compra/aprovação/entrega |
| `olist_order_items_dataset.csv` | Itens de cada pedido: produto, vendedor, preço, frete |
| `olist_order_payments_dataset.csv` | Forma de pagamento, parcelas, valor pago |
| `olist_order_reviews_dataset.csv` | Nota (1 a 5) e comentário da avaliação do pedido |
| `olist_customers_dataset.csv` | Cidade/estado do cliente |
| `olist_sellers_dataset.csv` | Cidade/estado do vendedor |
| `olist_products_dataset.csv` | Categoria, peso e dimensões do produto |
| `product_category_name_translation.csv` | Tradução do nome da categoria (PT → EN) |

**Como obter:** crie uma conta gratuita no Kaggle, baixe o dataset (botão
"Download") e extraia os CSVs numa pasta `dados/` no seu projeto. Se
preferir via linha de comando, a [Kaggle API](https://www.kaggle.com/docs/api)
permite `kaggle datasets download -d olistbr/brazilian-ecommerce`.

**Backup caso não consiga baixar (sem conta Kaggle, sem internet estável,
etc.):** o script abaixo gera uma versão sintética, porém realista, com o
mesmo esquema de tabelas e relacionamentos — menor (5 mil pedidos), mas
suficiente para responder a todas as perguntas do projeto. Rode uma vez e
use os CSVs gerados exatamente como usaria os originais.

```python
import numpy as np
import pandas as pd
import os

np.random.seed(42)
os.makedirs("dados", exist_ok=True)

n_pedidos = 5000
n_clientes = 3000
n_vendedores = 200
categorias = ["cama_mesa_banho", "beleza_saude", "esporte_lazer", "informatica_acessorios",
              "moveis_decoracao", "eletronicos", "brinquedos", "relogios_presentes"]
estados = ["SP", "RJ", "MG", "RS", "PR", "SC", "BA", "DF", "GO", "PE"]

# clientes
clientes = pd.DataFrame({
    "customer_id": [f"cust_{i}" for i in range(n_clientes)],
    "customer_state": np.random.choice(estados, n_clientes, p=[.42,.13,.12,.06,.05,.04,.05,.04,.05,.04]),
})
clientes.to_csv("dados/olist_customers_dataset.csv", index=False)

# vendedores
vendedores = pd.DataFrame({
    "seller_id": [f"seller_{i}" for i in range(n_vendedores)],
    "seller_state": np.random.choice(estados, n_vendedores),
})
vendedores.to_csv("dados/olist_sellers_dataset.csv", index=False)

# produtos
n_produtos = 800
produtos = pd.DataFrame({
    "product_id": [f"prod_{i}" for i in range(n_produtos)],
    "product_category_name": np.random.choice(categorias, n_produtos),
    "product_weight_g": np.random.randint(100, 15000, n_produtos),
})
produtos.to_csv("dados/olist_products_dataset.csv", index=False)

# pedidos + datas (com atraso simulado em ~15% dos casos)
datas_compra = pd.to_datetime("2017-01-01") + pd.to_timedelta(
    np.random.randint(0, 600, n_pedidos), unit="D"
)
dias_para_entrega_estimada = np.random.randint(7, 20, n_pedidos)
atraso = np.where(np.random.random(n_pedidos) < 0.15,
                   np.random.randint(3, 15, n_pedidos), 0)
dias_reais = dias_para_entrega_estimada + np.random.randint(-3, 5, n_pedidos) + atraso

pedidos = pd.DataFrame({
    "order_id": [f"order_{i}" for i in range(n_pedidos)],
    "customer_id": np.random.choice(clientes["customer_id"], n_pedidos),
    "order_status": np.random.choice(
        ["delivered", "shipped", "canceled"], n_pedidos, p=[.92, .05, .03]
    ),
    "order_purchase_timestamp": datas_compra,
    "order_estimated_delivery_date": datas_compra + pd.to_timedelta(dias_para_entrega_estimada, unit="D"),
    "order_delivered_customer_date": datas_compra + pd.to_timedelta(dias_reais, unit="D"),
})
# introduz valores ausentes de propósito (pedidos não entregues não têm data de entrega)
pedidos.loc[pedidos["order_status"] != "delivered", "order_delivered_customer_date"] = pd.NaT
pedidos.to_csv("dados/olist_orders_dataset.csv", index=False)

# itens do pedido (1 a 3 itens por pedido)
linhas_itens = []
for order_id in pedidos["order_id"]:
    for _ in range(np.random.randint(1, 4)):
        linhas_itens.append({
            "order_id": order_id,
            "product_id": np.random.choice(produtos["product_id"]),
            "seller_id": np.random.choice(vendedores["seller_id"]),
            "price": round(np.random.uniform(15, 800), 2),
            "freight_value": round(np.random.uniform(5, 80), 2),
        })
itens = pd.DataFrame(linhas_itens)
itens.to_csv("dados/olist_order_items_dataset.csv", index=False)

# pagamentos
pagamentos = pd.DataFrame({
    "order_id": pedidos["order_id"],
    "payment_type": np.random.choice(
        ["credit_card", "boleto", "voucher", "debit_card"], n_pedidos, p=[.75, .15, .06, .04]
    ),
    "payment_installments": np.random.randint(1, 13, n_pedidos),
    "payment_value": np.round(np.random.uniform(30, 1200, n_pedidos), 2),
})
pagamentos.to_csv("dados/olist_order_payments_dataset.csv", index=False)

# avaliações -- nota mais baixa quando houve atraso (correlação de propósito)
notas = np.where(atraso > 0,
                  np.random.choice([1, 2, 3], n_pedidos, p=[.4, .35, .25]),
                  np.random.choice([3, 4, 5], n_pedidos, p=[.1, .35, .55]))
avaliacoes = pd.DataFrame({
    "order_id": pedidos["order_id"],
    "review_score": notas,
})
avaliacoes.to_csv("dados/olist_order_reviews_dataset.csv", index=False)

print("Dados sintéticos gerados em dados/")
```

## As perguntas de negócio

O relatório final precisa responder, especificamente, a estas 8 perguntas
(não é uma lista de sugestões — são as perguntas que o "stakeholder"
pediu):

1. **Evolução de receita.** Como a receita mensal (soma de `price` dos
   itens entregues) evoluiu entre o primeiro e o último mês do dataset?
   Existe alguma sazonalidade visível?
2. **Prazo de entrega x satisfação.** Existe relação entre o atraso na
   entrega (`order_delivered_customer_date` menos
   `order_estimated_delivery_date`) e a nota da avaliação
   (`review_score`)? Quantifique com correlação e mostre visualmente.
3. **Top categorias.** Quais as 10 categorias de produto (`product_category_name`)
   com maior receita total? E quais têm o maior frete médio proporcional ao
   preço (`freight_value / price`)?
4. **Regionalidade.** O valor médio de pedido (soma de `payment_value` por
   `order_id`) varia entre os estados dos clientes? Existe uma região que
   se destaca para cima ou para baixo?
5. **Forma de pagamento.** Qual a forma de pagamento mais usada, e existe
   relação entre `payment_type` e o número médio de parcelas
   (`payment_installments`) ou o valor do pedido?
6. **Concentração de vendedores.** Os 20% de vendedores que mais vendem
   respondem por quanto da receita total? (Aplique a lógica do princípio de
   Pareto/80-20 usando os dados reais, não assuma o percentual.)
7. **Qualidade dos dados.** Quais problemas de qualidade você encontrou
   (valores ausentes, duplicatas, tipos incorretos, outliers) em pelo menos
   3 das tabelas, e como tratou cada um? Justifique a estratégia escolhida
   para cada problema.
8. **Recomendação final.** Com base em tudo isso, dê **uma** recomendação
   concreta e acionável para a diretoria comercial sobre onde focar no
   próximo trimestre (ex: uma categoria, uma região, um problema
   operacional), justificada pelos dados.

## Requisitos técnicos obrigatórios

Sua análise só está completa se, ao final, você consegue apontar onde no
código cada um destes itens foi cumprido:

- [ ] Combinou pelo menos **3 tabelas diferentes** com `merge` (Módulo 4, Tópico 10), escolhendo o `how` correto para cada junção e justificando a escolha.
- [ ] Diagnosticou e tratou valores ausentes, duplicatas e tipos de dados incorretos (Módulo 5), com pelo menos uma decisão de "remover" e uma de "preencher" justificadas.
- [ ] Converteu corretamente as colunas de data para `datetime` e calculou pelo menos uma métrica derivada de datas (ex: dias de atraso, mês da compra) (Módulo 5, Tópico 5).
- [ ] Usou `groupby` + `.agg()` com múltiplas agregações em pelo menos 2 pontos da análise (Módulo 4, Tópicos 8 e 9).
- [ ] Calculou e interpretou pelo menos uma matriz de correlação (Módulo 6, Tópico 4), sem confundir correlação com causalidade no texto do relatório.
- [ ] Produziu pelo menos **6 gráficos**, cobrindo no mínimo: 1 gráfico de linha (evolução temporal), 1 gráfico de barra (comparação de categorias), 1 boxplot (comparação de distribuição entre grupos), 1 scatter plot ou heatmap (relação entre variáveis) — todos com título, rótulos de eixo e, quando aplicável, legenda (Módulo 7).
- [ ] Discutiu explicitamente ao menos um caso de outlier ou de diferença entre média e mediana no texto do relatório (Módulo 5, Tópico 6 e Módulo 6, Tópico 1).
- [ ] Reconheceu pelo menos uma limitação dos dados ou da análise no relatório final (ex: amostra pequena de algum grupo, período coberto, dados sintéticos se for o caso).

## Entregáveis

1. **Notebook ou script** (`.ipynb` ou `.py`) com todo o código da análise, organizado nas seções: carregamento, diagnóstico, limpeza, análise e gráficos — nessa ordem, com comentários indicando cada seção.
2. **Relatório executivo** (arquivo `.md` ou `.pdf` separado, no máximo 1-2 páginas) estruturado como um memo real de analista para a diretoria:
   - **Situação**: o que foi analisado e por quê (2-3 frases).
   - **Achados**: resposta objetiva a cada uma das 8 perguntas, com o número/gráfico que sustenta cada resposta.
   - **Recomendação**: a recomendação do item 8, em destaque, com a justificativa de dados por trás.
   - **Limitações**: o que você reconhece que a análise não cobre ou não tem certeza suficiente para afirmar.

## Rubrica de avaliação

Use esta rubrica para se auto-avaliar antes de considerar o projeto pronto
(é assim, de forma similar, que um recrutador avaliaria a entrega):

| Critério | Peso | O que se espera |
|---|---|---|
| Correção técnica | 30% | Merges corretos, sem duplicação indevida de linhas; agregações batem com os dados; sem erros de execução |
| Qualidade da limpeza | 20% | Problemas de dados identificados E tratados com justificativa, não só "rodei `dropna()` em tudo" |
| Profundidade da análise | 20% | Respostas às 8 perguntas vão além do óbvio, cruzando variáveis quando faz sentido |
| Qualidade dos gráficos | 15% | Gráfico certo para cada pergunta (Módulo 7, Tópico 7), títulos e rótulos presentes, sem poluição visual |
| Comunicação do relatório | 15% | Um não-técnico consegue entender a recomendação final e por que ela faz sentido |

## Desafio bônus (opcional, para quem quiser ir além)

Escolha **um** dos desafios abaixo para aprofundar a análise:

- **Segmentação RFM simplificada**: para cada cliente, calcule Recência
  (dias desde a última compra), Frequência (número de pedidos) e Valor
  monetário (soma gasta). Classifique os clientes em 3-4 segmentos (ex:
  "campeões", "em risco", "novos") usando faixas de `pd.cut` nessas três
  métricas, e sugira uma ação de negócio diferente para cada segmento.
- **Retenção por coorte**: agrupe clientes pelo mês da primeira compra
  (a "coorte") e veja quantos deles voltaram a comprar nos meses
  seguintes. Monte uma tabela dinâmica (`pivot_table`) de coorte x mês com
  a taxa de retenção.
- **Amostragem e intervalo de confiança**: escolha uma das métricas do
  relatório (ex: nota média de avaliação) e, usando o que foi visto no
  Módulo 6 (Tópico 7), calcule o intervalo de confiança de 95% para essa
  métrica, discutindo se o tamanho da amostra disponível é suficiente para
  confiar no resultado.

## Checklist de conclusão

- [ ] Segui o brief e respondi às 8 perguntas específicas, nesta ordem, no relatório
- [ ] Cumpri todos os itens da lista de requisitos técnicos obrigatórios
- [ ] Entreguei os dois arquivos: notebook/script E relatório executivo separado
- [ ] Me autoavaliei pela rubrica antes de considerar concluído
- [ ] (Opcional) Resolvi um dos desafios bônus

## E depois?

Terminar este case significa que você tem, na prática, o portfólio de um
analista de dados júnior: um projeto de ponta a ponta, com dataset real,
perguntas de negócio fechadas e comunicação de resultado — exatamente o
tipo de material que vale a pena colocar num GitHub público e citar em
entrevistas. A partir daqui, os próximos passos naturais (fora do escopo
desta apostila) costumam ser: aprofundar SQL para buscar dados direto de
bancos, aprender uma ferramenta de dashboard (Power BI, Tableau, ou
Streamlit em Python), ou seguir para Machine Learning com scikit-learn, que
usa diretamente os DataFrames que você já sabe preparar.

Parabéns por chegar até aqui — o caminho de "sabe o básico de Python" até
"consegue tocar uma análise de dados do início ao fim" não é curto.
