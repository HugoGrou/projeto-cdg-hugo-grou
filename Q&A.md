# Q&A — Perguntas Frequentes sobre o Projeto

## Projeto: Segmentação de Clientes Telco Customer Churn

Este ficheiro reúne perguntas e respostas técnicas que podem ser usadas na preparação do pitch final e na defesa do projeto. O objetivo é antecipar dúvidas sobre a metodologia, o modelo final, as métricas, as limitações e o valor prático da solução.

---

## 1. Porque é que o projeto não usou `Churn` como variável-alvo?

O projeto foi definido como um problema **descritivo e não supervisionado**, focado em segmentação de clientes. Por isso, o objetivo não era prever se um cliente iria abandonar a empresa, mas sim identificar grupos de clientes com características semelhantes.

A variável `Churn` foi analisada no contexto exploratório, mas não foi usada como alvo de previsão. Usá-la como variável-alvo transformaria o projeto num problema de classificação supervisionada, o que não estaria alinhado com o objetivo SMART definido na Milestone 1.

---

## 2. Então o modelo consegue prever se um cliente vai abandonar a empresa?

Não. O modelo final **não prevê churn individual**.

A solução construída identifica **perfis de clientes** com base em características demográficas, contratuais, de serviços subscritos e de consumo. O resultado permite compreender melhor a estrutura da base de clientes, mas não deve ser interpretado como uma previsão direta de abandono.

Para prever churn seria necessário desenvolver outro projeto, com aprendizagem supervisionada, usando `Churn` como variável-alvo e métricas adequadas, como F1-Score, Recall, Precision ou AUC-ROC.

---

## 3. Porque foi usada uma abordagem de clustering?

Foi usada uma abordagem de **clustering** porque o objetivo era segmentar clientes sem usar uma variável-alvo. O clustering permite agrupar clientes com características semelhantes e descobrir padrões que não são imediatamente visíveis através de uma simples análise descritiva.

Esta abordagem é adequada quando se pretende responder a perguntas como:

* Que tipos de clientes existem na base de dados?
* Que características diferenciam os grupos?
* Como podem estes grupos apoiar decisões comerciais?

---

## 4. Qual foi o modelo final escolhido?

O modelo final escolhido foi um **Gaussian Mixture Model** com **3 clusters**, aplicado à variante de dados baseada em variáveis numéricas e variáveis de engenharia.

A configuração final obteve:

| Métrica                 | Resultado |
| :---------------------- | --------: |
| Número de clusters      |         3 |
| Coeficiente de Silhueta |    0,3947 |
| Davies-Bouldin Index    |    0,9626 |
| Calinski-Harabasz Score | 7142,2309 |
| Cluster mínimo          |    29,62% |

Estes valores devem ser atualizados caso mudem após uma execução final completa do notebook.

---

## 5. O objetivo SMART foi cumprido?

Sim, de acordo com os resultados finais obtidos no notebook.

O objetivo SMART exigia:

* construir um modelo descritivo de segmentação;
* identificar **3 perfis de clientes**;
* obter um Coeficiente de Silhueta médio igual ou superior a **0,24**;
* caracterizar cada perfil com pelo menos cinco variáveis relevantes;
* apoiar decisões de gestão comercial e relacionamento com clientes.

O modelo final identificou **3 clusters** e obteve uma Silhouette de **0,3947**, acima do mínimo definido.

Diferença face ao limiar mínimo:

```text
0,3947 - 0,24 = 0,1547
```

Assim, o critério quantitativo definido no objetivo foi superado.

---

## 6. O que significa uma Silhouette de 0,3947?

O Coeficiente de Silhueta mede a qualidade da separação entre clusters. De forma simples, avalia se os clientes estão mais próximos dos elementos do seu próprio grupo do que dos elementos de outros grupos.

Uma Silhouette de **0,3947** indica que existe uma separação aceitável entre os grupos para uma análise descritiva. Não significa que os clusters estejam perfeitamente separados, mas mostra que existe estrutura suficiente nos dados para criar perfis interpretáveis.

---

## 7. Porque é que não foi escolhido o modelo com 2 clusters se tinha Silhouette superior?

Durante a otimização, foi identificado um modelo com 2 clusters e Silhouette superior. No entanto, esse modelo não foi escolhido porque não cumpria o objetivo SMART, que exigia a identificação de **3 perfis de clientes**.

A escolha final equilibrou três critérios:

1. cumprimento do objetivo definido inicialmente;
2. qualidade da segmentação;
3. interpretabilidade dos perfis encontrados.

Por isso, foi selecionado o melhor modelo que respeitava a condição de ter 3 clusters.

---

## 8. Quais foram os três perfis encontrados?

Foram identificados três perfis principais:

| Cluster   | Interpretação resumida                                                            |
| :-------- | :-------------------------------------------------------------------------------- |
| Cluster 0 | Clientes com baixo consumo, poucos serviços e menor valor económico               |
| Cluster 1 | Clientes antigos, com maior valor acumulado e maior número de serviços subscritos |
| Cluster 2 | Clientes recentes, com mensalidade elevada e valor acumulado ainda reduzido       |

Estes perfis ajudam a perceber que a base de clientes não é homogénea e que diferentes grupos podem exigir estratégias comerciais diferentes.

---

## 9. Que variáveis ajudaram a caracterizar os perfis?

As variáveis mais importantes para interpretar os segmentos foram sobretudo:

* `tenure`;
* `MonthlyCharges`;
* `TotalCharges`;
* `ServiceCount`;
* `AvgChargePerTenure`;
* `HasInternetService`;
* `SeniorCitizen`.

Também foram usadas variáveis categóricas para enriquecer a interpretação dos perfis, como `Contract`, `PaymentMethod`, `InternetService`, `OnlineSecurity`, `TechSupport`, `StreamingTV` e `StreamingMovies`.

---

## 10. Porque foram criadas variáveis de engenharia?

As variáveis de engenharia foram criadas para resumir melhor comportamentos relevantes dos clientes.

Por exemplo:

* `ServiceCount` ajuda a representar o número de serviços subscritos;
* `HasInternetService` distingue clientes com e sem serviço de internet;
* `AvgChargePerTenure` ajuda a interpretar a relação entre encargos e antiguidade.

Estas variáveis facilitam a leitura dos perfis e tornam a segmentação mais interpretável.

---

## 11. Que valor prático tem esta segmentação?

A segmentação permite apoiar decisões comerciais mais direcionadas.

Exemplos:

* clientes com baixo consumo podem receber campanhas simples de adesão a serviços adicionais;
* clientes antigos e de maior valor podem ser alvo de ações de fidelização;
* clientes recentes com mensalidades elevadas podem beneficiar de acompanhamento inicial e comunicação clara sobre os serviços contratados.

Assim, o projeto transforma dados em conhecimento útil para gestão comercial e relacionamento com clientes.

---

## 12. Quais são as principais limitações do projeto?

As principais limitações são:

* o modelo não prevê churn individual;
* os clusters não provam relações de causalidade;
* os resultados dependem das variáveis disponíveis no dataset;
* não existem variáveis como satisfação do cliente, reclamações, região, campanhas recebidas ou histórico detalhado de contactos;
* a Silhouette indica separação aceitável, mas não perfeita;
* os perfis devem ser validados com conhecimento de negócio antes de serem usados em contexto real.

---

## 13. Existem riscos éticos na utilização deste modelo?

Sim. Embora o projeto use dados estruturados e não utilize identificadores pessoais na modelação, qualquer segmentação de clientes deve ser usada com cuidado.

O modelo não deve ser usado para discriminar clientes, limitar acesso a serviços ou aplicar condições comerciais injustas. A segmentação deve servir para melhorar comunicação, acompanhamento e adequação de propostas, mantendo supervisão humana e transparência.

A variável `SeniorCitizen`, por representar uma característica demográfica, deve ser interpretada com especial cuidado.

---

## 14. Como é que outra pessoa pode reproduzir os resultados?

Para reproduzir os resultados, deve:

1. aceder ao repositório GitHub do projeto;
2. consultar o `README.md` para perceber a estrutura do projeto;
3. abrir os notebooks na ordem indicada;
4. garantir que as bibliotecas necessárias estão instaladas através do `requirements.txt`;
5. executar o notebook de modelação do início ao fim;
6. confirmar que os resultados obtidos coincidem com os valores reportados em `docs/M3_modelacao.md` e `docs/M4_conclusoes.md`.

Caso os resultados mudem após nova execução, os ficheiros de documentação devem ser atualizados para manter coerência entre código, métricas e conclusões.

---

## 15. Que melhorias poderiam ser feitas no futuro?

Algumas melhorias futuras seriam:

1. recolher novas variáveis, como satisfação, reclamações, região, campanhas recebidas e histórico de contactos;
2. testar outros algoritmos de clustering, como HDBSCAN, OPTICS ou abordagens hierárquicas adicionais;
3. validar os segmentos com conhecimento de negócio;
4. criar uma aplicação em Streamlit para carregar novos dados e atribuir clientes aos perfis;
5. desenvolver um dashboard em Power BI para facilitar a interpretação dos segmentos;
6. monitorizar os clusters ao longo do tempo para verificar se continuam estáveis.

---

## Conclusão

Este projeto não deve ser visto como um sistema de previsão de churn, mas sim como uma solução descritiva de segmentação. O principal contributo foi identificar três perfis de clientes estatisticamente caracterizáveis e transformar os resultados técnicos em conhecimento útil para apoiar decisões de gestão comercial e relacionamento com clientes.
