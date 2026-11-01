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
Utilizei o algoritmo **Random Forest Classifier** por sua robustez e capacidade de lidar com múltiplas variáveis categóricas e numéricas. Os resultados obtidos na base de teste (1.409 clientes) foram:

* **Acurácia Geral:** 80% — O modelo classifica corretamente 8 em cada 10 clientes.
* **Precisão para Churn (Classe 1):** 66% — Quando o modelo faz uma previsão de cancelamento, a assertividade é de 66%.
* **Recall para Churn (Classe 1):** 47% — O modelo identificou corretamente 47% dos clientes que de fato cancelaram.

**Análise Crítica:** Embora a acurácia geral seja alta (80%), o modelo ainda falha em detectar mais da metade dos clientes em risco de saída (Recall de 47%). Isso ocorre porque o algoritmo tende a se especializar na classe majoritária (clientes que permanecem). Para o negócio, perder um Churn real custa mais caro do que gerar um alarme falso, tornando o aumento do Recall a nossa prioridade número um.

## 4. Próximos Passos (Melhorias Futuras)
Para evoluir o projeto e torná-lo ainda mais estratégico para o negócio, os próximos passos práticos incluem:
* **Balanceamento de Dados:** Aplicar técnicas de reamostragem ou ajustar o parâmetro de pesos das classes para forçar o modelo a aprender melhor as características dos clientes que cancelam.
* **Otimização de Hiperparâmetros:** Utilizar tuning para ajustar os parâmetros das árvores de decisão.
* **Testar Modelos de Boosting:** Implementar algoritmos avançados como XGBoost ou LightGBM.
