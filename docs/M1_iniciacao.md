# Milestone 1: Iniciação e Definição do Projeto

## 1. Descrição Detalhada do Problema

O presente projeto utiliza o conjunto de dados Telco Customer Churn, disponível na plataforma Kaggle. Este conjunto de dados contém informação sobre clientes de uma empresa de telecomunicações, incluindo características demográficas, tipo de contrato, serviços subscritos, método de pagamento, antiguidade do cliente e valores pagos.

Embora o conjunto de dados esteja associado ao tema de abandono de clientes, o objetivo principal deste projeto não é construir um modelo de classificação supervisionada nem prever individualmente se um cliente abandona ou permanece no serviço. O foco do trabalho será a construção de um modelo descritivo de segmentação de clientes, isto é, um modelo de agrupamento que permita identificar perfis de clientes com características semelhantes.

A segmentação de clientes é relevante em contexto de gestão porque permite compreender melhor a composição da base de clientes. Ao identificar grupos com comportamentos, contratos, serviços e padrões de consumo semelhantes, a empresa pode apoiar decisões de gestão comercial, comunicação, acompanhamento e relacionamento com clientes.

Neste projeto, serão consideradas variáveis demográficas, contratuais, de serviços subscritos e de consumo. A variável `Churn` existe no conjunto de dados, mas não constitui o foco principal do projeto e não será utilizada como variável-alvo de classificação.

## 2. Objetivo SMART

Construir, até ao dia 14/06/2026, um modelo descritivo de segmentação de clientes com base no conjunto de dados Telco Customer Churn, utilizando variáveis demográficas, contratuais, de serviços subscritos e de consumo, de modo a identificar 3 perfis de clientes estatisticamente caracterizáveis, garantindo uma solução final com Coeficiente de Silhueta médio igual ou superior a 0,24 e com cada perfil descrito através de pelo menos cinco variáveis relevantes, permitindo apoiar decisões de gestão comercial e relacionamento com clientes.

### Critérios SMART

* **Específico:** O objetivo centra-se na construção de um modelo descritivo de segmentação de clientes, utilizando o conjunto de dados Telco Customer Churn.

* **Mensurável:** O objetivo define como resultado esperado a identificação de 3 perfis de clientes, uma solução com Coeficiente de Silhueta médio igual ou superior a 0,24 e a descrição de cada perfil através de pelo menos cinco variáveis relevantes.

* **Atingível:** O conjunto de dados contém variáveis demográficas, contratuais, de serviços subscritos e de consumo suficientes para desenvolver uma análise de segmentação.

* **Relevante:** A identificação de perfis de clientes pode apoiar decisões de gestão comercial e relacionamento com clientes.

* **Temporal:** O objetivo deverá ser concretizado até ao dia 14/06/2026.

### Perguntas de Investigação

1. Quais são as características demográficas, contratuais, de serviços subscritos e de consumo que melhor descrevem a heterogeneidade dos clientes no conjunto de dados Telco Customer Churn?

2. Que perfis de clientes podem ser identificados no conjunto de dados e como se caracterizam estatisticamente em termos de antiguidade, mensalidade, valor total pago, tipo de contrato, método de pagamento e serviços subscritos?

3. De que forma os perfis de clientes identificados podem apoiar decisões de gestão comercial e de relacionamento com clientes?

## 3. Metodologia de Gestão (PBL)

* **Ferramentas de colaboração:** O projeto será desenvolvido com recurso ao GitHub, permitindo organizar o repositório, controlar versões e registar a evolução do trabalho através de mensagens de commit descritivas.

* **Ambiente de desenvolvimento:** A exploração inicial dos dados será realizada no Kaggle Code, uma vez que o conjunto de dados está disponível na plataforma Kaggle. O notebook inicial será guardado no repositório GitHub, na pasta `notebooks/`.

* **Documentação:** A documentação será organizada na pasta `docs/`, com ficheiros Markdown correspondentes às diferentes fases do projeto. O ficheiro `M1_iniciacao.md` documenta a definição do problema, o objetivo SMART, as perguntas de investigação, a metodologia, a viabilidade dos dados e o cronograma.

* **Organização do código:** O código será separado por fases. Na Milestone 1, o notebook `1.0_iniciacao.ipynb` contém apenas o carregamento do dataset, a visualização inicial, a análise dos tipos de dados, a verificação de valores nulos, a verificação de duplicados, a estatística descritiva e a análise inicial da estrutura do conjunto de dados.

* **Bibliotecas previstas:** As principais bibliotecas previstas para o desenvolvimento do projeto são `pandas`, `numpy`, `matplotlib`, `seaborn` e `scikit-learn`. Outras bibliotecas poderão ser utilizadas se forem necessárias e justificadas nas fases seguintes do projeto.

## 4. Análise de Viabilidade dos Dados

A análise de viabilidade dos dados teve como objetivo confirmar se o conjunto de dados Telco Customer Churn é adequado para o desenvolvimento de um modelo descritivo de segmentação de clientes. Nesta fase foram analisadas a disponibilidade dos dados, a sua dimensão, os tipos de variáveis existentes, a qualidade inicial dos registos e a sua adequação ao objetivo SMART definido.

O conjunto de dados encontra-se disponível na plataforma Kaggle e foi associado com sucesso a um notebook no Kaggle Code. O ficheiro CSV foi carregado sem erros, permitindo realizar a inspeção inicial através da visualização das primeiras linhas, análise da dimensão da tabela, verificação dos tipos de dados, estatísticas descritivas, valores em falta e duplicados.

A inspeção inicial permitiu confirmar que o dataset contém 7043 linhas e 21 colunas. Cada linha representa um cliente e cada coluna representa uma característica associada ao cliente, ao contrato, aos serviços subscritos ou aos pagamentos. A coluna `customerID` apresenta 7043 valores únicos, o que confirma que funciona como identificador técnico de cada cliente.

Relativamente à estrutura das variáveis, o conjunto de dados combina variáveis numéricas e variáveis categóricas. Na leitura inicial, foram identificadas 18 variáveis categóricas, 2 variáveis inteiras e 1 variável decimal. As variáveis `tenure` e `SeniorCitizen` surgem como inteiras, a variável `MonthlyCharges` surge como decimal e a maioria das restantes variáveis surge como categórica. A coluna `TotalCharges`, apesar de representar um valor monetário acumulado, encontra-se inicialmente armazenada como variável categórica, pelo que necessita de tratamento posterior.

A análise estatística inicial das variáveis numéricas mostrou que a variável `tenure`, que representa a antiguidade do cliente em meses, varia entre 0 e 72 meses, com média aproximada de 32,37 meses e mediana de 29 meses. A variável `MonthlyCharges`, que representa o valor mensal pago pelo cliente, varia entre 18,25 e 118,75, com média aproximada de 64,76 e mediana de 70,35. A variável `SeniorCitizen` apresenta apenas os valores 0 e 1, com média aproximada de 0,16, indicando que a maioria dos clientes não está identificada como cidadão sénior.

Após uma conversão temporária da coluna `TotalCharges` para formato numérico, verificou-se que esta variável apresenta 7032 valores válidos e 11 valores problemáticos. Entre os valores válidos, o mínimo observado foi 8,80, o máximo foi 8684,80, a média foi aproximadamente 2283,30 e a mediana foi aproximadamente 1397,48. Estes valores confirmam que `TotalCharges` representa um valor monetário acumulado, mas também mostram que esta coluna precisa de tratamento antes de ser utilizada como variável numérica na segmentação.

A verificação inicial da qualidade dos dados indicou que não existem linhas duplicadas, uma vez que foram identificados 0 registos duplicados. Também não foram identificados valores nulos diretamente através da verificação inicial de valores em falta. No entanto, a análise da coluna `TotalCharges` revelou que existem 11 registos problemáticos que não foram detetados como nulos no formato original, uma vez que a coluna estava armazenada como texto. Estes casos deverão ser tratados numa fase posterior de preparação dos dados.

Na análise das variáveis categóricas, verificou-se que várias delas representam informação útil para a segmentação. A variável `Contract` apresenta três categorias, sendo Month-to-month a categoria mais frequente, com 3875 clientes. A variável `InternetService` também apresenta três categorias, sendo Fiber optic a mais frequente, com 3096 clientes. A variável `PaymentMethod` apresenta quatro categorias, sendo Electronic check a mais frequente, com 2365 clientes. Estes resultados mostram que o dataset contém informação contratual, de serviços subscritos e de pagamentos que pode contribuir para a construção de perfis de clientes.

A variável `Churn` existe no conjunto de dados e apresenta duas categorias: `No` e `Yes`. Na inspeção inicial, verificou-se que 5174 clientes estão registados como `No`, correspondendo a aproximadamente 73,46% do conjunto de dados, e 1869 clientes estão registados como `Yes`, correspondendo a aproximadamente 26,54%. Esta variável não será utilizada como variável-alvo de classificação, uma vez que o objetivo validado é construir um modelo descritivo de segmentação de clientes.

Do ponto de vista da adequação ao objetivo SMART, o conjunto de dados é viável para o projeto, porque contém variáveis suficientes para caracterizar os clientes em diferentes dimensões: demográfica, contratual, serviços subscritos e consumo. Estas dimensões permitem construir e interpretar perfis de clientes, o que está alinhado com o objetivo de desenvolver um modelo descritivo de segmentação.

Do ponto de vista ético, o dataset não contém nomes reais, moradas, contactos diretos ou informação pessoal identificável dos clientes. A coluna `customerID` funciona apenas como identificador técnico. Ainda assim, os dados serão utilizados apenas para fins académicos e analisados de forma agregada, sem tentativa de identificação individual dos clientes.


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


## 5. Cronograma Interno

| Fase | Data Limite | Entregável Esperado |
| :--- | :--- | :--- |
| M1: Iniciação | 14/06/2026 | Repositório estruturado, README inicial, ficheiro `docs/M1_iniciacao.md` preenchido e notebook inicial no Kaggle com carregamento e inspeção dos dados. |
| M2: Exploração | 14/06/2026 | Notebook de análise exploratória, tratamento inicial dos dados e documentação das principais decisões em `docs/M2_exploracao.md`. |
| M3: Modelação | 14/06/2026 | Construção do modelo descritivo de segmentação, avaliação da solução obtida e caracterização estatística dos perfis de clientes. |
| M4: Finalização | 14/06/2026 | Interpretação final dos perfis identificados, resposta ao objetivo SMART, recomendações de gestão comercial e documentação em `docs/M4_conclusoes.md`. |

---

*Data de última atualização: 02/06/2026*
---

*Data de última atualização: 02/06/2026*
