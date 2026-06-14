# Milestone 1: Iniciação e Definição do Projeto

## 1. Descrição Detalhada do Problema

### Contexto do Setor: Telecomunicações e Gestão de Clientes

O setor das telecomunicações caracteriza-se por uma elevada diversidade de clientes, serviços e modelos contratuais. Numa mesma base de clientes podem coexistir utilizadores com perfis muito distintos: clientes com serviços básicos, clientes com vários serviços contratados, clientes recentes, clientes antigos, clientes com mensalidades reduzidas e clientes com encargos mensais mais elevados.

Esta heterogeneidade torna a gestão comercial mais complexa. Se todos os clientes forem tratados da mesma forma, existe o risco de aplicar estratégias pouco adequadas a determinados grupos. Por exemplo, um cliente com poucos serviços contratados pode necessitar de uma abordagem diferente de um cliente antigo com elevado valor acumulado. Da mesma forma, clientes recentes com mensalidades elevadas podem beneficiar de um acompanhamento inicial mais próximo, de forma a reforçar a perceção de valor dos serviços contratados.

Neste contexto, a Ciência de Dados pode apoiar a gestão de clientes ao permitir identificar padrões escondidos nos dados e transformar informação dispersa em conhecimento útil para a tomada de decisão. Em vez de analisar apenas indicadores isolados, como a mensalidade ou o tipo de contrato, é possível combinar várias dimensões dos clientes e identificar grupos com características semelhantes.

### Relevância do Problema no Contexto Atual

A segmentação de clientes é relevante porque permite compreender melhor a estrutura da base de clientes e apoiar decisões comerciais mais direcionadas. Num contexto empresarial, conhecer os diferentes perfis existentes pode ajudar a adaptar estratégias de comunicação, fidelização, venda cruzada e acompanhamento comercial.

O objetivo deste projeto não é prever individualmente se um cliente irá abandonar a empresa. Embora o dataset utilizado inclua a variável `Churn`, esta não será usada como variável-alvo de classificação. O foco do trabalho é descritivo: pretende-se identificar perfis de clientes e compreender como estes se distinguem entre si com base em variáveis demográficas, contratuais, de serviços subscritos e de consumo.

Esta opção metodológica está alinhada com uma abordagem não supervisionada, em que o objetivo principal não é prever uma classe conhecida, mas sim descobrir estruturas e padrões existentes nos dados.

### Formulação do Problema no Contexto da Ciência de Dados

Para analisar este problema, será utilizado o conjunto de dados **Telco Customer Churn**, disponibilizado na plataforma Kaggle. O dataset contém **7043 registos e 21 variáveis**, representando clientes de uma empresa de telecomunicações. As variáveis disponíveis incluem informação demográfica, características contratuais, serviços subscritos, métodos de pagamento e valores pagos pelos clientes.

O problema será tratado como um problema de **aprendizagem não supervisionada**, mais especificamente de **clustering**. Esta abordagem permite agrupar clientes com características semelhantes, sem utilizar uma variável-alvo. Assim, em vez de construir um modelo preditivo de churn, o projeto procura identificar segmentos de clientes que possam ser descritos estatisticamente e interpretados em contexto de gestão.

A variável `customerID` será considerada apenas como identificador e não deverá contribuir para a modelação. A variável `Churn`, apesar de existir no dataset, será excluída da construção dos clusters, para evitar transformar o projeto num problema supervisionado.

A análise será conduzida de forma progressiva, seguindo a metodologia CRISP-DM: primeiro será feita a compreensão do problema e dos dados; depois a análise exploratória e preparação; em seguida a modelação com algoritmos de clustering; e, por fim, a interpretação dos segmentos encontrados e a tradução dos resultados em valor prático.

### Objetivo Analítico do Projeto

O objetivo analítico principal deste projeto consiste em construir um modelo descritivo de segmentação de clientes, capaz de identificar **3 perfis estatisticamente caracterizáveis** no dataset Telco Customer Churn.

Para atingir esse objetivo, serão analisadas variáveis demográficas, contratuais, de serviços subscritos e de consumo, procurando perceber quais contribuem para diferenciar os clientes. A qualidade da segmentação será avaliada através do **Coeficiente de Silhueta**, com o objetivo mínimo de obter um valor médio igual ou superior a **0,24**.

Além da métrica técnica, o projeto será avaliado pela capacidade de gerar perfis interpretáveis. Cada perfil deverá ser descrito com base em pelo menos cinco variáveis relevantes, permitindo transformar o resultado técnico em conhecimento útil para decisões de gestão comercial e relacionamento com clientes.

Desta forma, o projeto procura demonstrar como técnicas de Ciência de Dados podem ser utilizadas não apenas para previsão, mas também para compreensão, segmentação e apoio à decisão em contexto de negócio.


## 2. Objetivo SMART

Construir, até ao dia **14/06/2026**, um modelo descritivo de segmentação de clientes com base no conjunto de dados **Telco Customer Churn**, utilizando variáveis demográficas, contratuais, de serviços subscritos e de consumo, de modo a identificar **3 perfis de clientes estatisticamente caracterizáveis**, garantindo uma solução final com **Coeficiente de Silhueta médio igual ou superior a 0,24** e com cada perfil descrito através de pelo menos **cinco variáveis relevantes**, permitindo apoiar decisões de gestão comercial e relacionamento com clientes.

### Perguntas de Investigação

1. Quais são as características demográficas, contratuais, de serviços subscritos e de consumo que melhor descrevem a heterogeneidade dos clientes no conjunto de dados **Telco Customer Churn**?

2. Que perfis de clientes podem ser identificados no conjunto de dados e como se caracterizam estatisticamente em termos de antiguidade, mensalidade, valor total pago, tipo de contrato, método de pagamento e serviços subscritos?

3. De que forma os perfis de clientes identificados podem apoiar decisões de gestão comercial e de relacionamento com clientes?

## 3. Metodologia de Gestão (PBL)

A metodologia de gestão do projeto será organizada de acordo com a lógica das *milestones* e com o enquadramento geral da metodologia **CRISP-DM**, sobretudo nas fases iniciais de compreensão do problema e compreensão dos dados.

Nesta primeira fase, o foco está na definição do problema, validação do objetivo SMART, identificação das perguntas de investigação, organização do repositório e inspeção inicial dos dados. As fases seguintes deverão desenvolver a exploração, preparação, modelação e interpretação dos resultados, mantendo sempre o foco no objetivo definido.

* **Ferramentas de colaboração:** O projeto será desenvolvido com recurso ao **GitHub**, permitindo organizar o repositório, controlar versões e registar a evolução do trabalho através de mensagens de *commit* descritivas.

* **Ambiente de desenvolvimento:** A exploração inicial dos dados será realizada no **Kaggle Code**, uma vez que o conjunto de dados está disponível na plataforma Kaggle. O notebook inicial será guardado no repositório GitHub, na pasta `notebooks/`.

* **Documentação:** A documentação será organizada na pasta `docs/`, com ficheiros Markdown correspondentes às diferentes fases do projeto. O ficheiro `M1_iniciacao.md` documenta a definição do problema, o objetivo SMART, as perguntas de investigação, a metodologia, a viabilidade dos dados e o cronograma.

* **Organização do código:** O código será separado por fases. Na *Milestone* 1, o notebook `1.0_iniciacao.ipynb` contém apenas o carregamento do dataset, a visualização inicial, a análise dos tipos de dados, a verificação de valores nulos, a verificação de duplicados, a estatística descritiva e a análise inicial da estrutura do conjunto de dados.

* **Bibliotecas previstas:** As principais bibliotecas previstas para o desenvolvimento do projeto são `pandas`, `numpy`, `matplotlib`, `seaborn` e `scikit-learn`. Outras bibliotecas poderão ser utilizadas se forem necessárias e justificadas nas fases seguintes do projeto.

* **Critério de evolução do trabalho:** Cada decisão tomada nas fases seguintes deverá ser justificada em função do objetivo SMART. Assim, a escolha das variáveis, os tratamentos aplicados, as técnicas de segmentação e a interpretação dos perfis deverão contribuir para a construção de um modelo descritivo coerente e estatisticamente caracterizável.

## 4. Análise de Viabilidade dos Dados

A análise de viabilidade dos dados teve como objetivo confirmar se o conjunto de dados **Telco Customer Churn** é adequado para o desenvolvimento de um modelo descritivo de segmentação de clientes. Nesta fase foram analisadas a disponibilidade dos dados, a sua dimensão, os tipos de variáveis existentes, a qualidade inicial dos registos e a sua adequação ao objetivo SMART definido.

O conjunto de dados encontra-se disponível na plataforma **Kaggle** e foi associado com sucesso a um notebook no **Kaggle Code**. O ficheiro CSV foi carregado sem erros, permitindo realizar a inspeção inicial através da visualização das primeiras linhas, análise da dimensão da tabela, verificação dos tipos de dados, estatísticas descritivas, valores em falta e duplicados.

A inspeção inicial permitiu confirmar que o dataset contém **7043 linhas** e **21 colunas**. Cada linha representa um cliente e cada coluna representa uma característica associada ao cliente, ao contrato, aos serviços subscritos ou aos pagamentos. A coluna `customerID` apresenta **7043 valores únicos**, o que confirma que funciona como identificador técnico de cada cliente.

Relativamente à estrutura das variáveis, o conjunto de dados combina variáveis numéricas e variáveis categóricas. Na leitura inicial, foram identificadas **18 variáveis categóricas**, **2 variáveis inteiras** e **1 variável decimal**. As variáveis `tenure` e `SeniorCitizen` surgem como inteiras, a variável `MonthlyCharges` surge como decimal e a maioria das restantes variáveis surge como categórica. A coluna `TotalCharges`, apesar de representar um valor monetário acumulado, encontra-se inicialmente armazenada como variável categórica, pelo que necessita de tratamento posterior.

A análise estatística inicial das variáveis numéricas mostrou que a variável `tenure`, que representa a antiguidade do cliente em meses, varia entre **0** e **72 meses**, com média aproximada de **32,37 meses** e mediana de **29 meses**. Esta variável poderá ser importante para a segmentação, uma vez que permite distinguir clientes recentes de clientes com uma relação mais prolongada com a empresa.

A variável `MonthlyCharges`, que representa o valor mensal pago pelo cliente, varia entre **18,25** e **118,75**, com média aproximada de **64,76** e mediana de **70,35**. Esta variável é relevante para o objetivo do projeto porque permite diferenciar clientes com níveis distintos de valor mensal associado aos serviços subscritos.

A variável `SeniorCitizen` apresenta apenas os valores **0** e **1**, com média aproximada de **0,16**, indicando que a maioria dos clientes não está identificada como cidadão sénior. Esta variável poderá contribuir para a caracterização demográfica dos perfis, embora a sua relevância final dependa dos padrões encontrados durante a análise exploratória.

Após uma conversão temporária da coluna `TotalCharges` para formato numérico, verificou-se que esta variável apresenta **7032 valores válidos** e **11 valores problemáticos**. Entre os valores válidos, o máximo observado foi **8684,80**, a média foi aproximadamente **2283,30** e a mediana foi aproximadamente **1397,48**. Estes valores confirmam que `TotalCharges` representa um valor monetário acumulado, mas também mostram que esta coluna precisa de tratamento antes de ser utilizada como variável numérica na segmentação.

Não incluo aqui o valor mínimo de `TotalCharges` porque é necessário confirmar esse valor diretamente no output final do notebook, uma vez que versões anteriores do texto tinham valores diferentes. Após confirmação no notebook, esse valor poderá ser acrescentado ao relatório.

A verificação inicial da qualidade dos dados indicou que não existem linhas duplicadas, uma vez que foram identificados **0 registos duplicados**. Também não foram identificados valores nulos diretamente através da verificação inicial de valores em falta. No entanto, a análise da coluna `TotalCharges` revelou que existem **11 registos problemáticos** que não foram detetados como nulos no formato original, uma vez que a coluna estava armazenada como texto. Estes casos deverão ser tratados numa fase posterior de preparação dos dados.

Na análise das variáveis categóricas, verificou-se que várias delas representam informação útil para a segmentação. A variável `Contract` apresenta três categorias, sendo **Month-to-month** a categoria mais frequente, com **3875 clientes**. A existência de diferentes tipos de contrato sugere que podem existir perfis de clientes com níveis distintos de compromisso contratual com a empresa.

A variável `InternetService` também apresenta três categorias, sendo **Fiber optic** a mais frequente, com **3096 clientes**. Esta variável poderá contribuir para distinguir perfis de clientes com diferentes formas de utilização dos serviços digitais.

A variável `PaymentMethod` apresenta quatro categorias, sendo **Electronic check** a mais frequente, com **2365 clientes**. Esta variável pode ser relevante para a caracterização dos perfis, uma vez que reflete diferenças nos hábitos administrativos e na forma como os clientes interagem com a empresa.

A variável `Churn` existe no conjunto de dados e apresenta duas categorias: `No` e `Yes`. Na inspeção inicial, verificou-se que **5174 clientes** estão registados como `No`, correspondendo a aproximadamente **73,46%** do conjunto de dados, e **1869 clientes** estão registados como `Yes`, correspondendo a aproximadamente **26,54%**. Esta variável não será utilizada como variável-alvo de classificação, uma vez que o objetivo validado é construir um modelo descritivo de segmentação de clientes.

Do ponto de vista da adequação ao objetivo SMART, o conjunto de dados é viável para o projeto porque contém variáveis suficientes para caracterizar os clientes em diferentes dimensões: demográfica, contratual, serviços subscritos e consumo. Estas dimensões permitem construir e interpretar perfis de clientes, o que está alinhado com o objetivo de desenvolver um modelo descritivo de segmentação.

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
| `Churn`            | Categórica binária                | Resultado observado | Yes = abandonou, No = permaneceu                                               | Indica se o cliente abandonou ou permaneceu no serviço.                                                                       | Variável presente no conjunto de dados. Não será utilizada como variável-alvo de classificação nem como foco do objetivo principal. |

## 5. Cronograma Interno

| Fase            | Data Limite | Entregável Esperado                                                                                                                                     |
| :-------------- | :---------- | :------------------------------------------------------------------------------------------------------------------------------------------------------ |
| M1: Iniciação   | 14/06/2026  | Repositório estruturado, README inicial, ficheiro `docs/M1_iniciacao.md` preenchido e notebook inicial no Kaggle com carregamento e inspeção dos dados. |
| M2: Exploração  | 14/06/2026  | Notebook de análise exploratória, tratamento inicial dos dados e documentação das principais decisões em `docs/M2_exploracao.md`.                       |
| M3: Modelação   | 14/06/2026  | Construção do modelo descritivo de segmentação, avaliação da solução obtida e caracterização estatística dos perfis de clientes.                        |
| M4: Finalização | 14/06/2026  | Interpretação final dos perfis identificados, resposta ao objetivo SMART, recomendações de gestão comercial e documentação em `docs/M4_conclusoes.md`.  |

## Referências Técnicas

* IBM. **Data Understanding Overview**. Disponível em: https://www.ibm.com/docs/en/spss-modeler/saas?topic=understanding-data-overview

* *scikit-learn*. **Silhouette Score**. Disponível em: https://scikit-learn.org/stable/modules/generated/sklearn.metrics.silhouette_score.html

* *scikit-learn*. **Davies-Bouldin Score**. Disponível em: https://scikit-learn.org/stable/modules/generated/sklearn.metrics.davies_bouldin_score.html

* *kmodes*. **K-Modes and K-Prototypes clustering**. Disponível em: https://pypi.org/project/kmodes/

---

*Data de última atualização: 14/06/2026*
