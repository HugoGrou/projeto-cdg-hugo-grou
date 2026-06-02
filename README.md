# Análise e Segmentação de Clientes

## Identificação da Equipa

* Hugo Grou (nº 2023137127)

## Organização do Repositório

A estrutura deste projeto segue boas práticas de Ciência de Dados e organização de projetos em *GitHub*.

* **`data/`**: Armazenamento dos dados do projeto.

  * **`data/raw/`**: Local destinado aos dados brutos ou à referência para o conjunto de dados original.

  * **`data/processed/`**: Local destinado aos dados tratados em fases posteriores do projeto.

* **`docs/`**: Documentação técnica do projeto, organizada por *milestones*.

  * **`M1_iniciacao.md`**: Definição do problema, objetivo SMART, perguntas de investigação, planeamento e análise inicial dos dados.

  * **`M2_exploracao.md`**: Exploração dos dados, preparação e principais conclusões da análise exploratória.

  * **`M3_modelacao.md`**: Construção, avaliação e interpretação do modelo descritivo de segmentação.

  * **`M4_conclusoes.md`**: Interpretação final dos resultados, resposta ao objetivo SMART, recomendações e limitações do projeto.

* **`notebooks/`**: Ficheiros desenvolvidos no *Kaggle Code* e exportados para o repositório.

* **`src/`**: Código fonte modular, caso seja necessário criar funções reutilizáveis ao longo do projeto.

* **`reports/`**: Pasta destinada a evidências visuais, relatórios finais e materiais de apresentação.

  * **`reports/figures/`**: Gráficos e imagens produzidos durante a análise.

* **`requirements.txt`**: Ficheiro com as bibliotecas necessárias para reproduzir o projeto.

## 1. Iniciação (*Milestone* 1)

### Contexto e Problema de Negócio

O presente projeto utiliza o conjunto de dados **Telco Customer Churn**, associado a clientes de uma empresa de telecomunicações.

Apesar de o conjunto de dados incluir uma variável que identifica o abandono do serviço, o foco principal deste projeto não é construir um modelo de classificação nem prever individualmente se um cliente abandona ou permanece. O trabalho será orientado para a construção de um **modelo descritivo de segmentação de clientes**, com o objetivo de identificar grupos de clientes com características semelhantes.

A segmentação de clientes é relevante para a gestão comercial, pois permite compreender melhor a composição da base de clientes, identificar perfis com características distintas e apoiar decisões relacionadas com comunicação, oferta de serviços, acompanhamento comercial e relacionamento com clientes.

### Objetivo SMART

Construir, até ao dia **23/04/2026**, um modelo descritivo de segmentação de clientes com base no conjunto de dados **Telco Customer Churn**, utilizando variáveis demográficas, contratuais, de serviços subscritos e de consumo, de modo a identificar **3 perfis de clientes estatisticamente caracterizáveis**, garantindo uma solução final com **Coeficiente de Silhueta médio igual ou superior a 0,24** e com cada perfil descrito através de pelo menos **cinco variáveis relevantes**, permitindo apoiar decisões de gestão comercial e relacionamento com clientes.

### Perguntas de Investigação

1. Quais são as características demográficas, contratuais, de serviços subscritos e de consumo que melhor descrevem a heterogeneidade dos clientes no conjunto de dados **Telco Customer Churn**?

2. Que perfis de clientes podem ser identificados no conjunto de dados e como se caracterizam estatisticamente em termos de antiguidade, mensalidade, valor total pago, tipo de contrato, método de pagamento e serviços subscritos?

3. De que forma os perfis de clientes identificados podem apoiar decisões de gestão comercial e de relacionamento com clientes?

### Fonte de Dados

* **Conjunto de dados:** Telco Customer Churn

* **Fonte:** [Telco Customer Churn no Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)

* **Dimensão:** 7043 linhas e 21 colunas

* **Unidade de análise:** Cliente

### Inspeção Inicial dos Dados

A inspeção inicial foi realizada no *Kaggle Code*, com o objetivo de compreender a estrutura geral do conjunto de dados **Telco Customer Churn** antes de avançar para fases posteriores de exploração, preparação e segmentação.

Nesta primeira análise foram observados os seguintes aspetos:

* dimensão do conjunto de dados;

* primeiras linhas da tabela;

* tipos de variáveis;

* estatísticas descritivas;

* existência de valores nulos;

* existência de linhas duplicadas;

* distribuição das principais variáveis;

* verificação inicial da coluna `TotalCharges`.

O conjunto de dados contém **7043 linhas** e **21 colunas**. Cada linha representa um cliente e cada coluna representa uma característica associada ao cliente, ao contrato, aos serviços subscritos ou aos pagamentos.

A análise inicial indicou que não existem linhas duplicadas. Também não foram identificados valores nulos diretamente através da verificação inicial de valores em falta. No entanto, foi identificado um problema na coluna `TotalCharges`: apesar de representar valores monetários, esta coluna encontra-se armazenada como variável categórica. Após uma conversão temporária para formato numérico, foram identificados **11 valores problemáticos**, que deverão ser tratados numa fase posterior de preparação dos dados.

A inspeção inicial mostrou ainda que o conjunto de dados combina variáveis numéricas e categóricas. As variáveis numéricas principais são `tenure`, `MonthlyCharges` e `TotalCharges`, sendo que `TotalCharges` necessita de tratamento antes de poder ser utilizada como variável numérica. As restantes variáveis são maioritariamente categóricas e descrevem características demográficas, contratuais, serviços subscritos e métodos de pagamento.

### Dicionário das Variáveis

| Variável           | Tipo Estatístico                  | Domínio             | Classes / Escala Semântica                                                     | Definição Operacional                                                                                                         | Papel Analítico                                                                                                                     |
| :----------------- | :-------------------------------- | :------------------ | :----------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------- |
| `customerID`       | Categórica nominal                | Identificador       | Código único por cliente                                                       | Identificador técnico de cada cliente no conjunto de dados.                                                                   | Variável identificadora. Não deverá ser usada na segmentação.                                                                       |
| `gender`           | Categórica nominal binária        | Cliente             | Female, Male                                                                   | Género registado do cliente.                                                                                                  | Variável demográfica. Pode ser usada na caracterização dos perfis.                                                                  |
| `SeniorCitizen`    | Categórica binária                | Cliente             | 0 = não sénior, 1 = sénior                                                     | Indica se o cliente é considerado cidadão sénior.                                                                             | Variável demográfica. Pode ser usada na segmentação e caracterização dos perfis.                                                    |
| `Partner`          | Categórica binária                | Cliente             | Yes, No                                                                        | Indica se o cliente tem parceiro.                                                                                             | Variável demográfica. Pode ser usada na análise dos perfis de clientes.                                                             |
| `Dependents`       | Categórica binária                | Cliente             | Yes, No                                                                        | Indica se o cliente tem dependentes.                                                                                          | Variável demográfica. Pode ser usada na análise dos perfis de clientes.                                                             |
| `tenure`           | Numérica discreta                 | Contrato            | Número de meses                                                                | Número de meses em que o cliente permaneceu com a empresa.                                                                    | Variável contratual relevante para a segmentação.                                                                                   |
| `PhoneService`     | Categórica binária                | Serviço             | Yes, No                                                                        | Indica se o cliente tem serviço telefónico.                                                                                   | Variável de serviços. Pode ser usada na segmentação.                                                                                |
| `MultipleLines`    | Categórica nominal                | Serviço             | Yes, No, No phone service                                                      | Indica se o cliente tem múltiplas linhas telefónicas.                                                                         | Variável de serviços. Pode ajudar a caracterizar padrões de subscrição.                                                             |
| `InternetService`  | Categórica nominal                | Serviço             | DSL, Fiber optic, No                                                           | Tipo de serviço de internet contratado pelo cliente.                                                                          | Variável de serviços. Pode ser usada na segmentação e caracterização dos perfis.                                                    |
| `OnlineSecurity`   | Categórica nominal                | Serviço             | Yes, No, No internet service                                                   | Indica se o cliente tem serviço de segurança online.                                                                          | Variável de serviços. Pode ajudar a distinguir perfis de subscrição.                                                                |
| `OnlineBackup`     | Categórica nominal                | Serviço             | Yes, No, No internet service                                                   | Indica se o cliente tem serviço de cópia de segurança online.                                                                 | Variável de serviços. Pode ser usada na caracterização dos perfis.                                                                  |
| `DeviceProtection` | Categórica nominal                | Serviço             | Yes, No, No internet service                                                   | Indica se o cliente tem proteção de dispositivos.                                                                             | Variável de serviços. Pode ajudar a caracterizar os perfis de clientes.                                                             |
| `TechSupport`      | Categórica nominal                | Serviço             | Yes, No, No internet service                                                   | Indica se o cliente tem suporte técnico contratado.                                                                           | Variável de serviços. Pode ser usada na caracterização dos perfis.                                                                  |
| `StreamingTV`      | Categórica nominal                | Serviço             | Yes, No, No internet service                                                   | Indica se o cliente tem serviço de televisão por *streaming*.                                                                 | Variável de serviços. Pode ser usada na segmentação.                                                                                |
| `StreamingMovies`  | Categórica nominal                | Serviço             | Yes, No, No internet service                                                   | Indica se o cliente tem serviço de filmes por *streaming*.                                                                    | Variável de serviços. Pode ser usada na segmentação.                                                                                |
| `Contract`         | Categórica ordinal                | Contrato            | Month-to-month, One year, Two year                                             | Tipo de contrato do cliente.                                                                                                  | Variável contratual central para a caracterização dos perfis.                                                                       |
| `PaperlessBilling` | Categórica binária                | Faturação           | Yes, No                                                                        | Indica se o cliente utiliza faturação sem papel.                                                                              | Variável contratual ou administrativa. Pode ser usada na caracterização dos perfis.                                                 |
| `PaymentMethod`    | Categórica nominal                | Pagamento           | Electronic check, Mailed check, Bank transfer automatic, Credit card automatic | Método de pagamento utilizado pelo cliente.                                                                                   | Variável de pagamento relevante para segmentação e análise de perfis.                                                               |
| `MonthlyCharges`   | Numérica contínua                 | Pagamento           | Valor monetário mensal                                                         | Valor mensal cobrado ao cliente.                                                                                              | Variável de consumo e pagamento. Pode ser usada na segmentação.                                                                     |
| `TotalCharges`     | Numérica contínua após tratamento | Pagamento           | Valor monetário acumulado                                                      | Valor total cobrado ao cliente ao longo do tempo. Inicialmente encontra-se como variável categórica e necessita de conversão. | Variável de consumo e pagamento. Deverá ser tratada antes de ser usada na segmentação.                                              |
| `Churn`            | Categórica binária                | Resultado observado | Yes = abandonou, No = permaneceu                                               | Indica se o cliente abandonou ou permaneceu no serviço.                                                                       | Variável presente no conjunto de dados. Não será utilizada como variável alvo de classificação nem como foco do objetivo principal. |

## 2. Exploração (*Milestone* 2)

### Limpeza e Preparação

Esta fase será desenvolvida na *Milestone* 2.

Com base na inspeção inicial, prevê-se que seja necessário tratar a coluna `TotalCharges`, uma vez que esta se encontra inicialmente como variável categórica, apesar de representar valores monetários.

Também será necessário preparar as variáveis demográficas, contratuais, de serviços subscritos e de consumo para a análise exploratória e para a futura segmentação de clientes.

Detalhes desta fase serão documentados em **`docs/M2_exploracao.md`**.

### Principais Conclusões da Análise Exploratória

A desenvolver na *Milestone* 2.

Nesta fase serão analisadas as variáveis demográficas, contratuais, de serviços subscritos e de consumo, recorrendo a tabelas, estatísticas descritivas e gráficos guardados na pasta **`reports/figures/`**.

## 3. Modelação (*Milestone* 3)

### Abordagem Técnica

A fase de modelação será orientada para a construção de um modelo descritivo de segmentação de clientes.

O desenvolvimento técnico incluirá a preparação das variáveis, a aplicação de técnicas de agrupamento, a avaliação da qualidade da solução obtida e a caracterização estatística dos perfis identificados.

A solução final deverá permitir identificar **3 perfis de clientes estatisticamente caracterizáveis**, apresentar um **Coeficiente de Silhueta médio igual ou superior a 0,24** e descrever cada perfil através de pelo menos **cinco variáveis relevantes**.

Detalhes desta fase serão documentados em **`docs/M3_modelacao.md`**.

## 4. Finalização (*Milestone* 4)

### Resposta ao Problema

A desenvolver na *Milestone* 4.

Nesta fase será apresentada a interpretação final dos perfis de clientes identificados e a resposta ao objetivo SMART definido para o projeto.

### Recomendações de Gestão Comercial

A desenvolver na *Milestone* 4.

As recomendações serão propostas com base nas características dos perfis de clientes identificados e terão como objetivo apoiar decisões de gestão comercial e relacionamento com clientes.

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
