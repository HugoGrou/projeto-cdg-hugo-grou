# Milestone 1: Iniciação e Definição do Projeto

## 1. Descrição Detalhada do Problema

O presente projeto utiliza o conjunto de dados **Telco Customer Churn**, disponível na plataforma Kaggle. Este conjunto de dados contém informação sobre clientes de uma empresa de telecomunicações, incluindo características demográficas, tipo de contrato, serviços subscritos, método de pagamento, antiguidade do cliente e valores pagos.

Embora o conjunto de dados esteja associado ao tema de abandono de clientes, o objetivo principal deste projeto não é construir um modelo de classificação supervisionada nem prever individualmente se um cliente abandona ou permanece no serviço. O foco do trabalho será a construção de um **modelo descritivo de segmentação de clientes**, isto é, um modelo de agrupamento que permita identificar perfis de clientes com características semelhantes.

A segmentação de clientes é relevante em contexto de gestão porque permite compreender melhor a composição da base de clientes. Ao identificar grupos com comportamentos, contratos, serviços e padrões de consumo semelhantes, a empresa pode apoiar decisões de gestão comercial, comunicação, acompanhamento e relacionamento com clientes.

Neste projeto, serão consideradas variáveis demográficas, contratuais, de serviços subscritos e de consumo. A variável `Churn` existe no conjunto de dados, mas não constitui o foco principal do projeto e não será utilizada como variável-alvo de classificação.

## 2. Objetivo SMART

Construir, até ao dia 14/06/2026, um modelo descritivo de segmentação de clientes com base no conjunto de dados Telco Customer Churn, utilizando variáveis demográficas, contratuais, de serviços subscritos e de consumo, de modo a identificar 3 perfis de clientes estatisticamente caracterizáveis, garantindo uma solução final com Coeficiente de Silhueta médio igual ou superior a 0,24 e com cada perfil descrito através de pelo menos cinco variáveis relevantes, permitindo apoiar decisões de gestão comercial e relacionamento com clientes.

### Critérios SMART

* **Específico:** O objetivo centra-se na construção de um modelo descritivo de segmentação de clientes, utilizando o conjunto de dados **Telco Customer Churn**.

* **Mensurável:** O objetivo define como resultado esperado a identificação de **3 perfis de clientes**, uma solução com **Coeficiente de Silhueta médio igual ou superior a 0,24** e a descrição de cada perfil através de pelo menos **cinco variáveis relevantes**.

* **Atingível:** O conjunto de dados contém variáveis demográficas, contratuais, de serviços subscritos e de consumo suficientes para desenvolver uma análise de segmentação.

* **Relevante:** A identificação de perfis de clientes pode apoiar decisões de gestão comercial e relacionamento com clientes.

* **Temporal:** O objetivo deverá ser concretizado até ao dia **23/04/2026**.

### Perguntas de Investigação

1. Quais são as características demográficas, contratuais, de serviços subscritos e de consumo que melhor descrevem a heterogeneidade dos clientes no conjunto de dados **Telco Customer Churn**?

2. Que perfis de clientes podem ser identificados no conjunto de dados e como se caracterizam estatisticamente em termos de antiguidade, mensalidade, valor total pago, tipo de contrato, método de pagamento e serviços subscritos?

3. De que forma os perfis de clientes identificados podem apoiar decisões de gestão comercial e de relacionamento com clientes?

## 3. Metodologia de Gestão (PBL)

* **Ferramentas de colaboração:** O projeto será desenvolvido com recurso ao **GitHub**, permitindo organizar o repositório, controlar versões e registar a evolução do trabalho através de mensagens de commit descritivas.

* **Ambiente de desenvolvimento:** A exploração inicial dos dados será realizada no **Kaggle Code**, uma vez que o conjunto de dados está disponível na plataforma Kaggle. O notebook inicial será guardado no repositório GitHub, na pasta `notebooks/`.

* **Documentação:** A documentação será organizada na pasta `docs/`, com ficheiros Markdown correspondentes às diferentes fases do projeto. O ficheiro `M1_iniciacao.md` documenta a definição do problema, o objetivo SMART, as perguntas de investigação, a metodologia, a viabilidade dos dados e o cronograma.

* **Organização do código:** O código será separado por fases. Na Milestone 1, o notebook `1.0_iniciacao.ipynb` contém apenas o carregamento do dataset, a visualização inicial, a análise dos tipos de dados, a verificação de valores nulos, a verificação de duplicados, a estatística descritiva e a análise inicial da estrutura do conjunto de dados.

* **Bibliotecas previstas:** As principais bibliotecas previstas para o desenvolvimento do projeto são `pandas`, `numpy`, `matplotlib`, `seaborn` e `scikit-learn`. Outras bibliotecas poderão ser utilizadas se forem necessárias e justificadas nas fases seguintes do projeto.

## 4. Análise de Viabilidade dos Dados

* **Disponibilidade:** O conjunto de dados **Telco Customer Churn** está disponível no Kaggle. O dataset já foi associado a um notebook no Kaggle Code e foi possível carregar o ficheiro CSV com sucesso.

* **Dimensão dos dados:** A inspeção inicial permitiu verificar que o conjunto de dados contém **7043 linhas** e **21 colunas**. Cada linha representa um cliente e cada coluna representa uma característica associada ao cliente, ao contrato, aos serviços subscritos ou aos pagamentos.

* **Estrutura das variáveis:** O conjunto de dados combina variáveis numéricas e categóricas. As variáveis numéricas principais identificadas são `tenure`, `MonthlyCharges` e `TotalCharges`, embora `TotalCharges` esteja inicialmente armazenada como variável categórica e necessite de tratamento posterior. As restantes variáveis são maioritariamente categóricas e descrevem características demográficas, contratuais, serviços subscritos e métodos de pagamento.

* **Qualidade inicial dos dados:** A verificação inicial indicou que não existem linhas duplicadas. Também não foram identificados valores nulos diretamente através da verificação inicial de valores em falta. No entanto, foi identificado um problema na coluna `TotalCharges`: apesar de representar valores monetários, esta coluna encontra-se armazenada como variável categórica. Após uma conversão temporária para formato numérico, foram identificados **11 valores problemáticos**, que deverão ser tratados numa fase posterior de preparação dos dados.

* **Variável `Churn`:** A variável `Churn` existe no conjunto de dados e apresenta duas categorias: `Yes` e `No`. Na inspeção inicial, verificou-se que **5174 clientes** estão registados como `No` e **1869 clientes** estão registados como `Yes`. Esta variável não será utilizada como variável-alvo de classificação, uma vez que o objetivo validado é construir um modelo descritivo de segmentação de clientes.

* **Adequação ao objetivo SMART:** O conjunto de dados é adequado ao objetivo definido, pois contém variáveis suficientes para caracterizar clientes em diferentes dimensões: demográfica, contratual, serviços subscritos e consumo. Estas variáveis permitem construir e interpretar perfis de clientes, o que está alinhado com o objetivo de segmentação.

* **Ética:** O conjunto de dados não contém nomes reais, moradas, contactos diretos ou informação pessoal identificável dos clientes. A coluna `customerID` funciona como identificador técnico. Ainda assim, os dados serão utilizados apenas para fins académicos e analisados de forma agregada.

## 5. Cronograma Interno

| Fase            | Data Limite | Entregável Esperado                                                                                                                                     |
| :-------------- | :---------- | :------------------------------------------------------------------------------------------------------------------------------------------------------ |
| M1: Iniciação   | 14/06/2026  | Repositório estruturado, README inicial, ficheiro `docs/M1_iniciacao.md` preenchido e notebook inicial no Kaggle com carregamento e inspeção dos dados. |
| M2: Exploração  | 14/06/2026  | Notebook de análise exploratória, tratamento inicial dos dados e documentação das principais decisões em `docs/M2_exploracao.md`.                       |
| M3: Modelação   | 14/06/2026  | Construção do modelo descritivo de segmentação, avaliação da solução obtida e caracterização estatística dos perfis de clientes.                        |
| M4: Finalização | 14/06/2026  | Interpretação final dos perfis identificados, resposta ao objetivo SMART, recomendações de gestão comercial e documentação em `docs/M4_conclusoes.md`.  |

---

*Data de última atualização: 02/06/2026*
