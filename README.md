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

Na inspeção inicial realizada no *Kaggle Code*, foi possível carregar o conjunto de dados e observar a sua estrutura geral.

Foram analisados os seguintes aspetos:

* dimensão do conjunto de dados;

* primeiras linhas da tabela;

* tipos de variáveis;

* estatísticas descritivas;

* existência de valores nulos;

* existência de linhas duplicadas;

* distribuição da variável `Churn`;

* verificação inicial da coluna `TotalCharges`.

A análise inicial indicou que o dataset contém **7043 linhas** e **21 colunas**. Não foram identificadas linhas duplicadas nem valores nulos diretamente através da verificação inicial. No entanto, foi observado que a coluna `TotalCharges` se encontra armazenada como variável categórica, apesar de representar valores monetários. Após uma conversão temporária para formato numérico, foram identificados **11 valores problemáticos**, que deverão ser tratados numa fase posterior.

A variável `Churn` apresenta duas categorias. Na inspeção inicial, verificou-se que **5174 clientes permaneceram** no serviço e **1869 clientes abandonaram**.

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
git clone [url-do-repositorio]
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
