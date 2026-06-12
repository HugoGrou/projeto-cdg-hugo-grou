# Análise e Segmentação de Clientes — Telco Customer Churn

## Identificação da Equipa

* **Grupo nº:** por preencher
* **Membros:**

  * Hugo Grou - nº de estudante por preencher

## Organização do Repositório

A estrutura deste projeto segue as boas práticas de Ciência de Dados e Engenharia de Software:

* **`data/`**: Armazenamento de dados, com dados brutos ou referência ao dataset original em `raw/` e dados tratados/resultados em `processed/`.
* **`docs/`**: Documentação técnica detalhada dividida por Milestones: M1, M2, M3 e M4.
* **`notebooks/`**: Jupyter Notebooks desenvolvidos no Kaggle para iniciação, exploração, limpeza, modelação e avaliação.
* **`src/`**: Código-fonte modular, caso sejam necessárias funções reutilizáveis.
* **`reports/`**: Relatórios, evidências visuais e exportação de figuras na pasta `figures/`.
* **`requirements.txt`**: Ficheiro de configuração com as bibliotecas necessárias para reproduzir o projeto.

## 1. Iniciação (Milestone 1)

### Contexto e Problema de Negócio

O projeto utiliza o dataset **Telco Customer Churn**, relativo a clientes de uma empresa de telecomunicações. O conjunto de dados contém informação demográfica, contratual, serviços subscritos, métodos de pagamento e valores pagos pelos clientes.

Embora o dataset inclua a variável `Churn`, este projeto não tem como objetivo construir um modelo supervisionado para prever abandono. Por indicação metodológica do trabalho, a abordagem adotada é **descritiva e não supervisionada**, com foco na **segmentação de clientes**.

O desafio principal consiste em identificar grupos de clientes com características semelhantes, de forma a apoiar decisões de gestão comercial e relacionamento com clientes.

### Objetivos do Projeto

* **Objetivo SMART:** Construir, até ao dia **14/06/2026**, um modelo descritivo de segmentação de clientes com base no conjunto de dados Telco Customer Churn, utilizando variáveis demográficas, contratuais, de serviços subscritos e de consumo, de modo a identificar **3 perfis de clientes estatisticamente caracterizáveis**, garantindo uma solução final com **Coeficiente de Silhueta médio igual ou superior a 0,24** e com cada perfil descrito através de pelo menos cinco variáveis relevantes, permitindo apoiar decisões de gestão comercial e relacionamento com clientes.

* **Questões de investigação:**

  1. Quais são as características demográficas, contratuais, de serviços subscritos e de consumo que melhor descrevem a heterogeneidade dos clientes?
  2. Que perfis de clientes podem ser identificados e como se caracterizam estatisticamente?
  3. De que forma os perfis identificados podem apoiar decisões de gestão comercial e relacionamento com clientes?

### Fonte de Dados

* **Dataset:** Telco Customer Churn
* **Fonte:** Kaggle — Telco Customer Churn
* **Dimensão inicial:** 7043 linhas e 21 colunas
* **Unidade de análise:** Cliente
* **Observação metodológica:** A variável `Churn` foi analisada de forma contextual, mas não foi usada como variável-alvo de classificação.

## 2. Exploração (Milestone 2)

### Limpeza e Preparação

Na Milestone 2 foi realizada a análise exploratória e a preparação dos dados para a fase de modelação.

As principais tarefas realizadas foram:

* análise estatística das variáveis numéricas;
* análise de frequência das variáveis categóricas;
* verificação de duplicados;
* identificação e tratamento de valores problemáticos;
* conversão da variável `TotalCharges` para formato numérico;
* tratamento dos valores problemáticos associados a `TotalCharges`;
* criação de novas variáveis relevantes para a segmentação;
* transformação de variáveis categóricas;
* escalonamento das variáveis numéricas;
* remoção de variáveis não adequadas para modelação, como `customerID`;
* preparação de um dataset final para clustering.

O dataset processado foi guardado na pasta `data/processed/`.

Mais detalhes estão disponíveis em `docs/M2_exploracao.md`.

### Principais Conclusões (EDA)

A análise exploratória permitiu identificar diferenças relevantes entre clientes ao nível de:

* antiguidade do cliente (`tenure`);
* mensalidade (`MonthlyCharges`);
* valor total pago (`TotalCharges`);
* tipo de contrato;
* método de pagamento;
* número de serviços subscritos;
* existência ou não de serviço de Internet.

Estas variáveis foram consideradas importantes para a construção dos perfis de clientes, uma vez que ajudam a distinguir clientes com diferentes níveis de consumo, permanência e envolvimento com os serviços da empresa.

* **Ponto-chave:** A preparação dos dados confirmou que existiam variáveis suficientes para avançar para uma abordagem de segmentação não supervisionada, desde que a variável `Churn` fosse excluída da modelação.

## 3. Modelação (Milestone 3)

### Abordagem Técnica

* **Modelos:** K-Means, MiniBatch K-Means, Agglomerative Clustering, DBSCAN, Bisecting K-Means, BIRCH e Gaussian Mixture Models.
* **Métrica Principal:** Silhouette Score.

Na Milestone 3 foi adotada uma abordagem de **clustering não supervisionado**, com o objetivo de identificar **3 perfis de clientes**.

A variável `Churn` não foi usada como variável-alvo. O foco foi avaliar a estrutura natural dos dados e identificar grupos de clientes com características semelhantes.

As principais métricas usadas foram:

* **Silhouette Score**, para avaliar a coesão e separação dos clusters;
* **Davies-Bouldin Index**, para avaliar a separação entre grupos;
* **Calinski-Harabasz Score**, para avaliar a estrutura dos agrupamentos;
* **Inércia**, sobretudo para o K-Means;
* **Percentagem mínima por cluster**, para evitar clusters residuais.

#### Baseline

O modelo baseline foi o **K-Means com 3 clusters**.

Resultado principal no dataset completo:

| Modelo           | Nº de clusters | Silhouette | Davies-Bouldin |
| :--------------- | -------------: | ---------: | -------------: |
| K-Means Baseline |              3 |     0,2161 |         1,6154 |

Este resultado ficou abaixo do valor mínimo definido no objetivo SMART, que era **0,24**.

#### Otimização e Modelo Final

Depois do baseline, foram testados vários modelos candidatos e diferentes representações dos dados.

O melhor modelo global encontrado foi um **GaussianMixture com 2 clusters**, com Silhouette de **0,4377**. No entanto, este modelo não foi escolhido como solução final porque o objetivo SMART define a identificação de **3 perfis de clientes**.

O modelo final selecionado foi:

| Elemento          | Valor                |
| :---------------- | :------------------- |
| Modelo            | GaussianMixture      |
| Variante de dados | Numericas_Engenharia |
| Nº de clusters    | 3                    |
| covariance_type   | spherical            |
| n_init            | 5                    |
| random_state      | 42                   |
| Silhouette        | 0,3947               |
| Davies-Bouldin    | 0,9626               |
| Calinski-Harabasz | 7142,2309            |
| Cluster mínimo    | 29,62%               |

Este modelo cumpre o objetivo SMART, uma vez que:

* identifica exatamente **3 perfis de clientes**;
* apresenta Silhouette superior a **0,24**;
* produz clusters com dimensão equilibrada;
* permite caracterizar cada perfil através de várias variáveis relevantes;
* melhora substancialmente o desempenho face ao K-Means baseline.

#### Perfis identificados

| Cluster | Nº de clientes | Percentagem | Interpretação                                                      |
| ------: | -------------: | ----------: | :----------------------------------------------------------------- |
|       0 |           2086 |      29,62% | Clientes com baixo consumo e menor utilização de serviços          |
|       1 |           2298 |      32,63% | Clientes antigos, com maior consumo e maior subscrição de serviços |
|       2 |           2659 |      37,75% | Clientes recentes com encargos mensais elevados                    |

#### Figuras principais da modelação

As principais figuras da Milestone 3 encontram-se em `reports/figures/`, incluindo:

* Método do Cotovelo;
* Silhouette Plot do modelo final;
* visualização PCA do modelo final;
* gráfico de perfil dos segmentos;
* gráfico de estabilidade do modelo final;
* gráfico da Silhouette média por cluster.

Mais detalhes estão disponíveis em `docs/M3_modelacao.md`.

## 4. Finalização (Milestone 4)

### Resposta ao Problema

A fase de finalização deverá consolidar os resultados obtidos nas milestones anteriores e transformar os perfis identificados em recomendações práticas.

O modelo final permitiu segmentar os clientes em três grupos interpretáveis:

1. clientes com baixo consumo e menor utilização de serviços;
2. clientes antigos, com maior consumo e maior subscrição de serviços;
3. clientes recentes com encargos mensais elevados.

Estes perfis podem apoiar decisões de gestão comercial e relacionamento com clientes, permitindo adaptar estratégias de comunicação, fidelização e acompanhamento de acordo com as características de cada segmento.

### Recomendações de Inovação

1. Criar estratégias diferenciadas de comunicação para cada perfil de cliente identificado.
2. Desenvolver ações de fidelização específicas para clientes antigos e de maior valor comercial.
3. Acompanhar de forma mais próxima clientes recentes com encargos mensais elevados.
4. Explorar oportunidades de venda cruzada para clientes com baixo número de serviços subscritos.
5. Usar os segmentos como base para análises futuras, sem interpretar o modelo como previsão direta de churn.

## Como Reproduzir este Projeto

1. Clone o repositório:

```bash
git clone https://github.com/HugoGrou/projeto-cdg-hugo-grou.git
```

2. Instale as dependências:

```bash
pip install -r requirements.txt
```

3. Execute os notebooks na pasta `notebooks/` seguindo a ordem numérica:

```text
1.0_iniciacao.ipynb
2.0_exploracao.ipynb
3.0_modelacao.ipynb
```

4. Consulte a documentação técnica na pasta `docs/`:

```text
docs/M1_iniciacao.md
docs/M2_exploracao.md
docs/M3_modelacao.md
docs/M4_conclusoes.md
```

**Instituição:** Coimbra Business School | ISCAC
**Curso:** Licenciatura em Ciência de Dados para a Gestão
**Unidade Curricular:** Projeto em Ciência de Dados
**Professor Responsável:** Dora Melo
