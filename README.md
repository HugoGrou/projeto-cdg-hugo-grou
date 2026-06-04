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

Embora o conjunto de dados inclua uma variável que identifica o abandono do serviço, o objetivo principal deste projeto não é construir um modelo de classificação nem prever individualmente se um cliente abandona ou permanece. O foco do trabalho é a construção de um **modelo descritivo de segmentação de clientes**, orientado para identificar grupos de clientes com características semelhantes.

A segmentação é útil porque permite deixar de observar a base de clientes como um conjunto homogéneo. Em vez de analisar todos os clientes da mesma forma, o projeto procura identificar perfis distintos a partir de características demográficas, contratuais, de serviços subscritos e de consumo. Esta abordagem pode apoiar decisões de gestão comercial, comunicação, acompanhamento e relacionamento com clientes.

Assim, a utilidade do projeto não está apenas em criar grupos, mas em compreender **o que distingue cada grupo** e **como essa informação pode ser interpretada em contexto de gestão**.

### Reflexão sobre a melhoria do trabalho

Este projeto será desenvolvido com uma preocupação explícita de melhoria qualitativa. O objetivo não é apenas cumprir uma sequência de tarefas ou preencher os ficheiros pedidos, mas demonstrar uma evolução clara na forma como o trabalho é planeado, justificado e interpretado.

Para isso, cada fase deverá responder ao objetivo SMART validado e às perguntas de investigação. A exploração dos dados deverá explicar por que motivo certas variáveis são relevantes para a segmentação. A preparação dos dados deverá justificar as decisões tomadas. A modelação deverá ser avaliada não apenas por métricas, mas também pela interpretabilidade dos perfis encontrados.

Desta forma, o projeto procura evoluir de uma abordagem meramente técnica para uma abordagem mais analítica, em que o código, os gráficos e os relatórios estejam ligados a uma narrativa coerente de Ciência de Dados aplicada à gestão.

### Objetivo SMART

Construir, até ao dia **14/06/2026**, um modelo descritivo de segmentação de clientes com base no conjunto de dados **Telco Customer Churn**, utilizando variáveis demográficas, contratuais, de serviços subscritos e de consumo, de modo a identificar **3 perfis de clientes estatisticamente caracterizáveis**, garantindo uma solução final com **Coeficiente de Silhueta médio igual ou superior a 0,24** e com cada perfil descrito através de pelo menos **cinco variáveis relevantes**, permitindo apoiar decisões de gestão comercial e relacionamento com clientes.

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

A inspeção inicial foi realizada no *Kaggle Code*, com o objetivo de compreender a estrutura geral do conjunto de dados **Telco Customer Churn** antes de avançar para as fases de exploração, preparação e segmentação.

O conjunto de dados contém **7043 observações** e **21 variáveis**. Cada observação representa um cliente e cada variável descreve uma característica associada ao cliente, ao contrato, aos serviços subscritos, ao método de pagamento ou aos valores pagos.

Na visualização das primeiras linhas do conjunto de dados, observou-se que existem variáveis de diferentes naturezas. Algumas descrevem características demográficas dos clientes, como `gender`, `SeniorCitizen`, `Partner` e `Dependents`. Outras estão relacionadas com os serviços contratados, como `PhoneService`, `InternetService`, `OnlineSecurity`, `TechSupport`, `StreamingTV` e `StreamingMovies`. Existem ainda variáveis associadas ao contrato e ao pagamento, como `Contract`, `PaperlessBilling`, `PaymentMethod`, `MonthlyCharges` e `TotalCharges`.

Relativamente aos tipos de dados, verificou-se que o conjunto de dados combina variáveis numéricas e categóricas. As variáveis `SeniorCitizen` e `tenure` surgem como valores inteiros, a variável `MonthlyCharges` surge como valor decimal e a maioria das restantes variáveis surge como categórica. A coluna `TotalCharges`, apesar de representar um valor monetário acumulado, surge inicialmente como variável categórica, pelo que necessita de tratamento posterior antes de poder ser utilizada como variável numérica.

A análise estatística inicial das variáveis numéricas mostrou que a variável `tenure`, que representa a antiguidade do cliente em meses, varia entre **0** e **72 meses**, com média de aproximadamente **32,37 meses** e mediana de **29 meses**. Esta variável poderá ser importante para a segmentação, uma vez que a antiguidade pode distinguir clientes recentes de clientes com relação mais prolongada com a empresa.

A variável `MonthlyCharges`, que representa o valor mensal pago pelo cliente, varia entre **18,25** e **118,75**, com média de aproximadamente **64,76** e mediana de **70,35**. Esta variável é relevante porque permite diferenciar clientes com níveis distintos de valor mensal associado aos serviços subscritos.

A variável `SeniorCitizen` apresenta valores **0** e **1**, sendo que a média aproximada de **0,16** indica que a maioria dos clientes não está identificada como cidadão sénior. Esta variável poderá ser usada na caracterização demográfica dos perfis, embora a sua relevância final dependa dos padrões encontrados durante a análise exploratória.

Na análise das variáveis categóricas, observou-se que `customerID` tem **7043 valores únicos**, confirmando que funciona como identificador técnico dos clientes. Por esse motivo, esta variável não deverá ser usada na segmentação, pois não representa uma característica comportamental, contratual ou de consumo.

A variável `Contract` apresenta três categorias, sendo **Month-to-month** a mais frequente, com **3875 ocorrências**. A existência de diferentes tipos de contrato sugere que podem existir perfis de clientes com níveis distintos de compromisso contratual com a empresa. Por esse motivo, esta variável poderá ter relevância na diferenciação dos segmentos.

A variável `InternetService` apresenta três categorias, sendo **Fiber optic** a mais frequente, com **3096 ocorrências**. Esta variável poderá ajudar a distinguir perfis de clientes com diferentes níveis de utilização de serviços digitais.

A variável `PaymentMethod` apresenta quatro categorias, sendo **Electronic check** a mais frequente, com **2365 ocorrências**. O método de pagamento pode contribuir para a caracterização dos perfis, uma vez que reflete diferenças nos hábitos administrativos e na forma como os clientes interagem com a empresa.

A verificação de valores em falta indicou que não existem valores nulos diretamente identificados pelo método de verificação inicial. Também não foram encontradas linhas duplicadas, uma vez que o número de duplicados identificado foi **0**.

No entanto, foi identificado um problema específico na coluna `TotalCharges`. Embora esta coluna não apresente valores nulos diretos, a conversão temporária para formato numérico permitiu identificar **11 valores problemáticos**. Estes casos correspondem a registos em que o valor total pago não está preenchido de forma numérica. Observou-se também que estes registos têm `tenure` igual a **0**, o que sugere que correspondem a clientes sem antiguidade registada no serviço. Estes valores deverão ser tratados numa fase posterior de preparação dos dados.

A variável `Churn` apresenta duas categorias: **No** e **Yes**. Na inspeção inicial, verificou-se que **5174 clientes** estão registados como **No**, correspondendo a aproximadamente **73,46%** do conjunto de dados, enquanto **1869 clientes** estão registados como **Yes**, correspondendo a aproximadamente **26,54%**. Esta variável existe no conjunto de dados, mas não constitui o foco principal do projeto, uma vez que o objetivo validado é construir um modelo descritivo de segmentação de clientes.

De forma geral, a inspeção inicial permitiu concluir que o conjunto de dados tem dimensão adequada para o desenvolvimento do projeto, não apresenta duplicados nem valores nulos diretos, mas requer tratamento específico da coluna `TotalCharges`. Também se confirmou que o conjunto de dados contém variáveis suficientes para caracterizar clientes em termos demográficos, contratuais, de serviços subscritos e de consumo, o que está alinhado com o objetivo SMART definido para o projeto.

### Dicionário das Variáveis

O dicionário completo das variáveis encontra-se documentado em `docs/M1_iniciacao.md`. No *README*, apresenta-se uma síntese dos principais grupos de variáveis considerados no projeto.

| Grupo de variáveis           | Variáveis principais                                                                                                                                      | Relevância para o projeto                                                                                                        |
| :--------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------- |
| Identificação                | `customerID`                                                                                                                                              | Identifica tecnicamente cada cliente, mas não deverá ser usada na segmentação por não representar comportamento ou perfil.       |
| Características demográficas | `gender`, `SeniorCitizen`, `Partner`, `Dependents`                                                                                                        | Permitem caracterizar os clientes e analisar se existem perfis demográficos distintos.                                           |
| Antiguidade e contrato       | `tenure`, `Contract`, `PaperlessBilling`                                                                                                                  | Podem distinguir clientes recentes, clientes com maior permanência e clientes com diferentes níveis de compromisso contratual.   |
| Serviços subscritos          | `PhoneService`, `MultipleLines`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies` | Permitem identificar padrões de utilização e combinações de serviços, sendo importantes para a construção dos perfis.            |
| Pagamento e consumo          | `PaymentMethod`, `MonthlyCharges`, `TotalCharges`                                                                                                         | Permitem diferenciar clientes de acordo com método de pagamento, valor mensal e valor acumulado pago.                            |
| Resultado observado          | `Churn`                                                                                                                                                   | Variável existente no conjunto de dados. Não será usada como variável alvo de classificação nem como foco do objetivo principal. |

## 2. Exploração (Milestone 2)
### Limpeza e Preparação
* [Breve resumo das ações de limpeza tomadas. Detalhes em `docs/M2_exploracao.md`]
### Principais Conclusões (EDA)
> *Dica: Insere aqui o gráfico mais importante do projeto.*
* **Ponto-chave:** [Ex: Identificámos que o fator X influencia em 40% o resultado Y, por aplicação
do método ganho de informação]
## 3. Modelação (Milestone 3)
### Abordagem Técnica
* **Modelos:** [Ex: Random Forest e XGBoost]
* **Métrica Principal:** [Ex: F1-Score ou RMSE]
## 4. Finalização (Milestone 4)
### Resposta ao Problema
[Resumo da solução e como ela gera valor para o negócio.]
### Recomendações de Inovação
1. [Sugestão prática baseada nos resultados] 

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

## Referências Técnicas

* IBM. *Data Understanding Overview*. Disponível em: https://www.ibm.com/docs/en/spss-modeler/saas?topic=understanding-data-overview

* *scikit-learn*. *Clustering*. Disponível em: https://scikit-learn.org/stable/modules/clustering.html

* *scikit-learn*. *Silhouette Score*. Disponível em: https://scikit-learn.org/stable/modules/generated/sklearn.metrics.silhouette_score.html

* *scikit-learn*. *Davies-Bouldin Score*. Disponível em: https://scikit-learn.org/stable/modules/generated/sklearn.metrics.davies_bouldin_score.html

* *kmodes*. *K-Modes and K-Prototypes clustering*. Disponível em: https://pypi.org/project/kmodes/

## Informação Institucional

**Instituição:** Coimbra Business School | ISCAC

**Curso:** Licenciatura em Ciência de Dados para a Gestão

**Unidade Curricular:** Projeto em Ciência de Dados

**Professor Responsável:** Dora Melo ([dmelo@iscac.pt](mailto:dmelo@iscac.pt))

---

*Data de última atualização: 02/06/2026*
