# Relatório de Conclusão e Entrega de Valor (Milestone 4)

## 1. Síntese de Resultados e Impacto

### O Problema Resolvido

O objetivo deste projeto foi construir um modelo descritivo de segmentação de clientes com base no conjunto de dados **Telco Customer Churn**, utilizando variáveis demográficas, contratuais, de serviços subscritos e de consumo, de modo a identificar **3 perfis de clientes estatisticamente caracterizáveis**.

O objetivo SMART definido na Milestone 1 foi:

> Construir, até ao dia **14/06/2026**, um modelo descritivo de segmentação de clientes com base no conjunto de dados Telco Customer Churn, utilizando variáveis demográficas, contratuais, de serviços subscritos e de consumo, de modo a identificar **3 perfis de clientes estatisticamente caracterizáveis**, garantindo uma solução final com **Coeficiente de Silhueta médio igual ou superior a 0,24** e com cada perfil descrito através de pelo menos cinco variáveis relevantes, permitindo apoiar decisões de gestão comercial e relacionamento com clientes.

Com base nos resultados obtidos na fase de modelação, este objetivo foi alcançado. O modelo final identificou exatamente **3 perfis de clientes** e obteve um **Coeficiente de Silhueta de 0,3947**, valor superior ao mínimo definido inicialmente de **0,24**.

A diferença face ao objetivo mínimo foi:

```text
0,3947 - 0,24 = 0,1547
```

Isto significa que o modelo final superou o critério mínimo de qualidade definido no início do projeto.

O modelo final escolhido foi um **Gaussian Mixture Model**, aplicado à variante de dados **Numéricas + Engenharia**, com **3 clusters**. Este modelo obteve:

* **Coeficiente de Silhueta:** 0,3947;
* **Davies-Bouldin Index:** 0,9626;
* **Calinski-Harabasz Score:** 7142,2309;
* **Percentagem mínima de clientes num cluster:** 29,62%.

A escolha do modelo final resultou da comparação entre o modelo baseline, modelos candidatos e uma fase de otimização avançada. Embora tenha sido encontrado um modelo com **2 clusters** e Silhouette superior, esse resultado não foi escolhido como solução final, porque o objetivo SMART exigia a identificação de **3 perfis de clientes**. Assim, foi selecionado o melhor modelo que respeitava simultaneamente a métrica de qualidade e o número de perfis definido no objetivo.

A distribuição final dos clusters foi equilibrada:

* **Cluster 0:** 2086 clientes, correspondendo a 29,62% do total;
* **Cluster 1:** 2298 clientes, correspondendo a 32,63% do total;
* **Cluster 2:** 2659 clientes, correspondendo a 37,75% do total.

Nenhum cluster ficou residual ou demasiado pequeno, o que torna a segmentação mais útil para interpretação e tomada de decisão.

### Interpretação dos Resultados

Em vez de tratar todos os clientes da mesma forma, o modelo permitiu identificar **três grupos com comportamentos distintos**:

1. clientes com baixo consumo e menor utilização de serviços;
2. clientes antigos, com maior valor acumulado e maior número de serviços subscritos;
3. clientes mais recentes, com encargos mensais elevados, mas menor valor acumulado até ao momento.

Em linguagem simples, o modelo mostra que a base de clientes não é homogénea. Existem clientes com níveis muito diferentes de permanência, consumo mensal, valor acumulado e utilização de serviços. Esta informação permite apoiar decisões de gestão comercial mais direcionadas, em vez de aplicar a mesma estratégia a todos os clientes.

O Coeficiente de Silhueta de **0,3947** indica que os grupos têm uma separação aceitável para um projeto descritivo de segmentação. Não significa que os clusters estejam perfeitamente separados, mas mostra que existe estrutura suficiente nos dados para identificar perfis úteis e interpretáveis.

### Evidências Visuais dos Resultados

As figuras seguintes apresentam as principais evidências visuais da solução final e encontram-se guardadas na pasta `reports/figures/`. Como este ficheiro está dentro da pasta `docs/`, o caminho relativo utilizado é `../reports/figures/...`.

#### Silhouette Plot do Modelo Final

![Silhouette Plot do Modelo Final](../reports/figures/m3_silhouette_plot_modelo_final.png)

Este gráfico permite observar a coesão interna dos clusters. A linha vertical representa o valor médio do Coeficiente de Silhueta. O resultado confirma que a solução final apresenta uma separação aceitável entre os grupos.

#### Visualização PCA dos Segmentos

![Visualização PCA do Modelo Final](../reports/figures/m3_pca_modelo_final.png)

A visualização PCA reduz os dados para duas dimensões, permitindo observar graficamente a distribuição dos clientes por cluster. No notebook, as duas primeiras componentes principais explicaram aproximadamente **90,5%** da variância da representação usada no modelo final, o que torna esta visualização útil para comunicar a estrutura dos segmentos.

#### Perfil dos Segmentos

![Perfil dos Segmentos](../reports/figures/m3_perfil_segmentos_variaveis_numericas.png)

Este gráfico resume as diferenças entre os clusters com base nas variáveis numéricas principais. É uma das imagens mais importantes para a Milestone 4, porque traduz a modelação técnica em perfis de negócio interpretáveis.

### Caracterização dos Perfis de Clientes

#### Cluster 0 — Clientes com baixo consumo e baixa utilização de serviços

O Cluster 0 representa **2086 clientes**, correspondendo a **29,62%** do total.

Este grupo apresenta valores médios baixos em variáveis associadas ao consumo e à utilização de serviços. O `MonthlyCharges` médio é de **25,52**, o `TotalCharges` médio é de **689,62** e o `ServiceCount` médio é de **1,25**. O `tenure` médio é de **27,61** e o `AvgChargePerTenure` médio é de **25,47**.

Este perfil representa clientes com encargos mensais baixos, baixo valor acumulado e poucos serviços subscritos. Também apresenta forte presença de clientes sem serviço de Internet, de acordo com a caracterização categórica feita no notebook.

Do ponto de vista de negócio, este grupo pode corresponder a clientes com utilização mais básica dos serviços da empresa. São clientes que podem representar oportunidades de crescimento comercial através de propostas simples e adequadas ao seu perfil.

Possíveis ações de gestão:

* propor campanhas de adesão gradual a serviços adicionais;
* comunicar pacotes simples e de baixo custo;
* evitar estratégias demasiado agressivas de venda;
* manter canais de comunicação adequados a clientes menos digitais ou com serviços mais básicos.

#### Cluster 1 — Clientes antigos, com maior valor acumulado e maior utilização de serviços

O Cluster 1 representa **2298 clientes**, correspondendo a **32,63%** do total.

Este grupo apresenta os valores médios mais elevados em várias dimensões importantes. O `tenure` médio é de **57,29**, o `MonthlyCharges` médio é de **89,79**, o `TotalCharges` médio é de **5127,99** e o `ServiceCount` médio é de **5,56**. O `AvgChargePerTenure` médio é de **89,85**.

Este perfil representa clientes com maior permanência, maior valor mensal, maior valor acumulado e maior número de serviços subscritos. É o segmento com maior intensidade de relação com a empresa.

Do ponto de vista comercial, este grupo pode ser considerado um segmento de elevado valor, porque combina antiguidade, consumo mensal elevado e utilização de vários serviços.

Possíveis ações de gestão:

* desenvolver ações de fidelização para proteger clientes de maior valor;
* oferecer benefícios associados à antiguidade;
* criar campanhas de manutenção e valorização da relação comercial;
* priorizar a qualidade do atendimento e do suporte;
* propor serviços premium apenas quando forem coerentes com o histórico de utilização.

#### Cluster 2 — Clientes recentes com encargos mensais elevados

O Cluster 2 representa **2659 clientes**, correspondendo a **37,75%** do total.

Este grupo apresenta menor tempo de permanência, mas encargos mensais relativamente elevados. O `tenure` médio é de **14,57**, o `MonthlyCharges` médio é de **73,92**, o `TotalCharges` médio é de **1065,63** e o `ServiceCount` médio é de **3,12**. O `AvgChargePerTenure` médio é de **73,74**.

Este perfil representa clientes mais recentes que já têm mensalidades relevantes, mas que ainda não acumularam muito valor ao longo do tempo.

Este segmento é importante porque pode exigir acompanhamento inicial. Clientes com mensalidades elevadas logo numa fase inicial da relação podem necessitar de uma boa experiência de onboarding, explicação clara do valor contratado e acompanhamento para evitar insatisfação.

Possíveis ações de gestão:

* reforçar a comunicação nos primeiros meses de contrato;
* garantir que o cliente compreende os serviços incluídos na mensalidade;
* monitorizar satisfação e pedidos de suporte;
* criar ações de acompanhamento inicial;
* avaliar oportunidades de fidelização antes de o cliente se tornar vulnerável a alternativas concorrentes.

A variável `AvgChargePerTenure` foi usada como apoio à interpretação dos perfis, mas deve ser lida com cautela, uma vez que apresentou correlação elevada com `MonthlyCharges` durante a fase de seleção de atributos.

### Valor para o Utilizador ou Negócio

O valor principal deste projeto não está em prever individualmente se um cliente vai abandonar a empresa. O projeto não é de classificação e não usa `Churn` como variável-alvo. O valor está em **compreender a estrutura da base de clientes** e identificar grupos com comportamentos semelhantes.

Através desta segmentação, uma equipa de gestão comercial pode:

* adaptar campanhas de comunicação a diferentes perfis;
* distinguir clientes básicos, clientes de elevado valor e clientes recentes com encargos relevantes;
* definir prioridades de acompanhamento comercial;
* apoiar estratégias de fidelização e relacionamento;
* melhorar a interpretação da base de clientes sem recorrer a decisões automáticas opacas.

A solução final transforma dados técnicos em conhecimento acionável: permite perceber **quem são os grupos de clientes**, **como diferem entre si** e **que tipo de abordagem comercial pode fazer sentido para cada grupo**.

## 2. Análise Crítica e Limitações

### Limitações dos Dados

Apesar de o conjunto de dados permitir uma segmentação útil, existem limitações importantes.

Em primeiro lugar, o dataset representa uma base de clientes específica e não deve ser automaticamente generalizado para todas as empresas de telecomunicações. Os padrões encontrados dependem das variáveis disponíveis e da população representada no conjunto de dados.

Em segundo lugar, o dataset não inclui algumas variáveis que poderiam melhorar a interpretação dos perfis, como:

* histórico temporal detalhado de contactos com o apoio ao cliente;
* número de reclamações;
* nível de satisfação do cliente;
* região geográfica;
* campanhas comerciais recebidas;
* histórico de alterações de contrato;
* utilização real dos serviços ao longo do tempo;
* motivo de eventual saída do cliente.

Estas variáveis poderiam ajudar a compreender melhor o comportamento dos clientes e a transformar a segmentação numa ferramenta mais rica para decisões de negócio.

Também é importante referir que a variável `customerID` foi removida por ser apenas um identificador, e a variável `Churn` não foi usada como variável-alvo, porque o projeto foi definido como descritivo e não supervisionado.

### Limitações do Modelo

O modelo final é um modelo de segmentação, não um modelo de previsão individual. Por isso, não deve ser interpretado como uma ferramenta que prevê se um cliente vai sair da empresa.

O modelo identifica grupos com características semelhantes, mas não prova relações de causalidade. Por exemplo, o facto de um grupo ter mensalidades mais elevadas não significa, por si só, que essa mensalidade cause determinado comportamento futuro. O modelo apenas descreve padrões presentes nos dados.

Também existem limitações associadas ao próprio Coeficiente de Silhueta. O valor final de **0,3947** indica uma separação aceitável, mas não perfeita. Isto significa que podem existir clientes próximos da fronteira entre clusters, especialmente quando partilham características semelhantes com mais do que um grupo.

O diagnóstico por cluster mostrou que o Cluster 0 apresentou Silhouette média de **0,3946** e **1,53%** de valores negativos. O Cluster 1 apresentou Silhouette média de **0,4189** e **4,44%** de valores negativos. O Cluster 2 apresentou Silhouette média de **0,3744** e **0,00%** de valores negativos.

Estes valores mostram que a maioria dos clientes está bem enquadrada no respetivo grupo, mas também indicam que existe alguma sobreposição, sobretudo no Cluster 1, onde a percentagem de valores negativos foi superior à dos restantes clusters.

### Contextos de Falha

O modelo pode ser menos adequado nos seguintes contextos:

* quando aplicado a dados de outra empresa com estrutura de clientes muito diferente;
* quando usado para prever churn individual, porque não foi construído para esse objetivo;
* quando usado sem atualização periódica, pois os perfis de clientes podem mudar ao longo do tempo;
* quando usado para decisões automáticas sem análise humana;
* quando aplicado a novos clientes com características que não estavam representadas no dataset original.

Assim, a solução deve ser vista como uma ferramenta de apoio à análise e à decisão, e não como um sistema automático de decisão comercial.

### Limitação Relacionada com a Escolha dos 3 Clusters

Durante a otimização avançada foi encontrado um modelo com **2 clusters** e Silhouette superior. No entanto, esse modelo não foi escolhido como solução final porque não cumpria o objetivo SMART, que exigia a identificação de **3 perfis de clientes**.

Esta decisão é importante: o projeto privilegiou o alinhamento com o objetivo definido inicialmente e a utilidade interpretativa dos 3 perfis. Ainda assim, para trabalho futuro, faria sentido comparar com mais profundidade a solução de 2 clusters, para perceber se ela representa uma segmentação mais simples e potencialmente mais robusta.

### Representação Final dos Dados

A representação final escolhida foi a variante **Numéricas + Engenharia**, que inclui variáveis numéricas e variáveis criadas durante a fase de preparação.

Foram analisadas variáveis demográficas, contratuais, de serviços e de consumo ao longo do projeto. No entanto, a solução final privilegiou variáveis numéricas e de engenharia por apresentarem melhor equilíbrio entre desempenho, estabilidade e interpretabilidade.

As variáveis categóricas foram especialmente importantes na fase de interpretação dos perfis, permitindo enriquecer a leitura dos segmentos encontrados.

## 3. Considerações Éticas e de Viés

### Privacidade

O projeto utilizou um dataset estruturado, sem recurso a nomes, moradas, contactos diretos ou informação pessoal sensível explícita. A variável `customerID` foi removida da modelação por funcionar apenas como identificador e não acrescentar valor analítico para a segmentação.

Apesar disso, a segmentação de clientes deve ser sempre usada com cuidado, porque mesmo dados aparentemente comerciais podem permitir diferenciar grupos de pessoas e influenciar decisões de relacionamento, comunicação ou prioridade comercial.

### Risco de Discriminação ou Tratamento Desigual

Uma das variáveis disponíveis no dataset é `SeniorCitizen`, que representa uma característica demográfica. Esta variável pode ajudar a descrever diferenças entre clientes, mas deve ser usada com cuidado em contexto real.

O modelo não deve ser utilizado para discriminar clientes, limitar acesso a serviços ou criar condições comerciais injustas. A segmentação deve servir para melhorar a comunicação, adequar ofertas e apoiar relacionamento com clientes, não para penalizar grupos específicos.

### Transparência

O projeto procurou manter transparência nas decisões tomadas:

* a variável `Churn` não foi usada como alvo, porque o objetivo não era previsão supervisionada;
* a variável `customerID` foi removida por ser identificador;
* foram documentadas as transformações realizadas;
* foram criadas variáveis de engenharia com interpretação clara;
* foram comparados modelos e métricas antes da escolha final;
* foram apresentadas limitações do modelo.

Esta transparência é importante para que qualquer pessoa consiga compreender como os dados foram transformados em segmentos e porque foi escolhida a solução final.

### Utilização Responsável

A segmentação deve ser usada como apoio à decisão humana. O modelo pode ajudar a identificar padrões, mas não substitui análise de contexto, conhecimento de negócio e validação por parte de equipas responsáveis.

Em contexto real, antes de usar esta solução para decisões comerciais, seria necessário validar os segmentos com dados atuais, avaliar o impacto sobre diferentes grupos de clientes e garantir conformidade com regras de proteção de dados.

## 4. Roadmap e Trabalhos Futuros

### 1. Melhoria Técnica

Uma primeira melhoria futura seria testar uma validação mais aprofundada da estabilidade dos clusters ao longo do tempo. Como o dataset não inclui uma dimensão temporal detalhada, não foi possível avaliar se os perfis se mantêm estáveis mês após mês.

Também seria útil comparar mais detalhadamente diferentes soluções de número de clusters, sobretudo:

* **2 clusters**, porque apresentou Silhouette superior na otimização avançada;
* **3 clusters**, porque foi a solução alinhada com o objetivo SMART;
* **4 ou mais clusters**, caso se pretenda uma segmentação mais detalhada.

Outra possibilidade seria testar métodos adicionais de clustering, como **HDBSCAN**, **OPTICS** ou modelos hierárquicos mais aprofundados, caso exista capacidade computacional suficiente.

### 2. Novas Variáveis

Para melhorar a utilidade de negócio da segmentação, seria relevante recolher novas variáveis, como:

* satisfação do cliente, através de pontuações de satisfação, NPS ou avaliações de atendimento;
* histórico de contactos, como número de chamadas, reclamações ou pedidos ao suporte;
* histórico comercial, incluindo campanhas recebidas, promoções aceites e alterações contratuais;
* informação temporal, como evolução mensal dos encargos, serviços adicionados ou removidos;
* dados geográficos agregados, caso sejam recolhidos de forma compatível com privacidade;
* indicadores de utilização real, como volume de dados, chamadas, streaming ou outros consumos efetivos.

Estas variáveis poderiam permitir perfis mais ricos e decisões comerciais mais fundamentadas.

### 3. Escalabilidade e Deployment

Como trabalho futuro, o projeto poderia evoluir para uma ferramenta simples de utilização por equipas não técnicas.

Uma possibilidade seria desenvolver uma aplicação em **Streamlit**, onde o utilizador pudesse carregar um novo ficheiro de clientes e obter:

* atribuição automática de cluster;
* resumo do perfil de cada cliente;
* visualização da distribuição dos segmentos;
* recomendações comerciais associadas a cada perfil.

Outra possibilidade seria construir um dashboard em **Power BI**, com gráficos sobre dimensão dos clusters, perfil médio dos segmentos e comparação entre variáveis principais.

### 4. Validação com Conhecimento de Negócio

Antes de aplicar esta segmentação num contexto real, seria importante validar os perfis com pessoas da área comercial, marketing ou suporte ao cliente.

Essa validação permitiria responder a perguntas como:

* os perfis fazem sentido do ponto de vista do negócio?
* as recomendações propostas são aplicáveis?
* existem segmentos que deveriam ser divididos ou agrupados?
* que ações comerciais seriam realmente viáveis para cada perfil?

Esta etapa ajudaria a transformar o modelo de segmentação numa ferramenta mais próxima da realidade operacional.

### 5. Monitorização Contínua

Caso o modelo fosse colocado em produção, seria necessário monitorizar periodicamente:

* se a distribuição dos clusters se mantém estável;
* se surgem novos perfis de clientes;
* se as variáveis usadas continuam relevantes;
* se os clusters continuam interpretáveis;
* se as ações comerciais associadas aos segmentos produzem resultados positivos.

Sem monitorização, existe o risco de o modelo deixar de representar corretamente a realidade dos clientes.

## Conclusão Final

O projeto cumpriu o objetivo definido na Milestone 1. Foi construído um modelo descritivo de segmentação de clientes com base no dataset **Telco Customer Churn**, recorrendo a uma abordagem não supervisionada e sem utilizar `Churn` como variável-alvo.

O modelo final escolhido foi um **Gaussian Mixture Model com 3 clusters**, obtendo um **Coeficiente de Silhueta de 0,3947**, acima do mínimo de **0,24** definido no objetivo SMART.

Foram identificados três perfis principais:

1. clientes com baixo consumo e baixa utilização de serviços;
2. clientes antigos, com maior valor acumulado e maior número de serviços;
3. clientes recentes, com mensalidade elevada e valor acumulado ainda reduzido.

A principal contribuição do projeto está na transformação dos dados em conhecimento acionável. A segmentação permite compreender melhor a base de clientes e apoiar decisões de gestão comercial, comunicação e relacionamento com clientes.

Apesar das limitações identificadas, a solução é coerente com o objetivo inicial, apresenta resultados interpretáveis e constitui uma base sólida para evolução futura, nomeadamente através da recolha de novas variáveis, validação com conhecimento de negócio e eventual desenvolvimento de uma ferramenta de utilização prática.

---

**Data de Conclusão:** 14/06/2026
**Versão do Projeto:** v4.0 Final
