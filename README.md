# Análise e Segmentação de Clientes para Estudo do Abandono

## Identificação da Equipa

* **Grupo nº:** A preencher

* **Membros:**

  * Hugo Grou (nº de estudante a preencher)

## Organização do Repositório

A estrutura deste projeto segue boas práticas de Ciência de Dados e organização de projetos em *GitHub*.

* **`data/`**: Armazenamento dos dados do projeto.

  * **`data/raw/`**: Local destinado aos dados brutos ou à referência para o conjunto de dados original.

  * **`data/processed/`**: Local destinado aos dados tratados em fases posteriores do projeto.

* **`docs/`**: Documentação técnica do projeto, organizada por *milestones*.

  * **`M1_iniciacao.md`**: Definição do problema, questão SMART, perguntas de investigação, planeamento e análise inicial dos dados.

  * **`M2_exploracao.md`**: Exploração dos dados, preparação e principais conclusões da análise exploratória.

  * **`M3_modelacao.md`**: Aplicação e comparação de técnicas de segmentação não supervisionada.

  * **`M4_conclusoes.md`**: Interpretação final dos resultados, recomendações e limitações do projeto.

* **`notebooks/`**: Ficheiros desenvolvidos no *Kaggle Code* e exportados para o repositório.

* **`src/`**: Código fonte modular, caso seja necessário criar funções reutilizáveis ao longo do projeto.

* **`reports/`**: Pasta destinada a evidências visuais, relatórios finais e materiais de apresentação.

  * **`reports/figures/`**: Gráficos e imagens produzidos durante a análise.

* **`requirements.txt`**: Ficheiro com as bibliotecas necessárias para reproduzir o projeto.

## 1. Iniciação (Milestone 1)

### Contexto e Problema de Negócio

O presente projeto insere-se no tema **Previsão de Abandono de Clientes** (*Churn Prediction*), utilizando o conjunto de dados **Telco Customer Churn**.

O abandono de clientes é um problema relevante para empresas que prestam serviços por subscrição, como empresas de telecomunicações. Quando um cliente cancela o serviço, a empresa perde receita futura e pode ter de investir mais recursos na aquisição de novos clientes.

Neste projeto, o objetivo não é construir um modelo de classificação supervisionada para prever individualmente se um cliente abandona ou não o serviço. Em vez disso, o trabalho será orientado para a análise exploratória e segmentação de clientes, com o objetivo de identificar perfis de clientes associados a maiores taxas de abandono.

A variável `Churn` será utilizada apenas para analisar os segmentos identificados, permitindo calcular a taxa de abandono em cada grupo de clientes. Esta variável não será utilizada como variável alvo para treinar um modelo supervisionado.

### Questão SMART do Projeto

Até ao fim do projeto, em que medida a aplicação e comparação de técnicas de segmentação não supervisionada, nomeadamente *K-Prototypes*, *K-Means* e *Clustering Hierárquico Aglomerativo*, permite identificar entre **3 e 5 perfis distintos de clientes** no conjunto de dados **Telco Customer Churn**, com base em variáveis demográficas, contratuais e de consumo, avaliando a qualidade dos agrupamentos através do *Silhouette Score*, do *Davies-Bouldin Index* e da interpretação estatística dos segmentos, de forma a identificar perfis com taxas de abandono superiores à média global do dataset e apoiar recomendações de retenção direcionadas?

### Perguntas de Investigação

1. Quais são as variáveis demográficas, contratuais e de consumo que apresentam maiores diferenças entre os clientes que abandonaram o serviço e os clientes que permaneceram?

2. Que perfis distintos de clientes podem ser identificados através da aplicação de técnicas de segmentação não supervisionada ao conjunto de dados **Telco Customer Churn**?

3. Qual das técnicas testadas, entre *K-Prototypes*, *K-Means* e *Clustering Hierárquico Aglomerativo*, apresenta a solução de segmentação mais adequada, considerando métricas como *Silhouette Score*, *Davies-Bouldin Index* e a interpretabilidade dos segmentos?

4. Quais são as principais características dos segmentos identificados, considerando variáveis como antiguidade, tipo de contrato, serviços subscritos, método de pagamento, mensalidade e valor total pago?

5. Que segmentos de clientes apresentam taxas de abandono superiores à média global do conjunto de dados e que recomendações de retenção podem ser propostas para esses perfis?

### Fonte de Dados

* **Dataset:** Telco Customer Churn

* **Fonte:** [Telco Customer Churn no Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)

* **Dimensão:** 7043 linhas e 21 colunas

* **Unidade de análise:** Cliente

* **Variável de abandono:** `Churn`

### Inspeção Inicial dos Dados

A inspeção inicial foi realizada no *Kaggle Code*, com o objetivo de compreender a estrutura geral do conjunto de dados **Telco Customer Churn** antes de avançar para fases posteriores de exploração, limpeza e segmentação.

Nesta primeira análise foram observados os seguintes aspetos: dimensão do conjunto de dados, primeiras linhas da tabela, tipos de variáveis, estatísticas descritivas, existência de valores nulos, existência de linhas duplicadas, distribuição da variável `Churn` e verificação inicial da coluna `TotalCharges`.

O conjunto de dados contém **7043 linhas** e **21 colunas**. Cada linha representa um cliente e cada coluna representa uma característica associada ao cliente, ao contrato, aos serviços subscritos, aos pagamentos ou ao estado de abandono.

A análise inicial indicou que não existem linhas duplicadas. Também não foram identificados valores nulos diretamente através da verificação inicial de valores em falta. No entanto, foi identificado um problema na coluna `TotalCharges`: apesar de representar valores monetários, esta coluna encontra-se armazenada como variável categórica. Após uma conversão temporária para formato numérico, foram identificados **11 valores problemáticos**, que deverão ser tratados numa fase posterior de preparação dos dados.

Relativamente à variável `Churn`, verificou-se que **5174 clientes permaneceram** no serviço e **1869 clientes abandonaram**. Isto corresponde a uma distribuição aproximada de **73,46% de clientes sem abandono** e **26,54% de clientes com abandono**. Esta informação será importante nas fases seguintes, não para treinar um modelo de classificação, mas para analisar a taxa de abandono em cada segmento de clientes identificado.

A inspeção inicial também mostrou que o conjunto de dados combina variáveis numéricas e categóricas. As variáveis numéricas principais são `tenure`, `MonthlyCharges` e `TotalCharges`, sendo que `TotalCharges` necessita de tratamento antes de poder ser usada como variável numérica. As restantes variáveis são maioritariamente categóricas e descrevem características demográficas, contratuais, serviços subscritos e métodos de pagamento.

### Dicionário das Variáveis

| Variável           | Tipo Estatístico                  | Domínio             | Classes / Escala Semântica                                                     | Definição Operacional                                                                                                         | Papel Analítico                                                                                                  |
| :----------------- | :-------------------------------- | :------------------ | :----------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------- |
| `customerID`       | Categórica nominal                | Identificador       | Código único por cliente                                                       | Identificador técnico de cada cliente no conjunto de dados.                                                                   | Variável identificadora. Não deverá ser usada na segmentação.                                                    |
| `gender`           | Categórica nominal binária        | Cliente             | Female, Male                                                                   | Género registado do cliente.                                                                                                  | Variável demográfica. Pode ser usada na caracterização dos segmentos.                                            |
| `SeniorCitizen`    | Categórica binária                | Cliente             | 0 = não sénior, 1 = sénior                                                     | Indica se o cliente é considerado cidadão sénior.                                                                             | Variável demográfica. Pode ser usada na segmentação e caracterização dos perfis.                                 |
| `Partner`          | Categórica binária                | Cliente             | Yes, No                                                                        | Indica se o cliente tem parceiro.                                                                                             | Variável demográfica. Pode ser usada na análise dos perfis de clientes.                                          |
| `Dependents`       | Categórica binária                | Cliente             | Yes, No                                                                        | Indica se o cliente tem dependentes.                                                                                          | Variável demográfica. Pode ser usada na análise dos perfis de clientes.                                          |
| `tenure`           | Numérica discreta                 | Contrato            | Número de meses                                                                | Número de meses em que o cliente permaneceu com a empresa.                                                                    | Variável contratual relevante para segmentação e análise de abandono.                                            |
| `PhoneService`     | Categórica binária                | Serviço             | Yes, No                                                                        | Indica se o cliente tem serviço telefónico.                                                                                   | Variável de serviços. Pode ser usada na segmentação.                                                             |
| `MultipleLines`    | Categórica nominal                | Serviço             | Yes, No, No phone service                                                      | Indica se o cliente tem múltiplas linhas telefónicas.                                                                         | Variável de serviços. Pode ajudar a caracterizar padrões de subscrição.                                          |
| `InternetService`  | Categórica nominal                | Serviço             | DSL, Fiber optic, No                                                           | Tipo de serviço de internet contratado pelo cliente.                                                                          | Variável de serviços com possível relevância para segmentação e análise de abandono.                             |
| `OnlineSecurity`   | Categórica nominal                | Serviço             | Yes, No, No internet service                                                   | Indica se o cliente tem serviço de segurança online.                                                                          | Variável de serviços. Pode ajudar a distinguir perfis de subscrição.                                             |
| `OnlineBackup`     | Categórica nominal                | Serviço             | Yes, No, No internet service                                                   | Indica se o cliente tem serviço de cópia de segurança online.                                                                 | Variável de serviços. Pode ser usada na caracterização dos segmentos.                                            |
| `DeviceProtection` | Categórica nominal                | Serviço             | Yes, No, No internet service                                                   | Indica se o cliente tem proteção de dispositivos.                                                                             | Variável de serviços. Pode ajudar a caracterizar os perfis de clientes.                                          |
| `TechSupport`      | Categórica nominal                | Serviço             | Yes, No, No internet service                                                   | Indica se o cliente tem suporte técnico contratado.                                                                           | Variável de serviços com possível relevância na análise de abandono.                                             |
| `StreamingTV`      | Categórica nominal                | Serviço             | Yes, No, No internet service                                                   | Indica se o cliente tem serviço de televisão por *streaming*.                                                                 | Variável de serviços. Pode ser usada na segmentação.                                                             |
| `StreamingMovies`  | Categórica nominal                | Serviço             | Yes, No, No internet service                                                   | Indica se o cliente tem serviço de filmes por *streaming*.                                                                    | Variável de serviços. Pode ser usada na segmentação.                                                             |
| `Contract`         | Categórica ordinal                | Contrato            | Month-to-month, One year, Two year                                             | Tipo de contrato do cliente.                                                                                                  | Variável contratual central para análise de abandono e segmentação.                                              |
| `PaperlessBilling` | Categórica binária                | Faturação           | Yes, No                                                                        | Indica se o cliente utiliza faturação sem papel.                                                                              | Variável contratual ou administrativa. Pode ser usada na caracterização dos perfis.                              |
| `PaymentMethod`    | Categórica nominal                | Pagamento           | Electronic check, Mailed check, Bank transfer automatic, Credit card automatic | Método de pagamento utilizado pelo cliente.                                                                                   | Variável de pagamento relevante para segmentação e análise de perfis.                                            |
| `MonthlyCharges`   | Numérica contínua                 | Pagamento           | Valor monetário mensal                                                         | Valor mensal cobrado ao cliente.                                                                                              | Variável de consumo e pagamento. Pode ser usada na segmentação.                                                  |
| `TotalCharges`     | Numérica contínua após tratamento | Pagamento           | Valor monetário acumulado                                                      | Valor total cobrado ao cliente ao longo do tempo. Inicialmente encontra-se como variável categórica e necessita de conversão. | Variável de consumo e pagamento. Deverá ser tratada antes de ser usada na segmentação.                           |
| `Churn`            | Categórica binária                | Resultado observado | Yes = abandonou, No = permaneceu                                               | Indica se o cliente abandonou ou permaneceu no serviço.                                                                       | Variável de referência para análise posterior dos segmentos. Não será usada como variável-alvo de classificação. |
.

## 2. Exploração (Milestone 2)

### Limpeza e Preparação

Esta fase será desenvolvida na Milestone 2.

Com base na inspeção inicial, prevê-se que seja necessário tratar a coluna `TotalCharges`, uma vez que esta se encontra inicialmente como variável categórica, apesar de representar valores monetários.

Também será necessário preparar as variáveis demográficas, contratuais e de consumo para a análise exploratória e para a futura segmentação de clientes.

Detalhes desta fase serão documentados em **`docs/M2_exploracao.md`**.

### Principais Conclusões da Análise Exploratória

A desenvolver na Milestone 2.

Nesta fase serão analisadas as relações entre variáveis demográficas, contratuais e de consumo com a variável `Churn`, recorrendo a tabelas, estatísticas descritivas e gráficos guardados na pasta **`reports/figures/`**.

## 3. Modelação (Milestone 3)

### Abordagem Técnica

A fase de modelação será orientada para segmentação não supervisionada, e não para classificação supervisionada.

* **Técnicas previstas:** *K-Prototypes*, *K-Means* e *Clustering Hierárquico Aglomerativo*.

* **Métricas previstas:** *Silhouette Score*, *Davies-Bouldin Index* e interpretação estatística dos segmentos.

* **Resultado esperado:** Identificar entre **3 e 5 perfis distintos de clientes** e analisar quais apresentam taxas de abandono superiores à média global do conjunto de dados.

A variável `Churn` será utilizada apenas após a criação dos segmentos, para analisar a taxa de abandono em cada perfil identificado.

Detalhes desta fase serão documentados em **`docs/M3_modelacao.md`**.

## 4. Finalização (Milestone 4)

### Resposta ao Problema

A desenvolver na Milestone 4.

Nesta fase será apresentada a interpretação final dos segmentos identificados, com especial atenção aos perfis de clientes que apresentem maiores taxas de abandono.

### Recomendações de Retenção

A desenvolver na Milestone 4.

As recomendações serão propostas com base nas características dos segmentos de clientes identificados e terão como objetivo apoiar estratégias de retenção direcionadas.

## Como Reproduzir este Projeto

1. Clonar o repositório:

```bash
git clone https://github.com/HugoGrou/projeto-cdg-hugo-grou.git
```

2. Instalar as dependências:

```bash
pip install -r requirements.txt
```

3. Abrir os ficheiros da pasta **`notebooks/`** seguindo a ordem numérica.

4. Consultar a documentação de cada fase na pasta **`docs/`**.

## Informação Institucional

**Instituição:** Coimbra Business School | ISCAC

**Curso:** Licenciatura em Ciência de Dados para a Gestão

**Unidade Curricular:** Projeto em Ciência de Dados

**Professor Responsável:** Dora Melo ([dmelo@iscac.pt](mailto:dmelo@iscac.pt))

---

*Data de última atualização: 01/06/2026*
