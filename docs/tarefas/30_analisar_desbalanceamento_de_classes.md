# 30 — Analisar desbalanceamento de classes

## Objetivo

Determinar se acurácia é suficiente para avaliar o classificador de diabetes.

## Dependências

Tarefas 09 e 26.

## Procedimento

1. Comparar a proporção de positivos em treino e teste.
2. Avaliar precision, recall e F1 da classe positiva em conjunto com acurácia.
3. Registrar a conclusão em um relatório de experimento.
4. Caso recall ou F1 não atendam ao objetivo definido, calcular pesos de classe exclusivamente a partir de `y_train`.
5. Executar experimento separado com `CrossEntropyLoss(weight=...)` e comparar os resultados, preservando o baseline.

## Critério de aceite

A decisão sobre pesos de classe é fundamentada em métricas além da acurácia e não usa teste para calcular os pesos.
