# Milestone 2: Análise Exploratória e Engenharia de Atributos

## 1. Análise Exploratória de Dados (EDA)

### 1.1. Distribuição das variáveis críticas para segmentação

O projeto segue uma abordagem de **aprendizagem não supervisionada**, com o objetivo de construir um modelo descritivo de segmentação de clientes. Por esse motivo, não existe uma variável-alvo no sentido clássico de classificação ou regressão.

A variável `Churn` existe no dataset original, mas não foi utilizada como variável-alvo, uma vez que o objetivo do projeto não é prever abandono, mas sim identificar **3 perfis de clientes estatisticamente caracterizáveis** com base em variáveis demográficas, contratuais, de serviços subscritos e de consumo.

Assim, em vez de analisar a distribuição de uma variável-alvo, a análise exploratória incidiu sobre variáveis consideradas críticas para diferenciar os clientes. Entre as variáveis numéricas, foram especialmente relevantes `tenure`, `MonthlyCharges` e `TotalCharges`.

A variável `tenure` representa o tempo de permanência do cliente, em meses, e é importante para distinguir clientes recentes de clientes antigos. Esta variável apresentou uma média de **32,37 meses**, uma mediana de **29 meses**, um desvio padrão de **24,56**, um valor mínimo de **0** e um valor máximo de **72 meses**. O seu coeficiente de variação foi de **0,7587**, o que indica uma dispersão considerável e confirma a existência de clientes com tempos de permanência bastante diferentes.

A variável `MonthlyCharges` representa o valor mensal cobrado ao cliente e permite distinguir clientes com baixo, médio ou elevado valor mensal. Esta variável apresentou uma média de **64,76**, uma mediana de **70,35**, um desvio padrão de **30,09**, um valor mínimo de **18,25** e um valor máximo de **118,75**. O coeficiente de variação foi de **0,4646**, sendo inferior ao das restantes variáveis analisadas, mas ainda assim suficiente para mostrar diferenças relevantes nos encargos mensais dos clientes.

A variável `TotalCharges` representa o valor total acumulado ao longo da relação do cliente com a empresa. Esta variável é particularmente importante para a segmentação, porque combina indiretamente o efeito do tempo de permanência com o valor mensal pago. Apresentou uma média de **2279,73**, uma mediana de **1394,55**, um desvio padrão de **2266,79**, um valor mínimo de **0** e um valor máximo de **8684,80**. O seu coeficiente de variação foi de **0,9943**, o mais elevado entre as três variáveis analisadas, revelando uma dispersão relativa muito significativa.

Foram criados histogramas e boxplots para estas variáveis, permitindo observar a distribuição dos valores, a dispersão e a eventual existência de valores extremos. De forma geral, a análise mostrou que `TotalCharges` é a variável com maior variabilidade relativa, o que é coerente com a sua natureza acumulada. A variável `tenure` também apresentou uma dispersão relevante, refletindo a existência de clientes muito recentes e clientes com vários anos de relação com a empresa. Já `MonthlyCharges`, apesar de apresentar menor dispersão relativa, continua a ser importante para distinguir clientes com diferentes níveis de consumo mensal.

Em conjunto, estas três variáveis fornecem informação essencial para a segmentação, uma vez que permitem diferenciar clientes em função da antiguidade, do valor mensal pago e do valor económico acumulado ao longo da relação com a empresa.

#### Figuras associadas

A análise da distribuição das variáveis numéricas foi apoiada pelos seguintes gráficos:

![Histograma de tenure](../reports/figures/histograma_tenure.png)

O histograma de `tenure` mostra a distribuição do tempo de permanência dos clientes. Observa-se uma concentração elevada de clientes com poucos meses de relação com a empresa, mas também um grupo relevante de clientes com permanência elevada, próximo do limite máximo observado. Esta dispersão confirma a utilidade da variável para distinguir clientes recentes de clientes antigos.

![Histograma de MonthlyCharges](../reports/figures/histograma_MonthlyCharges.png)

O histograma de `MonthlyCharges` mostra que existem clientes com mensalidades bastante diferentes. Destaca-se uma concentração de clientes com encargos mensais mais baixos, mas também uma presença relevante de clientes com valores mensais médios e elevados. Esta variável é importante para diferenciar clientes com diferentes níveis de consumo mensal.

![Histograma de TotalCharges](../reports/figures/histograma_TotalCharges.png)

O histograma de `TotalCharges` apresenta uma distribuição assimétrica, com maior concentração de clientes em valores totais acumulados mais baixos. Isto é coerente com a existência de clientes recentes ou com menor consumo acumulado. A cauda à direita indica que existe também um conjunto de clientes com valor económico acumulado mais elevado.

![Boxplot de tenure](../reports/figures/boxplot_tenure.png)

O boxplot de `tenure` confirma a grande dispersão do tempo de permanência dos clientes. A mediana situa-se numa zona intermédia, refletindo a coexistência de clientes recentes e clientes com vários anos de relação com a empresa.

![Boxplot de MonthlyCharges](../reports/figures/boxplot_MonthlyCharges.png)

O boxplot de `MonthlyCharges` mostra uma amplitude considerável nos valores mensais pagos pelos clientes. Esta variação reforça a relevância da variável para a segmentação, uma vez que permite distinguir clientes com diferentes níveis de encargos mensais.

![Boxplot de TotalCharges](../reports/figures/boxplot_TotalCharges.png)

O boxplot de `TotalCharges` evidencia uma forte dispersão no valor total acumulado pelos clientes. Esta variável é particularmente relevante para a segmentação, porque reflete simultaneamente o tempo de permanência e os encargos mensais pagos ao longo da relação com a empresa.

Em conjunto, estes gráficos mostram que `tenure`, `MonthlyCharges` e `TotalCharges` apresentam variabilidade suficiente para contribuir para a diferenciação dos clientes na fase de segmentação.

#### Frequência das variáveis categóricas

Foram também analisadas as frequências absolutas e relativas das variáveis categóricas, de forma a compreender a composição da base de clientes ao nível dos serviços contratados, tipo de contrato, método de pagamento e características demográficas.

A variável `customerID` foi excluída por ser apenas um identificador. A variável `Churn` não foi utilizada como alvo, mantendo a coerência com a abordagem não supervisionada.

As variáveis categóricas analisadas foram: `gender`, `Partner`, `Dependents`, `PhoneService`, `MultipleLines`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies`, `Contract`, `PaperlessBilling` e `PaymentMethod`.

Entre estas variáveis, destacaram-se como especialmente relevantes `Contract`, `InternetService`, `PaymentMethod`, `OnlineSecurity`, `TechSupport`, `PaperlessBilling` e `MultipleLines`, porque ajudam a distinguir clientes com diferentes tipos de contrato, níveis de adesão a serviços adicionais e comportamentos de pagamento. Estas diferenças são importantes para a construção de perfis de clientes na fase de segmentação.

A análise das variáveis categóricas foi apoiada pelos seguintes gráficos:

![Frequência de Contract](../reports/figures/frequencia_Contract.png)

O gráfico da variável `Contract` permite observar a distribuição dos clientes por tipo de contrato. Esta variável é relevante porque distingue clientes com contrato mensal, anual ou bianual, podendo refletir diferentes níveis de compromisso com a empresa.

![Frequência de InternetService](../reports/figures/frequencia_InternetService.png)

O gráfico da variável `InternetService` mostra a distribuição dos clientes de acordo com o tipo de serviço de internet contratado. Esta informação é importante para diferenciar clientes sem internet, clientes com DSL e clientes com fibra ótica.

![Frequência de PaymentMethod](../reports/figures/frequencia_PaymentMethod.png)

O gráfico da variável `PaymentMethod` permite analisar os métodos de pagamento utilizados pelos clientes. Esta variável pode ajudar a identificar diferenças nos comportamentos de pagamento e na relação contratual com a empresa.

![Frequência de OnlineSecurity](../reports/figures/frequencia_OnlineSecurity.png)

O gráfico da variável `OnlineSecurity` mostra a adesão dos clientes ao serviço adicional de segurança online. Esta variável contribui para perceber o nível de subscrição de serviços complementares.

![Frequência de TechSupport](../reports/figures/frequencia_TechSupport.png)

O gráfico da variável `TechSupport` permite observar a adesão ao serviço de apoio técnico. Esta informação é relevante para distinguir clientes com maior ou menor nível de suporte contratado.

Em conjunto, estas variáveis categóricas ajudam a complementar a análise das variáveis numéricas, permitindo caracterizar melhor os diferentes perfis de clientes a identificar na fase de clustering.


### 1.2. Correlações Relevantes

A análise bivariada teve como objetivo identificar relações factuais entre variáveis críticas para a segmentação. Como não existe variável-alvo, foram analisadas relações entre atributos relevantes para a diferenciação dos clientes.

Foi gerada uma matriz de correlação com as variáveis `tenure`, `MonthlyCharges`, `TotalCharges` e `SeniorCitizen`.

#### Matriz de correlação

A análise da matriz de correlação permitiu avaliar a relação entre as principais variáveis numéricas do dataset. A correlação mais elevada foi observada entre `tenure` e `TotalCharges`, com um valor de **0,8262**. Este resultado é esperado, uma vez que clientes com maior tempo de permanência tendem a acumular encargos totais mais elevados ao longo da relação com a empresa.

A relação entre `MonthlyCharges` e `TotalCharges` também foi positiva, com uma correlação de **0,6512**. Isto indica que clientes com mensalidades mais elevadas tendem, em geral, a apresentar valores totais pagos superiores.

A correlação entre `tenure` e `MonthlyCharges` foi mais baixa, com um valor de **0,2479**, sugerindo que o tempo de permanência e o valor mensal pago não representam exatamente a mesma dimensão do comportamento do cliente. Esta observação é relevante para a segmentação, porque permite distinguir perfis diferentes, como clientes antigos com mensalidades mais baixas ou clientes recentes com mensalidades mais elevadas.

As restantes correlações com `SeniorCitizen` foram mais reduzidas. A correlação entre `MonthlyCharges` e `SeniorCitizen` foi de **0,2202**, entre `TotalCharges` e `SeniorCitizen` foi de **0,1030**, e entre `tenure` e `SeniorCitizen` foi de **0,0166**. Estes valores sugerem que esta variável demográfica, isoladamente, não apresenta uma relação linear forte com as principais variáveis de consumo e permanência.

#### Conclusões visuais principais

A análise bivariada permitiu retirar três conclusões principais. Em primeiro lugar, `tenure` e `TotalCharges` apresentam uma relação positiva forte, indicando que clientes com maior permanência tendem a acumular maior valor total. Em segundo lugar, `MonthlyCharges` e `TotalCharges` apresentam uma relação positiva moderada a forte, mostrando que clientes com encargos mensais mais altos tendem a alcançar valores acumulados superiores. Por fim, as variáveis contratuais e de serviços, como `Contract` e `InternetService`, ajudam a contextualizar a dispersão observada nos clientes e podem apoiar a identificação de perfis diferentes na fase de segmentação.

A análise bivariada foi apoiada pelos seguintes gráficos:

![Heatmap de correlação](../reports/figures/heatmap_correlacao_variaveis_numericas.png)

O heatmap de correlação resume visualmente as relações entre as variáveis numéricas analisadas. Destaca-se a correlação forte entre `tenure` e `TotalCharges`, bem como a relação positiva entre `MonthlyCharges` e `TotalCharges`.

![Scatter tenure vs TotalCharges](../reports/figures/scatter_tenure_totalcharges.png)

O gráfico de dispersão entre `tenure` e `TotalCharges` mostra que clientes com maior tempo de permanência tendem a apresentar valores totais pagos mais elevados. Esta relação reforça a importância de `tenure` para distinguir clientes recentes de clientes antigos.

![Scatter MonthlyCharges vs TotalCharges](../reports/figures/scatter_monthlycharges_totalcharges.png)

O gráfico entre `MonthlyCharges` e `TotalCharges` evidencia que clientes com mensalidades mais altas tendem a acumular valores totais superiores, embora a dispersão indique que o valor total também depende do tempo de permanência.

![Scatter tenure vs MonthlyCharges](../reports/figures/scatter_tenure_monthlycharges.png)

O gráfico entre `tenure` e `MonthlyCharges` mostra uma relação menos forte do que as anteriores. Isto sugere que a antiguidade do cliente e o valor mensal pago representam dimensões diferentes, ambas úteis para a segmentação.

![Scatter tenure vs TotalCharges por Contract](../reports/figures/scatter_tenure_totalcharges_contract.png)

Este gráfico acrescenta a variável `Contract` à relação entre `tenure` e `TotalCharges`. A sua utilidade está em perceber se diferentes tipos de contrato ajudam a explicar padrões de permanência e valor acumulado.

![Scatter MonthlyCharges vs TotalCharges por InternetService](../reports/figures/scatter_monthlycharges_totalcharges_internetservice.png)

Este gráfico permite observar a relação entre `MonthlyCharges` e `TotalCharges` considerando o tipo de serviço de internet. A variável `InternetService` ajuda a contextualizar diferenças nos encargos mensais e no valor total acumulado pelos clientes.

Em conjunto, estes gráficos mostram que as variáveis numéricas e categóricas analisadas fornecem informação complementar para a segmentação, permitindo distinguir clientes com diferentes níveis de permanência, consumo mensal, valor acumulado e características contratuais.


## 2. Qualidade dos Dados e Limpeza

### 2.1. Tratamento de Dados em Falta (Missing Data)

Foi calculada a percentagem de valores em falta por coluna. Na inspeção inicial, o método `isna()` não identificou valores nulos nas colunas originais. No entanto, foi identificado um problema específico na variável `TotalCharges`: esta coluna estava lida como texto (`object`), apesar de representar um valor monetário.

Ao converter `TotalCharges` para formato numérico com `pd.to_numeric(..., errors='coerce')`, foram identificados **11 valores problemáticos**, correspondentes a aproximadamente **0,16%** dos registos.

O cálculo da percentagem foi:

```text
11 / 7043 × 100 = 0,1562% ≈ 0,16%
```

Estes 11 valores estavam associados a clientes com `tenure = 0`. Como `tenure = 0` indica ausência de tempo de permanência, a decisão aplicada foi preencher `TotalCharges` com **0** nesses casos. Esta opção foi considerada mais coerente do que eliminar as linhas ou imputar pela média/mediana, uma vez que estes registos representam clientes reais e o valor problemático estava relacionado com a ausência de valor acumulado.

A eliminação das linhas não foi escolhida porque os 11 registos representam uma percentagem muito reduzida do dataset e não indicavam ausência generalizada de informação. Também não foi escolhida imputação pela média ou mediana, porque, quando `tenure = 0`, a interpretação mais adequada é que o cliente ainda não acumulou encargos totais. Assim, o valor `0` é mais interpretável do que um valor artificial baseado na média ou mediana dos restantes clientes.

Após o tratamento, o dataset ficou com **0 valores em falta**.

Foi definida adicionalmente uma regra geral para eventuais valores em falta futuros: em variáveis numéricas, deverá ser usado o preenchimento pela mediana, por ser menos sensível a valores extremos do que a média; em variáveis categóricas, deverá ser usado o preenchimento pela moda, por representar a categoria mais frequente.

### 2.2. Outliers e Inconsistências

Foram analisados possíveis erros e valores extremos nas variáveis numéricas mais relevantes para a segmentação: `tenure`, `MonthlyCharges` e `TotalCharges`.

Antes da análise de outliers, foi corrigido o tipo de dados de `TotalCharges`, que passou de texto para variável numérica (`float64`). Esta correção era necessária porque algoritmos de segmentação e medidas estatísticas não conseguem trabalhar corretamente com valores monetários armazenados como texto.

Na verificação de valores impossíveis, não foram identificados valores negativos nas variáveis analisadas. A variável `tenure` apresentou valores entre **0** e **72** meses, com média de **32,37** e mediana de **29**. A variável `MonthlyCharges` apresentou valores entre **18,25** e **118,75**, com média de **64,76** e mediana de **70,35**. A variável `TotalCharges` apresentou valores entre **0** e **8684,80**, com média de **2279,73** e mediana de **1394,55**.

Assim, não foram encontrados valores impossíveis do tipo `tenure < 0`, `MonthlyCharges < 0` ou `TotalCharges < 0`.

Foi também aplicado o método IQR às variáveis `tenure`, `MonthlyCharges` e `TotalCharges`. Para `tenure`, o primeiro quartil foi **9**, o terceiro quartil foi **55** e o intervalo interquartil foi **46**, resultando num limite inferior de **-60** e num limite superior de **124**. Para `MonthlyCharges`, o primeiro quartil foi **35,50**, o terceiro quartil foi **89,85** e o intervalo interquartil foi **54,35**, com limite inferior de **-46,025** e limite superior de **171,375**. Para `TotalCharges`, o primeiro quartil foi **398,55**, o terceiro quartil foi **3786,60** e o intervalo interquartil foi **3388,05**, com limite inferior de **-4683,525** e limite superior de **8868,675**.

Com base neste método, não foram identificados outliers nas três variáveis analisadas. Ainda assim, foram criadas colunas indicadoras de outliers (`tenure_outlier`, `MonthlyCharges_outlier` e `TotalCharges_outlier`) para documentar a verificação realizada. Todas ficaram com valor total igual a **0**.

Não foram removidos registos por outliers. Esta decisão foi tomada porque não foram identificados outliers pelo método IQR, os valores máximos observados são plausíveis no contexto do negócio, a remoção automática poderia eliminar clientes reais com maior permanência ou maior valor económico, e a fase de modelação utilizará escalonamento para controlar diferenças de escala entre variáveis.

A análise de outliers foi apoiada pelos seguintes gráficos:

![Boxplot de outliers tenure](../reports/figures/boxplot_outliers_tenure.png)

O boxplot de `tenure` mostra que os valores observados estão dentro de um intervalo plausível, entre clientes sem permanência acumulada e clientes com permanência elevada. Não foram identificados outliers pelo método IQR.

![Boxplot de outliers MonthlyCharges](../reports/figures/boxplot_outliers_MonthlyCharges.png)

O boxplot de `MonthlyCharges` mostra uma variação considerável nos encargos mensais, mas sem valores classificados como outliers pelo método IQR. Isto indica que os diferentes níveis de mensalidade fazem parte da variabilidade normal do dataset.

![Boxplot de outliers TotalCharges](../reports/figures/boxplot_outliers_TotalCharges.png)

O boxplot de `TotalCharges` evidencia uma dispersão elevada no valor total acumulado, o que é esperado por depender do tempo de permanência e da mensalidade. Apesar desta dispersão, não foram identificados outliers pelo método IQR.

Em conjunto, a análise de qualidade dos dados confirmou que o dataset ficou adequado para a fase de modelação, após a correção de `TotalCharges` e o tratamento dos 11 valores problemáticos.


## 3. Engenharia de Atributos (Feature Engineering)

### 3.1. Transformações Realizadas

A transformação de variáveis foi feita para preparar o dataset para algoritmos de segmentação. Como estes algoritmos trabalham com informação numérica, foi necessário converter variáveis categóricas e colocar variáveis contínuas numa escala comparável.

Foram inicialmente selecionadas **19 variáveis** alinhadas com o Objetivo SMART: `gender`, `SeniorCitizen`, `Partner`, `Dependents`, `tenure`, `Contract`, `PaperlessBilling`, `PaymentMethod`, `PhoneService`, `MultipleLines`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies`, `MonthlyCharges` e `TotalCharges`.

A variável `customerID` foi excluída por ser apenas um identificador. A variável `Churn` foi também excluída da preparação para modelação, uma vez que o projeto segue uma abordagem não supervisionada e não pretende prever abandono individual.

Foi aplicado **One-Hot Encoding** às variáveis categóricas. Esta técnica foi escolhida porque as categorias do dataset não têm uma ordem natural. Por exemplo, não faria sentido atribuir uma hierarquia artificial entre `DSL`, `Fiber optic` e `No`, ou entre os diferentes métodos de pagamento. Na primeira transformação, o dataset passou de **19 variáveis** para **45 atributos** após o One-Hot Encoding.

As variáveis numéricas `tenure`, `MonthlyCharges` e `TotalCharges` foram escalonadas com **StandardScaler**. Esta decisão foi tomada porque algoritmos de clustering baseados em distância, como o K-Means, são sensíveis à escala das variáveis. Sem escalonamento, uma variável como `TotalCharges`, que tem valores muito superiores aos de `tenure`, poderia dominar indevidamente o cálculo das distâncias. Após o escalonamento, estas variáveis ficaram centradas aproximadamente em média 0 e desvio padrão próximo de 1.

A validação final confirmou que, após a transformação inicial, não existiam colunas não numéricas, não existiam valores em falta, `Churn` não estava presente no dataset preparado e `customerID` também não estava presente. Nesta fase, o dataset transformado tinha **7043 linhas e 45 colunas**, antes da seleção final de atributos.

#### Seleção de atributos

A seleção de atributos teve como objetivo consolidar o dataset final para modelação, removendo variáveis não informativas, redundantes ou com correlação demasiado elevada.

A variável `customerID` foi removida por ser apenas um identificador e não contribuir para a segmentação. A variável `Churn` foi excluída porque o projeto é não supervisionado. No One-Hot Encoding foi usada a opção `drop_first=True`, para reduzir redundância entre categorias. Não foram identificadas colunas constantes, ou seja, não existiam atributos com apenas um valor. Foi ainda aplicado um critério de remoção por correlação elevada, usando um limiar de correlação absoluta superior a **0,90**.

Após o One-Hot Encoding com redução de redundância, o dataset tinha **7043 linhas e 33 atributos**. Depois, foi calculada uma matriz de correlação absoluta entre os atributos codificados, tendo sido removidas variáveis redundantes.

Foram removidas as variáveis `AvgChargePerTenure`, `MultipleLines_No phone service`, `InternetService_No`, `OnlineSecurity_No internet service`, `OnlineBackup_No internet service`, `DeviceProtection_No internet service`, `TechSupport_No internet service`, `StreamingTV_No internet service` e `StreamingMovies_No internet service`.

A variável `AvgChargePerTenure` foi removida por apresentar correlação elevada com `MonthlyCharges`. As restantes variáveis removidas estavam relacionadas com categorias redundantes, sobretudo associadas à ausência de serviço telefónico ou ausência de serviço de internet. Esta remoção ajudou a reduzir multicolinearidade e a simplificar a representação final dos dados.

Após esta etapa, o dataset passou de **33 atributos** para **24 atributos finais**.

Depois da seleção, foram escalonadas as variáveis contínuas `tenure`, `MonthlyCharges`, `TotalCharges` e `ServiceCount`. O atributo `AvgChargePerTenure` já não foi escalonado na versão final porque foi removido por correlação elevada.

A validação final do dataset processado confirmou que o dataset final tem **7043 linhas e 24 atributos**, não contém colunas não numéricas, não contém valores em falta, e não inclui `Churn` nem `customerID`.

A seleção de atributos foi apoiada pela seguinte matriz de correlação:

![Heatmap de feature selection](../reports/figures/heatmap_feature_selection_correlacao.png)

O heatmap de seleção de atributos permitiu identificar relações fortes entre variáveis codificadas e variáveis criadas. Esta análise foi importante para remover atributos redundantes e garantir que o dataset final usado na modelação fosse mais simples, numérico e adequado à segmentação.

### 3.2. Criação de Novos Atributos

Foram criadas três novas variáveis a partir das variáveis existentes. Embora o requisito mínimo fosse criar pelo menos duas novas variáveis, foram criadas três para enriquecer a análise de segmentação.

A variável `ServiceCount` foi criada através da soma dos serviços subscritos com valor `Yes`. O objetivo foi medir o nível de utilização de serviços por cliente. Esta variável apresentou média de **3,36**, desvio padrão de **2,06**, mínimo de **0**, mediana de **3** e máximo de **8**.

A variável `AvgChargePerTenure` foi criada a partir da divisão de `TotalCharges` por `tenure`, assumindo valor **0** quando `tenure = 0`. O objetivo foi representar o valor médio acumulado por mês de permanência. Esta variável apresentou média de **64,70**, desvio padrão de **30,27**, mínimo de **0**, mediana de **70,30** e máximo de **121,40**.

A variável `HasInternetService` foi criada com valor **1** quando `InternetService` era diferente de `No`, e valor **0** quando o cliente não tinha serviço de internet. O objetivo foi distinguir de forma simples clientes com e sem serviço de internet. Esta variável apresentou média de **0,78**, desvio padrão de **0,41**, mínimo de **0**, mediana de **1** e máximo de **1**.

Não foram identificados valores em falta nas novas variáveis.

Como o projeto não tem variável-alvo, a utilidade das novas variáveis foi avaliada através da sua relação com variáveis críticas para a segmentação. A variável `ServiceCount` mostrou relação relevante com `MonthlyCharges` e `TotalCharges`, o que faz sentido, uma vez que clientes com mais serviços subscritos tendem a pagar mais por mês e a acumular maior valor total. A correlação entre `MonthlyCharges` e `ServiceCount` foi de **0,8023**, e a correlação entre `TotalCharges` e `ServiceCount` foi de **0,7959**.

A variável `AvgChargePerTenure` apresentou correlação muito elevada com `MonthlyCharges`, com valor de **0,9944**. Por esse motivo, apesar de ter sido criada e analisada, foi posteriormente removida na fase de seleção de atributos por redundância. Também apresentou correlação relevante com `ServiceCount`, com valor de **0,7974**.

A variável `HasInternetService` apresentou relação relevante com `MonthlyCharges`, com correlação de **0,7636**, e com `AvgChargePerTenure`, com correlação de **0,7585**. Apesar disso, foi mantida na versão final porque resume de forma simples a distinção entre clientes com e sem serviço de internet. A relação entre `tenure` e `ServiceCount` foi de **0,5236**, indicando uma associação positiva moderada entre permanência e número de serviços subscritos.

#### Relação com variáveis categóricas relevantes

Foram também calculadas médias das novas variáveis por categorias de `Contract`, `InternetService` e `PaymentMethod`.

Por tipo de contrato, os clientes com contrato **Month-to-month** apresentaram `ServiceCount` médio de **2,84**, `AvgChargePerTenure` médio de **66,38** e `HasInternetService` médio de **0,86**. Os clientes com contrato de **One year** apresentaram `ServiceCount` médio de **3,82**, `AvgChargePerTenure` médio de **65,06** e `HasInternetService` médio de **0,75**. Já os clientes com contrato de **Two year** apresentaram `ServiceCount` médio de **4,17**, `AvgChargePerTenure` médio de **60,54** e `HasInternetService` médio de **0,62**. Assim, os clientes com contrato de dois anos apresentaram, em média, maior número de serviços subscritos.

Por tipo de serviço de internet, os clientes com **DSL** apresentaram `ServiceCount` médio de **3,67**, `AvgChargePerTenure` médio de **57,98** e `HasInternetService` médio de **1,00**. Os clientes com **Fiber optic** apresentaram `ServiceCount` médio de **4,18**, `AvgChargePerTenure` médio de **91,46** e `HasInternetService` médio de **1,00**. Os clientes sem serviço de internet apresentaram `ServiceCount` médio de **1,22**, `AvgChargePerTenure` médio de **21,05** e `HasInternetService` médio de **0,00**. Estes resultados indicam que clientes com fibra ótica apresentam maior intensidade de serviços e maior valor económico médio.

Por método de pagamento, os clientes com **Bank transfer (automatic)** apresentaram `ServiceCount` médio de **3,85**, `AvgChargePerTenure` médio de **67,09** e `HasInternetService` médio de **0,78**. Os clientes com **Credit card (automatic)** apresentaram `ServiceCount` médio de **3,88**, `AvgChargePerTenure` médio de **66,48** e `HasInternetService` médio de **0,78**. Os clientes com **Electronic check** apresentaram `ServiceCount` médio de **3,47**, `AvgChargePerTenure` médio de **76,26** e `HasInternetService` médio de **0,95**. Por fim, os clientes com **Mailed check** apresentaram `ServiceCount` médio de **2,26**, `AvgChargePerTenure` médio de **43,76** e `HasInternetService` médio de **0,54**.

Os clientes com `Electronic check` apresentaram maior média de `AvgChargePerTenure` e maior proporção de clientes com serviço de internet. Esta observação pode ser útil para a interpretação dos segmentos na Milestone 3, mas não deve ser interpretada como relação causal.

A análise dos novos atributos foi apoiada pelos seguintes gráficos:

![Heatmap novos atributos](../reports/figures/heatmap_novos_atributos_variaveis_criticas.png)

O heatmap dos novos atributos permitiu avaliar a relação entre as variáveis criadas e as variáveis críticas para segmentação. Destaca-se a forte associação entre `AvgChargePerTenure` e `MonthlyCharges`, o que justificou a remoção posterior de `AvgChargePerTenure` por redundância.

![ServiceCount vs MonthlyCharges](../reports/figures/scatter_servicecount_monthlycharges.png)

O gráfico entre `ServiceCount` e `MonthlyCharges` mostra que clientes com maior número de serviços subscritos tendem a apresentar encargos mensais mais elevados. Esta relação reforça a utilidade de `ServiceCount` para diferenciar perfis de clientes.

![AvgChargePerTenure vs MonthlyCharges](../reports/figures/scatter_avgchargepertenure_monthlycharges.png)

O gráfico entre `AvgChargePerTenure` e `MonthlyCharges` evidencia uma relação muito forte entre as duas variáveis. Por esse motivo, `AvgChargePerTenure` foi útil para análise exploratória, mas foi removida da versão final por redundância.

![ServiceCount por Contract](../reports/figures/boxplot_servicecount_contract.png)

O boxplot de `ServiceCount` por tipo de contrato permite comparar o número de serviços subscritos entre clientes com contratos mensais, anuais e bianuais. Esta análise ajuda a perceber se o tipo de contrato está associado a diferentes níveis de utilização de serviços.

Em conjunto, as variáveis criadas enriqueceram a análise exploratória e apoiaram a construção de uma representação mais informativa para a segmentação de clientes.


## 4. Dicionário de Dados Final (Pós-Processamento)

A tabela seguinte apresenta os atributos finais entregues à fase de modelação.

| Atributo                                | Tipo                | Descrição                                                        |
| :-------------------------------------- | :------------------ | :--------------------------------------------------------------- |
| `SeniorCitizen`                         | Binário             | Indica se o cliente é sénior: 1 = sim, 0 = não.                  |
| `tenure`                                | Numérico escalonado | Tempo de permanência do cliente, após StandardScaler.            |
| `MonthlyCharges`                        | Numérico escalonado | Encargo mensal do cliente, após StandardScaler.                  |
| `TotalCharges`                          | Numérico escalonado | Encargo total acumulado, após correção de tipo e StandardScaler. |
| `ServiceCount`                          | Numérico escalonado | Número de serviços subscritos pelo cliente, após StandardScaler. |
| `HasInternetService`                    | Binário             | 1 = cliente tem serviço de internet; 0 = não tem.                |
| `gender_Male`                           | Binário             | Resultado do One-Hot Encoding da variável `gender`.              |
| `Partner_Yes`                           | Binário             | Indica se o cliente tem parceiro/a.                              |
| `Dependents_Yes`                        | Binário             | Indica se o cliente tem dependentes.                             |
| `Contract_One year`                     | Binário             | Indica contrato de um ano.                                       |
| `Contract_Two year`                     | Binário             | Indica contrato de dois anos.                                    |
| `PaperlessBilling_Yes`                  | Binário             | Indica faturação digital.                                        |
| `PaymentMethod_Credit card (automatic)` | Binário             | Indica pagamento por cartão de crédito automático.               |
| `PaymentMethod_Electronic check`        | Binário             | Indica pagamento por cheque eletrónico.                          |
| `PaymentMethod_Mailed check`            | Binário             | Indica pagamento por cheque enviado por correio.                 |
| `PhoneService_Yes`                      | Binário             | Indica se o cliente tem serviço telefónico.                      |
| `MultipleLines_Yes`                     | Binário             | Indica se o cliente tem múltiplas linhas.                        |
| `InternetService_Fiber optic`           | Binário             | Indica serviço de internet por fibra ótica.                      |
| `OnlineSecurity_Yes`                    | Binário             | Indica subscrição de segurança online.                           |
| `OnlineBackup_Yes`                      | Binário             | Indica subscrição de backup online.                              |
| `DeviceProtection_Yes`                  | Binário             | Indica subscrição de proteção de dispositivo.                    |
| `TechSupport_Yes`                       | Binário             | Indica subscrição de suporte técnico.                            |
| `StreamingTV_Yes`                       | Binário             | Indica subscrição de streaming TV.                               |
| `StreamingMovies_Yes`                   | Binário             | Indica subscrição de streaming de filmes.                        |

### Variáveis removidas

| Variável                         | Motivo                                                                      |
| :------------------------------- | :-------------------------------------------------------------------------- |
| `customerID`                     | Identificador sem valor analítico para clustering.                          |
| `Churn`                          | Excluída por o projeto ser não supervisionado.                              |
| `AvgChargePerTenure`             | Correlação elevada com `MonthlyCharges`.                                    |
| Variáveis `No internet service`  | Redundantes com ausência de serviço de internet e com `HasInternetService`. |
| `MultipleLines_No phone service` | Redundante com informação de serviço telefónico.                            |

## 5. Conclusões da Fase de Exploração

A Milestone 2 permitiu aprofundar a compreensão estatística do dataset e preparar os dados para a fase de modelação.

As principais conclusões foram:

1. **As variáveis `tenure`, `MonthlyCharges` e `TotalCharges` são relevantes para a diferenciação de clientes.** `TotalCharges` apresentou a maior dispersão relativa e está fortemente correlacionada com `tenure`.

2. **A variável `TotalCharges` exigiu correção de tipo.** Inicialmente estava lida como texto, apesar de representar valores monetários. Após conversão para numérico, foram identificados 11 valores problemáticos associados a `tenure = 0`, que foram tratados com preenchimento por 0.

3. **Não foram identificados outliers pelo método IQR nas principais variáveis numéricas.** Também não foram encontrados valores negativos ou incoerentes em `tenure`, `MonthlyCharges` e `TotalCharges`.

4. **Foram criados novos atributos relevantes para a segmentação.** `ServiceCount`, `AvgChargePerTenure` e `HasInternetService` permitiram explorar dimensões agregadas de serviços e valor económico.

5. **A seleção de atributos reduziu redundância.** A variável `AvgChargePerTenure` foi removida por correlação muito elevada com `MonthlyCharges`, e várias categorias “No internet service” foram removidas por redundância.

6. **O dataset final está pronto para a Milestone 3.** A versão final contém 7043 linhas e 24 atributos numéricos, sem valores em falta, sem identificadores e sem `Churn` como variável-alvo.

Assim, os dados estão preparados para a fase de modelação não supervisionada, onde serão testados algoritmos de clustering e avaliada a capacidade de identificar 3 perfis de clientes estatisticamente caracterizáveis.

### Rastreabilidade dos artefactos

A implementação técnica desta Milestone encontra-se no notebook:

* `notebooks/2.0_exploracao.ipynb`

Os ficheiros principais resultantes da preparação dos dados são:

* `data/processed/telco_customer_churn_m2_final_processado.csv`;
* `data/processed/lista_atributos_finais_m2.csv`;
* `data/processed/atributos_removidos_m2.csv`.

As figuras utilizadas ao longo deste relatório encontram-se na pasta:

* `reports/figures/`.

---

*Data de última atualização: 14/06/2026*
