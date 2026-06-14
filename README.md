# Análise e Segmentação de Clientes — Telco Customer Churn

## Resumo

As empresas de telecomunicações lidam com bases de clientes cada vez mais heterogéneas, compostas por pessoas com diferentes níveis de consumo, antiguidade, serviços subscritos e formas de relacionamento contratual. Tratar todos os clientes da mesma forma pode limitar a eficácia das decisões comerciais, uma vez que clientes com perfis diferentes podem exigir estratégias distintas de comunicação, fidelização e acompanhamento.

Este projeto propõe uma abordagem descritiva para compreender melhor essa diversidade através da segmentação de clientes. Recorrendo ao dataset **Telco Customer Churn**, que contém 7043 registos e 21 variáveis relacionadas com informação demográfica, contratual, serviços subscritos e valores pagos, foi desenvolvida uma solução de **clustering não supervisionado** para identificar perfis de clientes com características semelhantes.

Apesar de o dataset incluir a variável `Churn`, esta não foi utilizada como variável-alvo, porque o objetivo do projeto não é prever abandono, mas sim construir conhecimento sobre a estrutura da base de clientes. A metodologia seguida baseia-se no ciclo **CRISP-DM**, passando pelas fases de compreensão do problema, análise exploratória, preparação dos dados, modelação, avaliação e interpretação dos resultados.

O modelo final selecionado foi o **Gaussian Mixture Model com 3 clusters**, obtendo um **Coeficiente de Silhueta de 0,3947**, acima do mínimo de 0,24 definido no objetivo SMART. A solução permitiu identificar três perfis principais: clientes com baixo consumo e menor utilização de serviços, clientes antigos com maior consumo e maior subscrição de serviços, e clientes recentes com encargos mensais elevados. Estes perfis podem apoiar decisões de gestão comercial e relacionamento com clientes, permitindo adaptar estratégias a cada segmento identificado.


## Identificação da Equipa

* **Membros:**

  * Hugo Grou — 2023137127

## Organização do Repositório

A estrutura deste projeto segue as boas práticas de Ciência de Dados e Engenharia de Software:

* **`data/`**: Armazenamento de dados, com referência aos dados brutos em `raw/` e dados tratados/resultados em `processed/`.
* **`docs/`**: Documentação técnica detalhada dividida por Milestones: M1, M2, M3 e M4.
* **`notebooks/`**: Jupyter Notebooks desenvolvidos no Kaggle para iniciação, exploração, limpeza, modelação e avaliação.
* **`src/`**: Código-fonte modular, caso sejam necessárias funções reutilizáveis.
* **`reports/`**: Relatórios, evidências visuais e exportação de figuras na pasta `figures/`.
* **`requirements.txt`**: Ficheiro de configuração com as bibliotecas necessárias para reproduzir o projeto.
* **`Q&A.md`**: Ficheiro de apoio à defesa final, com perguntas frequentes sobre o projeto, metodologia, resultados e limitações.

## 1. Iniciação (Milestone 1)

### Contexto e Problema de Negócio

O projeto utiliza o dataset **Telco Customer Churn**, relativo a clientes de uma empresa de telecomunicações. O conjunto de dados contém informação demográfica, contratual, serviços subscritos, métodos de pagamento e valores pagos pelos clientes.

Embora o dataset inclua a variável `Churn`, este projeto não tem como objetivo construir um modelo supervisionado para prever abandono. A abordagem adotada é **descritiva e não supervisionada**, com foco na **segmentação de clientes**.

O desafio principal consiste em identificar grupos de clientes com características semelhantes, de forma a apoiar decisões de gestão comercial e relacionamento com clientes. Em vez de tratar todos os clientes da mesma forma, pretende-se perceber se existem perfis distintos que possam justificar estratégias diferenciadas.

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

Na Milestone 2 foi realizada a análise exploratória e a preparação dos dados para a fase de modelação. Esta etapa teve como objetivo compreender a estrutura do dataset, identificar problemas de qualidade dos dados e preparar uma versão adequada para a aplicação de algoritmos de clustering.

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
* exclusão da variável `Churn` da modelação, por não existir objetivo supervisionado;
* preparação de um dataset final para clustering.

O dataset processado foi guardado na pasta `data/processed/`.

Mais detalhes estão disponíveis em [`docs/M2_exploracao.md`](docs/M2_exploracao.md).

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

### Gráfico Principal da Exploração

![Matriz de Correlação das Variáveis Numéricas](reports/figures/heatmap_correlacao_variaveis_numericas.png)

A matriz de correlação permitiu observar relações importantes entre as variáveis numéricas do dataset. Destaca-se a correlação forte entre `tenure` e `TotalCharges` (`0,83`), indicando que clientes com maior tempo de permanência tendem a acumular maior valor pago. Também existe uma correlação positiva entre `MonthlyCharges` e `TotalCharges` (`0,65`), mostrando a relevância destas variáveis para distinguir diferentes perfis de clientes.

* **Ponto-chave:** A exploração confirmou que `tenure`, `MonthlyCharges` e `TotalCharges` eram variáveis relevantes para preparar a segmentação não supervisionada.

## 3. Modelação (Milestone 3)

### Abordagem Técnica

Na Milestone 3 foi aplicada uma abordagem de **clustering não supervisionado**, com o objetivo de identificar **3 perfis de clientes** a partir das variáveis preparadas na fase anterior.

A variável `Churn` não foi usada como variável-alvo, uma vez que o projeto não pretende prever abandono, mas sim compreender a estrutura natural da base de clientes.

Foram testados vários algoritmos de agrupamento, incluindo K-Means, MiniBatch K-Means, Agglomerative Clustering, DBSCAN, Bisecting K-Means, BIRCH e Gaussian Mixture Models. A métrica principal usada para avaliar a qualidade dos agrupamentos foi o **Silhouette Score**, complementada pelo Davies-Bouldin Index, Calinski-Harabasz Score e pela análise da dimensão dos clusters.

O modelo baseline foi o **K-Means com 3 clusters**, que obteve uma Silhouette de **0,2161**, ficando abaixo do mínimo de **0,24** definido no objetivo SMART. Por esse motivo, foram testados modelos candidatos e diferentes configurações.

O modelo final escolhido foi um **Gaussian Mixture Model com 3 clusters**, usando a variante de dados `Numericas_Engenharia`. Este modelo obteve uma **Silhouette de 0,3947**, um **Davies-Bouldin Index de 0,9626** e um **Calinski-Harabasz Score de 7142,2309**. A solução final respeita o objetivo SMART, porque identifica exatamente **3 perfis de clientes** e supera o valor mínimo de Silhouette definido inicialmente.

Os três perfis identificados foram interpretados como:

* **Cluster 0:** clientes com baixo consumo e menor utilização de serviços;
* **Cluster 1:** clientes antigos, com maior consumo e maior subscrição de serviços;
* **Cluster 2:** clientes recentes com encargos mensais elevados.

Assim, a modelação permitiu transformar os dados preparados na Milestone 2 em segmentos interpretáveis, capazes de apoiar decisões de gestão comercial e relacionamento com clientes.

Mais detalhes estão disponíveis em [`docs/M3_modelacao.md`](docs/M3_modelacao.md).

## 4. Finalização (Milestone 4)

### Resposta ao Problema

A fase de finalização consolidou os resultados obtidos nas milestones anteriores e transformou os perfis identificados em conclusões práticas.

O modelo final permitiu segmentar os clientes em três grupos interpretáveis:

1. **Clientes com baixo consumo e menor utilização de serviços**;
2. **Clientes antigos, com maior consumo e maior subscrição de serviços**;
3. **Clientes recentes com encargos mensais elevados**.

A resposta ao problema inicial é que a base de clientes não deve ser tratada como um grupo homogéneo. Existem perfis diferentes, com níveis distintos de consumo, permanência e utilização de serviços. Esta segmentação permite apoiar decisões de gestão comercial e relacionamento com clientes, adaptando estratégias de comunicação, fidelização e acompanhamento de acordo com as características de cada segmento.

Em linguagem simples, a métrica técnica principal significa que os dados apresentaram estrutura suficiente para identificar grupos úteis e interpretáveis. O modelo não prevê abandono individual, mas ajuda a perceber **que tipos de clientes existem** e **como podem ser tratados de forma diferenciada**.

### Recomendações de Inovação

1. Testar algoritmos adicionais de clustering, como HDBSCAN, OPTICS e abordagens hierárquicas, para verificar se é possível obter segmentos mais estáveis, interpretáveis e com melhor separação do que a solução atual com Gaussian Mixture Model;

2. Comparar de forma mais aprofundada soluções com 2, 3 e 4 clusters, avaliando o equilíbrio entre Coeficiente de Silhueta, dimensão dos grupos, interpretabilidade dos perfis e utilidade prática para a gestão comercial;

3. Integrar novas variáveis de negócio, como satisfação do cliente, número de reclamações, contactos com o apoio ao cliente, campanhas recebidas e alterações contratuais, para enriquecer a caracterização dos segmentos;

4. Incorporar a dimensão temporal dos clientes, analisando a evolução mensal das mensalidades, serviços subscritos, tempo de permanência e alterações contratuais, de modo a perceber se os clientes mudam de perfil ao longo do tempo;

5. Validar os perfis identificados com equipas de marketing, vendas ou apoio ao cliente, para confirmar se os segmentos fazem sentido do ponto de vista operacional e se as recomendações associadas são aplicáveis;

6. Criar um dashboard em Power BI para apresentar a distribuição dos clusters, as principais características de cada perfil e as recomendações comerciais associadas, facilitando a interpretação por utilizadores não técnicos;

7. Desenvolver uma interface Streamlit que permita carregar novos dados de clientes e atribuir automaticamente cada cliente a um dos perfis identificados, tornando a solução utilizável fora do notebook Kaggle;

8. Explorar, numa fase futura separada, um modelo supervisionado de previsão de churn usando a variável `Churn` como alvo, permitindo comparar a utilidade de uma abordagem descritiva com uma abordagem preditiva.

Mais detalhes estão disponíveis em [`docs/M4_conclusoes.md`](docs/M4_conclusoes.md).

## Como Reproduzir este Projeto

1. Clone o repositório: `git clone https://github.com/HugoGrou/projeto-cdg-hugo-grou.git`
2. Instale as dependências: `pip install -r requirements.txt`
3. Execute os notebooks na pasta `notebooks/` seguindo a ordem numérica.

**Instituição:** Coimbra Business School | ISCAC
**Curso:** Licenciatura em Ciência de Dados para a Gestão
**Unidade Curricular:** Projeto em Ciência de Dados
**Professor Responsável:** Dora Melo
