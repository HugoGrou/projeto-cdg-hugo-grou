# Milestone 3: Modelação e Avaliação

## 1. Estratégia de Modelação

Nesta milestone foi desenvolvida a fase de **modelação e avaliação** do projeto, seguindo a lógica da metodologia CRISP-DM. Como o objetivo do trabalho é construir um **modelo descritivo de segmentação de clientes**, a abordagem adotada foi **não supervisionada**, recorrendo a algoritmos de clustering.

O objetivo SMART definido para o projeto consiste em construir, até **14/06/2026**, um modelo descritivo de segmentação de clientes com base no conjunto de dados **Telco Customer Churn**, utilizando variáveis demográficas, contratuais, de serviços subscritos e de consumo, de modo a identificar **3 perfis de clientes estatisticamente caracterizáveis**, garantindo uma solução final com **Coeficiente de Silhueta médio igual ou superior a 0,24** e com cada perfil descrito através de pelo menos cinco variáveis relevantes.

Por este motivo, a variável `Churn` não foi utilizada como variável-alvo e não foi desenvolvido um modelo de classificação. O foco desta fase foi identificar grupos de clientes com características semelhantes, sem ensinar o modelo a prever uma classe previamente conhecida.

### Preparação dos dados para modelação

O dataset utilizado na modelação foi o dataset final preparado na Milestone 2, após as etapas de limpeza, transformação, criação de novos atributos e seleção de variáveis.

No início da Milestone 3, o notebook confirmou que o dataset de modelação tinha **7043 observações** e **24 variáveis**, sem valores em falta e apenas com variáveis numéricas após transformação. Também foi confirmada a ausência das variáveis `Churn` e `customerID`.

A remoção de `Churn` foi essencial para manter o caráter não supervisionado do projeto. A remoção de `customerID` também foi necessária, uma vez que esta variável funciona apenas como identificador e não tem valor analítico para a segmentação.

### Divisão do dataset

Embora o problema seja não supervisionado, foi feita uma divisão do dataset em treino e teste para avaliar a estabilidade dos agrupamentos em diferentes subconjuntos de dados.

A divisão usada foi de aproximadamente **80% para treino** e **20% para teste**, correspondendo a **5634 observações no conjunto de treino** e **1409 observações no conjunto de teste**.

Esta divisão não teve como objetivo prever uma variável-alvo, mas sim comparar a qualidade dos agrupamentos em amostras diferentes e verificar se os resultados eram consistentes.

### Métricas de sucesso

Como se trata de clustering, a avaliação foi feita com métricas internas de coesão e separação dos grupos.

A métrica principal foi o **Silhouette Score**, porque permite avaliar se os clientes estão mais próximos dos elementos do seu próprio cluster do que dos elementos dos outros clusters. Valores mais elevados indicam melhor separação entre grupos. Esta métrica foi especialmente importante porque o Objetivo SMART definiu como critério mínimo um valor médio de Silhouette igual ou superior a **0,24**.

Foram também utilizadas métricas complementares. O **Davies-Bouldin Index** foi usado para avaliar a separação entre clusters, sendo preferíveis valores mais baixos. O **Calinski-Harabasz Score** foi usado para avaliar a relação entre a separação entre clusters e a coesão interna dos grupos, sendo preferíveis valores mais elevados. No caso do K-Means, foi ainda analisada a **inércia**, que mede a compactação interna dos clusters. Por fim, foi considerada a percentagem mínima por cluster, para garantir que a solução não criava grupos residuais ou pouco representativos.

---

## 2. Experiências Realizadas

### 2.1. Modelo Baseline

O modelo baseline foi construído com o algoritmo **K-Means**, por ser um algoritmo simples, conhecido e adequado como ponto de partida para problemas de clustering.

Apesar de o K-Means permitir testar diferentes números de clusters, foi usado **k = 3**, porque o Objetivo SMART do projeto define a identificação de **3 perfis de clientes**. Assim, o baseline foi construído já com o mesmo número de grupos pretendido para a solução final.

No conjunto de treino, o baseline obteve **Silhouette de 0,2151**, **Davies-Bouldin de 1,6238**, **Calinski-Harabasz de 2187,4128** e **inércia de 25631,3821**. No conjunto de teste, obteve **Silhouette de 0,2194**, **Davies-Bouldin de 1,5860**, **Calinski-Harabasz de 547,2395** e **inércia de 6431,5630**.

No dataset completo, o K-Means baseline com 3 clusters obteve **Silhouette de 0,2161**, **Davies-Bouldin de 1,6154**, **Calinski-Harabasz de 2734,0298** e **inércia de 32059,2893**.

A distribuição global dos clusters do baseline foi relativamente equilibrada: o Cluster 0 reuniu **2171 clientes** (**30,82%**), o Cluster 1 reuniu **2265 clientes** (**32,16%**) e o Cluster 2 reuniu **2607 clientes** (**37,02%**).

Apesar desta distribuição equilibrada, o valor de Silhouette ficou abaixo do mínimo de **0,24** definido no objetivo SMART. Por esse motivo, foi necessário continuar a experimentação com outros modelos e configurações.

### Figura 1 — Distribuição dos clusters do baseline

![Distribuição dos clusters do baseline](../reports/figures/m3_baseline_kmeans_dimensao_clusters.png)

Esta figura apresenta a dimensão dos três clusters obtidos pelo modelo baseline. A distribuição é relativamente equilibrada, sem clusters residuais. No entanto, o equilíbrio na dimensão dos grupos não garante, por si só, uma boa separação entre eles.

### Figura 2 — Visualização PCA do baseline

![PCA do baseline K-Means](../reports/figures/m3_baseline_kmeans_pca_2d.png)

A visualização PCA projeta os dados em duas componentes principais. No baseline, a variância explicada acumulada pelas duas primeiras componentes foi de aproximadamente **0,5983**. A figura permite observar a distribuição dos grupos num espaço bidimensional, mas não mostra uma separação muito forte entre clusters, o que está de acordo com o Silhouette relativamente baixo.

---

### 2.2. Modelos Candidatos

Após o baseline, foram testados vários modelos candidatos para verificar se era possível melhorar a qualidade da segmentação.

Foram executadas **43 experiências iniciais**, distribuídas por **K-Means**, **MiniBatch K-Means**, **Agglomerative Clustering** e **DBSCAN**. O K-Means foi usado como algoritmo de particionamento de referência. O MiniBatch K-Means foi testado como variante mais eficiente do K-Means. O Agglomerative Clustering foi incluído para testar uma abordagem hierárquica. O DBSCAN foi testado por ser um algoritmo baseado em densidade.

Nos resultados iniciais, os melhores desempenhos no conjunto de teste surgiram com modelos baseados em K-Means. O K-Means com `k=3`, `init=k-means++` e `n_init=10` obteve **Silhouette de 0,2194** e **Davies-Bouldin de 1,5860**. A configuração equivalente com `n_init=20` apresentou o mesmo resultado. O MiniBatch K-Means com `k=3` e `batch_size=1024` obteve **Silhouette de 0,2191**, ficando muito próximo do K-Means.

Os modelos hierárquicos apresentaram valores de Silhouette inferiores. O Agglomerative Clustering com `k=3` e `linkage=average` obteve **Silhouette de 0,2025**, enquanto a configuração com `linkage=ward` obteve **0,1985**. O DBSCAN não apresentou uma solução válida e competitiva nas configurações testadas.

O melhor modelo candidato inicial foi, portanto, o **K-Means com 3 clusters**, com **Silhouette de 0,2194** no conjunto de teste. No entanto, este resultado continuou abaixo do valor mínimo de **0,24** definido no Objetivo SMART.

### Figura 3 — Comparação dos modelos candidatos

![Comparação dos modelos candidatos](../reports/figures/m3_comparacao_modelos_candidatos_silhouette.png)

Este gráfico compara os principais modelos candidatos através do Silhouette Score. A análise mostra que K-Means e MiniBatch K-Means obtiveram os melhores resultados iniciais, mas sem melhoria suficiente face ao objetivo quantitativo definido.

### Figura 4 — Método do Cotovelo

![Método do Cotovelo para K-Means](../reports/figures/m3_elbow_method_kmeans.png)

O Método do Cotovelo foi usado como apoio visual para analisar a evolução da inércia em função do número de clusters. Esta figura ajuda a perceber se existe um ponto em que o aumento do número de clusters deixa de trazer uma redução significativa da inércia. No entanto, como o objetivo do projeto define **3 perfis**, a decisão final não foi baseada apenas na inércia, mas também no alinhamento com o SMART e nas métricas de coesão e separação.

---

## 3. Otimização dos Modelos

### 3.1. Otimização inicial do K-Means

Na primeira fase de otimização, foi realizada uma pesquisa manual de hiperparâmetros para o K-Means, com validação cruzada manual.

Foram testadas **64 configurações** de K-Means, variando parâmetros como `n_clusters`, `init`, `n_init`, `max_iter`, `algorithm` e `random_state`.

A validação cruzada foi feita com **5 folds**, permitindo calcular a média e o desvio-padrão das métricas entre diferentes partições dos dados.

A melhor configuração K-Means com 3 clusters foi definida com `n_clusters=3`, `init="random"`, `n_init=20`, `max_iter=300`, `algorithm="elkan"` e `random_state=42`.

Em validação cruzada, esta configuração obteve **Silhouette médio de 0,2159**, com **desvio-padrão de 0,0049**, e **Davies-Bouldin médio de 1,6129**. O desvio-padrão reduzido indica alguma estabilidade entre folds, mas a melhoria face ao baseline não foi material.

No dataset completo, o K-Means otimizado manteve praticamente o mesmo desempenho do baseline, com **Silhouette de 0,2161**, **Davies-Bouldin de 1,6155**, **Calinski-Harabasz de 2734,0301** e **inércia de 32059,3038**.

Assim, esta fase serviu sobretudo para confirmar que o K-Means com 3 clusters era relativamente estável, mas limitado na capacidade de separar os clientes de forma suficientemente clara.

### Figura 5 — Estabilidade das configurações K-Means

![Estabilidade das configurações K-Means](../reports/figures/m3_kmeans_cross_validation_top_configuracoes.png)

Este gráfico mostra a estabilidade das melhores configurações testadas em validação cruzada. Os valores de Silhouette são próximos entre si, o que sugere que a alteração dos hiperparâmetros do K-Means não foi suficiente para melhorar significativamente a segmentação.

### Figura 6 — Comparação baseline vs K-Means otimizado

![Comparação baseline vs otimizado](../reports/figures/m3_comparacao_baseline_vs_otimizado_silhouette.png)

A figura confirma visualmente que o K-Means otimizado não apresentou melhoria material em relação ao K-Means baseline. Ambos os modelos ficaram com Silhouette de aproximadamente **0,2161**.

### Figura 7 — Curva de estabilidade do K-Means por tamanho de amostra

![Curva de estabilidade K-Means](../reports/figures/m3_curva_estabilidade_kmeans.png)

Esta curva avalia a estabilidade do modelo com diferentes frações do conjunto de treino. O Silhouette manteve-se próximo de **0,219** nas diferentes frações, o que sugere estabilidade, mas também confirma que o K-Means não atingiu o nível mínimo pretendido no Objetivo SMART.

---

### 3.2. Otimização avançada dos modelos candidatos

Como o K-Means otimizado não atingiu o valor mínimo de Silhouette definido no objetivo, foi realizada uma etapa de otimização avançada.

Nesta fase foram testadas novas famílias de modelos e novas representações dos dados, incluindo K-Means com grelha alargada, MiniBatch K-Means, Bisecting K-Means, Gaussian Mixture Models, BIRCH, variantes com PCA e uma variante com variáveis numéricas e atributos de engenharia.

Modelos como **Spectral Clustering**, **OPTICS** e **HDBSCAN** foram considerados, mas não integraram a comparação final da procura rápida devido ao maior custo computacional no Kaggle.

Para reduzir o tempo de execução, a otimização avançada foi feita em duas etapas. Primeiro, foi criado um ranking inicial numa amostra de até **3000 observações**. Depois, os melhores modelos foram avaliados no dataset completo.

Foram usadas várias variantes do espaço de atributos, incluindo `Atual_M2`, `Atual_M2_PCA80`, `Atual_M2_PCA90` e `Numericas_Engenharia`.

A variante `Numericas_Engenharia` apresentou os melhores resultados. Esta melhoria sugere que uma representação mais simples e focada em variáveis numéricas e atributos de engenharia reduziu ruído e melhorou a separação entre segmentos.

O melhor modelo global encontrado foi um **Gaussian Mixture Model com 2 clusters**, aplicado à variante `Numericas_Engenharia`, com **Silhouette de 0,4377**, **Davies-Bouldin de 0,8396**, **Calinski-Harabasz de 7232,9524** e cluster mínimo de **31,55%**. Apesar de apresentar o melhor desempenho global, este modelo não foi escolhido como solução final, porque o Objetivo SMART do projeto define a identificação de **3 perfis de clientes**.

O melhor modelo alinhado com o Objetivo SMART foi um **Gaussian Mixture Model com 3 clusters**, também aplicado à variante `Numericas_Engenharia`. Este modelo obteve **Silhouette de 0,3947**, **Davies-Bouldin de 0,9626**, **Calinski-Harabasz de 7142,2309** e cluster mínimo de **29,62%**.

A configuração final selecionada foi `GaussianMixture` com `covariance_type="spherical"`, `n_components=3`, `n_init=5` e `random_state=42`.

Este modelo foi escolhido porque respeita o objetivo de identificar 3 perfis de clientes, ultrapassa claramente o valor mínimo de Silhouette definido no SMART, apresenta clusters com dimensão equilibrada, melhora substancialmente o desempenho do K-Means inicial e otimizado, e mantém uma segmentação interpretável.

Em comparação com o K-Means otimizado, cuja Silhouette foi **0,2161**, o Gaussian Mixture Model com 3 clusters obteve uma melhoria de **0,1786** na Silhouette. O modelo de 2 clusters foi mantido apenas como referência comparativa, uma vez que tinha melhor métrica global, mas não cumpria a estrutura definida no objetivo do projeto.

### Figura 8 — Top 15 modelos da otimização avançada

![Top 15 otimização avançada](../reports/figures/m3_top15_otimizacao_avancada_silhouette.png)

Esta figura apresenta os 15 melhores modelos da otimização avançada segundo o Silhouette Score. Observa-se que os melhores resultados surgem com a variante `Numericas_Engenharia`, o que reforça a importância da seleção e transformação de atributos na qualidade da segmentação.

---

## 4. Avaliação do Modelo Final

O modelo final selecionado foi um **Gaussian Mixture Model**, usando a variante de dados `Numericas_Engenharia`, com **3 clusters**, `covariance_type="spherical"`, `n_init=5` e `random_state=42`.

Este modelo obteve **Silhouette de 0,3947**, **Davies-Bouldin de 0,9626**, **Calinski-Harabasz de 7142,2309** e cluster mínimo de **29,62%**.

A avaliação final foi feita com base no modelo escolhido, usando `X_modelo_final` e `labels_modelo_final`, de modo a garantir coerência entre a decisão final, os gráficos e as estatísticas finais.

### Distribuição dos clusters finais

A distribuição dos clusters finais foi equilibrada. O Cluster 0 reuniu **2086 clientes**, correspondendo a **29,62%** do total. O Cluster 1 reuniu **2298 clientes**, correspondendo a **32,63%**. O Cluster 2 reuniu **2659 clientes**, correspondendo a **37,75%**.

Como o menor cluster representa **29,62%** dos clientes, não existem clusters residuais. Isto indica que os três grupos encontrados têm dimensão suficiente para serem interpretados como segmentos de negócio.

### 4.1. Análise de Coesão e Separação dos Clusters

Como o problema é não supervisionado, não existe matriz de confusão nem erros de previsão no sentido tradicional. Em vez disso, a avaliação foi feita através da análise da coesão e separação dos grupos.

O Silhouette médio final calculado no gráfico de silhueta foi aproximadamente **0,3949**. Este valor é muito próximo do valor registado no ranking final da otimização avançada, que foi **0,3947**. A pequena diferença pode resultar de arredondamentos ou da forma de cálculo/amostragem usada em cada etapa do notebook.

O resultado final supera claramente o objetivo mínimo definido no SMART:

```text
Silhouette objetivo mínimo: 0,24
Silhouette final: 0,3947
Diferença: 0,3947 - 0,24 = 0,1547
```

Assim, o modelo final cumpre o critério quantitativo do objetivo.

### Figura 9 — Silhouette Plot do modelo final

![Silhouette Plot do modelo final](../reports/figures/m3_silhouette_plot_modelo_final.png)

O Silhouette Plot permite avaliar a qualidade dos clusters individualmente. Quanto mais elevados forem os valores de Silhouette, melhor é a atribuição dos clientes ao respetivo cluster. O valor médio de aproximadamente **0,3949** indica uma separação superior à obtida com o K-Means inicial, embora não perfeita. Isto significa que os grupos têm estrutura interpretável, mas ainda existe alguma proximidade entre segmentos.

### Figura 10 — Visualização PCA do modelo final

![PCA do modelo final](../reports/figures/m3_pca_modelo_final.png)

A visualização PCA projeta os clientes em duas componentes principais. No modelo final, as duas primeiras componentes explicaram aproximadamente **90,5%** da variância acumulada, com **0,6967** na primeira componente e **0,2083** na segunda componente.

Esta projeção permite observar a separação dos três segmentos num espaço bidimensional. Como a variância acumulada é elevada, a visualização PCA é uma representação útil da estrutura dos dados usada pelo modelo final.

---

## 4.2. Perfil dos Segmentos

A caracterização dos clusters foi feita com base nos dados originais tratados na Milestone 2, para tornar a interpretação dos segmentos mais próxima do contexto de negócio.

### Cluster 0 — Clientes com baixo consumo e menor utilização de serviços

O Cluster 0 representa **2086 clientes**, correspondendo a **29,62%** do total.

Este grupo apresenta `MonthlyCharges` médio baixo, com valor de **25,52**, `ServiceCount` médio baixo, com valor de **1,25**, e `TotalCharges` médio de **689,62**. O `tenure` médio é de **27,61** e o `AvgChargePerTenure` médio é de **25,47**.

Além disso, este segmento apresenta forte presença de clientes sem serviço de Internet, maior peso de pagamentos por `mailed check` e maior proporção de contratos `month-to-month`, embora também existam clientes com contratos mais longos.

Este grupo pode ser interpretado como um segmento de clientes com menor intensidade de utilização dos serviços, custos mensais baixos e menor valor acumulado. Do ponto de vista de negócio, representa clientes de baixo valor mensal, potencialmente mais simples do ponto de vista contratual e tecnológico.

### Cluster 1 — Clientes antigos, com maior consumo e maior subscrição de serviços

O Cluster 1 representa **2298 clientes**, correspondendo a **32,63%** do total.

Este grupo apresenta o maior `tenure` médio, com **57,29**, o maior `MonthlyCharges` médio, com **89,79**, o maior `TotalCharges` médio, com **5127,99**, e o maior `ServiceCount` médio, com **5,56**. O `AvgChargePerTenure` médio é de **89,85**.

Este segmento apresenta maior presença de clientes com múltiplos serviços, maior peso de contratos de longa duração e maior utilização de métodos de pagamento automáticos.

Este grupo pode ser interpretado como o segmento de clientes mais antigos, com maior envolvimento com a empresa, maior consumo mensal e maior número de serviços contratados. É provavelmente o segmento de maior valor comercial.

### Cluster 2 — Clientes recentes com encargos mensais elevados

O Cluster 2 representa **2659 clientes**, correspondendo a **37,75%** do total.

Este grupo apresenta o menor `tenure` médio, com **14,57**, mas tem um `MonthlyCharges` médio elevado, com **73,92**. O `TotalCharges` médio é relativamente baixo, com **1065,63**, devido ao menor tempo de permanência. O `ServiceCount` médio é intermédio, com **3,12**, e o `AvgChargePerTenure` médio é de **73,74**.

Este segmento apresenta maior presença de clientes com serviço de Internet e maior peso de contratos `month-to-month`.

Este grupo pode ser interpretado como um segmento de clientes mais recentes, com encargos mensais relativamente elevados, mas ainda com baixo valor acumulado. Pode ser um segmento importante para ações de acompanhamento inicial e gestão da relação com o cliente.

### Figura 11 — Perfil dos segmentos

![Perfil dos segmentos](../reports/figures/m3_perfil_segmentos_variaveis_numericas.png)

O gráfico de perfil dos segmentos compara as principais variáveis numéricas dos clusters numa escala normalizada. A figura mostra que o Cluster 0 tem valores baixos em mensalidade, número de serviços e valor acumulado; o Cluster 1 apresenta os valores mais elevados em praticamente todas as variáveis de consumo e permanência; e o Cluster 2 combina baixa permanência com mensalidade elevada.

Esta figura é importante porque traduz os resultados estatísticos do clustering em perfis interpretáveis de negócio.

---

### 4.3. Variáveis que mais distinguem os clusters

As variáveis diferenciadoras foram identificadas através dos desvios das médias de cada cluster face à média global.

No Cluster 0, as variáveis mais relevantes foram `MonthlyCharges`, `ServiceCount`, `TotalCharges`, `HasInternetService` e `tenure`, indicando clientes com baixo consumo, poucos serviços e menor valor acumulado.

No Cluster 1, as variáveis mais relevantes foram `TotalCharges`, `ServiceCount`, `tenure`, `MonthlyCharges` e `HasInternetService`, indicando clientes antigos, com muitos serviços e elevado valor acumulado.

No Cluster 2, as variáveis mais relevantes foram `tenure`, `TotalCharges`, `MonthlyCharges`, `HasInternetService` e `ServiceCount`, indicando clientes recentes, com mensalidade elevada, mas menor valor acumulado.

Esta análise confirma que os três perfis são caracterizáveis por pelo menos cinco variáveis relevantes, tal como definido no Objetivo SMART.

---

## 5. Conclusão da Fase de Modelação

A fase de modelação permitiu comparar diferentes estratégias de clustering e selecionar um modelo final coerente com o objetivo do projeto.

Inicialmente, o K-Means baseline com 3 clusters obteve um Silhouette de **0,2161** no dataset completo. Este valor ficou abaixo do mínimo definido no Objetivo SMART. A otimização do K-Means, mesmo com validação cruzada e pesquisa de hiperparâmetros, não gerou melhoria material, mantendo o Silhouette em **0,2161**.

A fase de otimização avançada permitiu testar novas famílias de modelos e novas representações dos dados. O melhor modelo global encontrado foi um Gaussian Mixture Model com 2 clusters, com Silhouette de **0,4377**. No entanto, este modelo não foi escolhido como solução final porque não respeitava o objetivo de identificar **3 perfis de clientes**.

O modelo final selecionado foi o **Gaussian Mixture Model com 3 clusters**, aplicado à variante `Numericas_Engenharia`, com **Silhouette de 0,3947**, **Davies-Bouldin de 0,9626**, **Calinski-Harabasz de 7142,2309** e cluster mínimo de **29,62%**.

Este modelo cumpre o Objetivo SMART, porque identifica **3 perfis de clientes**, supera o valor mínimo de Silhouette definido e permite caracterizar cada perfil através de várias variáveis relevantes.

### Resposta à questão crítica da Milestone 3

A questão crítica desta milestone é perceber se o modelo é fiável e se resolve o problema definido.

A resposta é **parcialmente positiva**. O modelo final é adequado como solução descritiva de segmentação, porque apresenta melhor separação dos grupos do que o baseline, cumpre o critério quantitativo definido e gera segmentos interpretáveis para apoiar decisões de gestão comercial e relacionamento com clientes.

No entanto, é importante realçar que este modelo **não prevê abandono de clientes**. O modelo identifica perfis de clientes com características semelhantes. Qualquer utilização posterior para decisões de retenção deve ser feita como apoio exploratório e não como previsão direta de churn.

### Limitações

A principal limitação é o facto de o modelo ser não supervisionado. Por esse motivo, não existe uma variável-alvo que permita validar se os clusters correspondem diretamente a risco de abandono ou a outro resultado concreto de negócio.

Outra limitação está relacionada com a interpretação dos clusters, que depende das variáveis disponíveis no dataset. Caso existissem variáveis adicionais, como satisfação do cliente, histórico de reclamações ou contactos com o apoio técnico, os segmentos poderiam ser mais ricos do ponto de vista de negócio.

A variante final `Numericas_Engenharia` usa uma representação mais reduzida dos dados, o que melhorou a separação entre clusters, mas pode deixar de fora alguma informação categórica. Esta decisão representa um compromisso entre desempenho técnico, simplicidade e interpretabilidade.

A validação cruzada explícita foi aplicada inicialmente ao K-Means. A escolha final do Gaussian Mixture Model foi baseada na otimização avançada e na avaliação no dataset completo. Caso seja necessário reforçar esta fase, poderá ser acrescentada uma validação K-Fold específica para o Gaussian Mixture Model final.

### Decisão final

A decisão final foi selecionar o seguinte modelo:

```text
GaussianMixture
Variante: Numericas_Engenharia
Nº de clusters: 3
covariance_type: spherical
n_init: 5
random_state: 42
```

Este modelo será usado como base para a fase seguinte do projeto, onde os perfis obtidos poderão ser convertidos em conclusões, recomendações de negócio e propostas de ação.

---

*Data de última atualização: 12/06/2026*
