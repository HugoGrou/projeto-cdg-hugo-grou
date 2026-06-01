# Análise e Segmentação de Clientes para Estudo do Abandono

## Identificação da Equipa

* Hugo Grou (nº 2023137127)

## Organização do Repositório

A estrutura deste projeto segue boas práticas de Ciência de Dados e organização de projetos em *GitHub*.

* **`data/`**: Armazenamento dos dados do projeto.

  * **`data/raw/`**: Local destinado aos dados brutos ou à referência para o conjunto de dados original.

  * **`data/processed/`**: Local destinado aos dados tratados em fases posteriores do projeto.

* **`docs/`**: Documentação técnica do projeto, organizada por *milestones*.

  * **`M1_iniciacao.md`**: Definição do problema, objetivo, perguntas de investigação, planeamento e análise inicial dos dados.

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

A variável **Churn** será utilizada apenas para analisar os segmentos identificados, permitindo calcular a taxa de abandono em cada grupo de clientes. Esta variável não será utilizada como variável alvo para treinar um modelo supervisionado.

### Objetivos do Projeto

* **Objetivo 1:** Aplicar e comparar técnicas de segmentação não supervisionada, nomeadamente *K-Prototypes*, *K-Means* e *Clustering Hierárquico Aglomerativo*, ao conjunto de dados **Telco Customer Churn**, utilizando variáveis demográficas, contratuais e de consumo, como antiguidade do cliente, tipo de contrato, serviços subscritos, método de pagamento, mensalidade e valor total pago, com o objetivo de identificar entre **3 e 5 perfis distintos de clientes** até ao dia **23/04/2026**.

* **Objetivo 2:** Avaliar a qualidade dos segmentos através de métricas como *Silhouette Score*, *Davies-Bouldin Index* e interpretação estatística dos grupos, selecionando a solução de segmentação mais adequada e identificando quais os perfis que apresentam taxas de abandono superiores à média global do conjunto de dados.

### Perguntas de Investigação

1. Quais são as variáveis demográficas, contratuais e de consumo que apresentam maiores diferenças entre os clientes que abandonaram o serviço e os clientes que permaneceram?

2. Que perfis distintos de clientes podem ser identificados através da aplicação de técnicas de segmentação não supervisionada ao conjunto de dados **Telco Customer Churn**?

3. Qual das técnicas testadas, entre *K-Prototypes*, *K-Means* e *Clustering Hierárquico Aglomerativo*, apresenta a solução de segmentação mais adequada, considerando métricas como *Silhouette Score*, *Davies-Bouldin Index* e a interpretabilidade dos segmentos?

4. Quais são as principais características dos segmentos identificados, considerando variáveis como antiguidade, tipo de contrato, serviços subscritos, método de pagamento, mensalidade e valor total pago?

5. Que segmentos de clientes apresentam taxas de abandono superiores à média global do conjunto de dados e que recomendações de retenção podem ser propostas para esses perfis?

### Fonte de Dados

* **Dataset:** Telco Customer Churn

* **Fonte:** https://www.kaggle.com/datasets/blastchar/telco-customer-churn

* **Dimensão:** 7043 linhas e 21 colunas

* **Unidade de análise:** Cliente

* **Variável de abandono:** Churn

## 2. Exploração (Milestone 2)

### Limpeza e Preparação

Esta fase será desenvolvida na Milestone 2. Com base na inspeção inicial, prevê-se que seja necessário analisar e tratar a coluna **TotalCharges**, uma vez que esta se encontra inicialmente como variável categórica, apesar de representar valores monetários.

Também será necessário preparar as variáveis para a análise exploratória e para a futura segmentação de clientes.

Detalhes desta fase serão documentados em **`docs/M2_exploracao.md`**.

### Principais Conclusões (EDA)

A desenvolver na Milestone 2.

Nesta fase serão analisadas as relações entre variáveis demográficas, contratuais e de consumo com a variável **Churn**, com recurso a tabelas, estatísticas descritivas e gráficos guardados na pasta **`reports/figures/`**.

## 3. Modelação (Milestone 3)

### Abordagem Técnica

A fase de modelação será orientada para segmentação não supervisionada, e não para classificação supervisionada.

* **Técnicas previstas:** *K-Prototypes*, *K-Means* e *Clustering Hierárquico Aglomerativo*.

* **Métricas previstas:** *Silhouette Score*, *Davies-Bouldin Index* e interpretação estatística dos segmentos.

* **Resultado esperado:** Identificar entre 3 e 5 perfis distintos de clientes e analisar quais apresentam taxas de abandono superiores à média global do conjunto de dados.

Detalhes desta fase serão documentados em **`docs/M3_modelacao.md`**.

## 4. Finalização (Milestone 4)

### Resposta ao Problema

A desenvolver na Milestone 4.

Nesta fase será apresentada a interpretação final dos segmentos identificados, com especial atenção aos perfis de clientes que apresentem maiores taxas de abandono.

### Recomendações de Inovação

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

