# 📉 Previsão de Churn em Telecomunicações com Machine Learning

## 1. O Problema de Negócio
Reter clientes atuais é drasticamente mais barato do que adquirir novos. Neste projeto, o objetivo foi construir um modelo preditivo para identificar clientes de uma empresa de telecomunicações que apresentam alto risco de cancelar seus serviços (Churn). Com essa previsão, o time de marketing e retenção pode agir preventivamente oferecendo incentivos personalizados, evitando a perda de receita recorrente.

## 2. Análise Exploratória e Insights Clave
Durante o desenvolvimento, identificou-se que a base de dados apresentava um forte desbalanceamento: cerca de 73.5% dos clientes eram da classe "Não Churn" contra 26.5% da classe "Churn".

Ao analisar as características dos clientes, dois insights de negócio principais foram encontrados:

* **O tipo de contrato é decisivo:** Clientes com contrato mês a mês (Month-to-month) possuem uma taxa de cancelamento massivamente maior do que clientes com contratos anuais ou bianuais. Incentivar a migração para planos de longo prazo é uma estratégia direta de retenção.

![Churn por Contrato](churn_por_contrato.png)

* **O risco é maior no início:** A maior densidade de cancelamentos ocorre nos primeiros meses de relacionamento do cliente com a empresa (Tenure entre 0 e 12 meses). Estratégias de onboarding e suporte dedicado no início da jornada são fundamentais.

![Churn por Tempo](churn_por_tempo.png)

## 3. Solução Técnica e Avaliação do Modelo

Na primeira tentativa, utilizei o algoritmo **Random Forest Classifier** básico. Os resultados obtidos na base de teste (1.409 clientes) foram:

* **Acurácia Geral:** 80%
* **Precisão para Churn (Classe 1):** 66%
* **Recall para Churn (Classe 1):** 47%

### Tentativa de Otimização (Pesos Balanceados)
Identificando que o modelo falhava em detectar mais da metade dos clientes em risco de saída (Recall de 47%), apliquei o parâmetro `class_weight='balanced'` para tentar penalizar os erros da classe minoritária. 

No entanto, o comportamento do algoritmo se manteve estável, mantendo o **Recall em 47%** e a **Precisão em 68%**. Isso demonstra que, para este conjunto de dados específico, apenas balancear o peso interno das árvores de decisão não foi suficiente para mover o limiar de decisão do modelo.

## 4. Próximos Passos (Próximas Sprints do Projeto)
Como cientista de dados focado no negócio, sei que manter o Recall baixo significa perder dinheiro deixando clientes irem embora. Por isso, as próximas etapas planejadas para este repositório são:

1. **Balanceamento de Dados Avançado (SMOTE):** Utilizar a biblioteca `imblearn` para gerar dados sintéticos dos clientes que deram Churn, equilibrando a base antes do treino.
2. **Ajuste de Limiar de Decisão (Threshold Tuning):** Modificar manualmente o ponto de corte da probabilidade do modelo (mudar de 0.5 para 0.3, por exemplo) para priorizar o Recall em detrimento da Precisão.
3. **Mudança de Algoritmo:** Implementar o **XGBoost** ou **LightGBM**, algoritmos baseados em gradiente que costumam performar melhor em cenários tabulares complexos e desbalanceados.
