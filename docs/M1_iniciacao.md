# Milestone 1: Iniciação e Definição do Projeto

## 1. Descrição Detalhada do Problema

O presente projeto insere-se no tema **Previsão de Abandono de Clientes (Churn Prediction)**, utilizando o conjunto de dados **Telco Customer Churn**. Este dataset contém informação sobre clientes de uma empresa de telecomunicações, incluindo características demográficas, tipo de contrato, serviços subscritos, método de pagamento, antiguidade do cliente, valores pagos e a indicação de abandono do serviço.

O abandono de clientes é um problema relevante para empresas que funcionam com serviços por subscrição, como telecomunicações, software ou serviços financeiros. Quando um cliente cancela o serviço, a empresa perde receita futura e pode ter de investir mais recursos na aquisição de novos clientes. Por isso, compreender os perfis de clientes associados a maiores taxas de abandono pode apoiar decisões de retenção mais direcionadas.

Neste projeto, o objetivo não é construir um modelo de classificação supervisionada para prever individualmente se um cliente abandona ou não o serviço. Em vez disso, o trabalho será orientado para a **análise exploratória e segmentação de clientes**, procurando identificar grupos de clientes com características semelhantes e analisar quais desses grupos apresentam maiores taxas de abandono.

A variável **Churn** será utilizada apenas para analisar os segmentos identificados, isto é, para calcular e interpretar a taxa de abandono em cada perfil de cliente. Esta variável não será utilizada como variável-alvo para treinar um modelo supervisionado.

## 2. Objetivos SMART

*Defina os objetivos do projeto seguindo a lógica SMART (Específico, Mensurável, Atingível, Relevante e Temporal):*

1. **Objetivo 1:** Aplicar e comparar técnicas de segmentação não supervisionada, nomeadamente **K-Prototypes**, **K-Means** e **Clustering Hierárquico Aglomerativo**, ao conjunto de dados **Telco Customer Churn**, utilizando variáveis demográficas, contratuais e de consumo, como antiguidade do cliente, tipo de contrato, serviços subscritos, método de pagamento, mensalidade e valor total pago, com o objetivo de identificar entre **3 e 5 perfis distintos de clientes** até ao dia **23/04/2026**.

   A qualidade dos segmentos será avaliada através de métricas como **Silhouette Score**, **Davies-Bouldin Index** e interpretação estatística dos grupos. O resultado esperado é selecionar a solução de segmentação mais adequada e identificar quais os perfis que apresentam **taxas de abandono superiores à média global do dataset**, de modo a apoiar recomendações de retenção direcionadas.

### Questão SMART

Até ao dia **23/04/2026**, em que medida a aplicação e comparação de técnicas de segmentação não supervisionada, nomeadamente **K-Prototypes**, **K-Means** e **Clustering Hierárquico Aglomerativo**, permite identificar entre **3 e 5 perfis distintos de clientes** no conjunto de dados **Telco Customer Churn**, com base em variáveis demográficas, contratuais e de consumo, avaliando a qualidade dos agrupamentos através do **Silhouette Score**, do **Davies-Bouldin Index** e da interpretação estatística dos segmentos, de forma a identificar perfis com taxas de abandono superiores à média global do dataset e apoiar recomendações de retenção direcionadas?

### Perguntas de Investigação

1. Quais são as variáveis demográficas, contratuais e de consumo que apresentam maiores diferenças entre os clientes que abandonaram o serviço e os clientes que permaneceram?

2. Que perfis distintos de clientes podem ser identificados através da aplicação de técnicas de segmentação não supervisionada ao conjunto de dados **Telco Customer Churn**?

3. Qual das técnicas testadas, entre **K-Prototypes**, **K-Means** e **Clustering Hierárquico Aglomerativo**, apresenta a solução de segmentação mais adequada, considerando métricas como **Silhouette Score**, **Davies-Bouldin Index** e a interpretabilidade dos segmentos?

4. Quais são as principais características dos segmentos identificados, considerando variáveis como antiguidade, tipo de contrato, serviços subscritos, método de pagamento, mensalidade e valor total pago?

5. Que segmentos de clientes apresentam taxas de abandono superiores à média global do dataset e que recomendações de retenção podem ser propostas para esses perfis?

## 3. Metodologia de Gestão (PBL)

* **Ferramentas de Colaboração:** O projeto será desenvolvido com recurso ao **GitHub**, para organização do repositório, controlo de versões e registo da evolução do trabalho através de commits descritivos.

* **Ambiente de Desenvolvimento:** A exploração inicial dos dados será realizada no **Kaggle Code**, uma vez que o dataset está disponível na plataforma Kaggle. O notebook inicial será posteriormente guardado no repositório GitHub, na pasta `notebooks/`.

* **Documentação:** A documentação do projeto será realizada em ficheiros Markdown na pasta `docs/`, seguindo a estrutura das milestones. O ficheiro `M1_iniciacao.md` será usado para documentar a definição do problema, os objetivos, as perguntas de investigação, a viabilidade dos dados e as primeiras conclusões da inspeção inicial.

* **Organização do Código:** O código será organizado por fases, começando pela inspeção inicial dos dados. Nesta fase, o notebook `1.0_iniciacao.ipynb` terá apenas o carregamento do dataset, a visualização inicial, a análise dos tipos de dados, a verificação de valores nulos, a análise de duplicados, a estatística descritiva e a distribuição da variável `Churn`.

* **Bibliotecas Previstas:** As principais bibliotecas previstas para o desenvolvimento do projeto são `pandas`, `numpy`, `matplotlib`, `seaborn` e `scikit-learn`. Para a fase de segmentação, poderá ser necessário utilizar uma biblioteca adicional para o algoritmo **K-Prototypes**, como `kmodes`, caso seja compatível com o ambiente utilizado.

## 4. Análise de Viabilidade dos Dados

* **Disponibilidade:** O conjunto de dados **Telco Customer Churn** está disponível no Kaggle. O dataset já foi associado a um notebook no Kaggle Code e foi possível carregar o ficheiro CSV com sucesso.

* **Dimensão dos Dados:** A inspeção inicial permitiu verificar que o dataset contém **7043 linhas** e **21 colunas**. Cada linha representa um cliente e cada coluna representa uma característica associada ao cliente ou ao seu contrato.

* **Qualidade Inicial:** Numa primeira análise, não foram identificados valores nulos diretamente através da verificação de valores em falta. Também não foram identificadas linhas duplicadas. No entanto, foi observado que a coluna **TotalCharges** está armazenada como variável categórica, apesar de representar valores monetários. Após uma conversão temporária para formato numérico, foram identificados **11 valores problemáticos/em falta**, que deverão ser tratados numa fase posterior de preparação dos dados.

* **Tipos de Variáveis:** O dataset contém variáveis numéricas, como `tenure` e `MonthlyCharges`, e várias variáveis categóricas, como `gender`, `Partner`, `Dependents`, `PhoneService`, `InternetService`, `Contract`, `PaymentMethod` e `Churn`. A coluna `TotalCharges` necessita de tratamento posterior para ser corretamente utilizada como variável numérica.

* **Distribuição da Variável Churn:** A variável `Churn` apresenta duas categorias: clientes que permaneceram no serviço e clientes que abandonaram. Na inspeção inicial, verificou-se que **5174 clientes permaneceram** e **1869 clientes abandonaram** o serviço. Esta informação será usada para analisar a taxa de abandono em cada segmento identificado nas fases seguintes.

* **Ética:** O dataset não contém nomes reais, moradas, contactos diretos ou informação pessoal identificável dos clientes. A coluna `customerID` funciona apenas como identificador técnico. Ainda assim, o tratamento dos dados será feito de forma responsável, utilizando a informação apenas para fins académicos e de análise agregada.

## 5. Cronograma Interno

| Fase            | Data Limite      | Entregável Esperado                                                                                                                                     |
| :-------------- | :--------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------ |
| M1: Iniciação   | 24/02/2026       | Repositório estruturado, README inicial, ficheiro `docs/M1_iniciacao.md` preenchido e notebook inicial no Kaggle com carregamento e inspeção dos dados. |
| M2: Exploração  | Data a confirmar | Notebook de análise exploratória, tratamento inicial dos dados e documentação das principais decisões em `docs/M2_exploracao.md`.                       |
| M3: Modelação   | 23/04/2026       | Aplicação e comparação de técnicas de segmentação não supervisionada, avaliação dos segmentos e documentação em `docs/M3_modelacao.md`.                 |
| M4: Finalização | Data a confirmar | Interpretação final dos segmentos, recomendações de retenção, limitações do projeto e documentação em `docs/M4_conclusoes.md`.                          |

---

*Data de última atualização: 01/06/2026*

