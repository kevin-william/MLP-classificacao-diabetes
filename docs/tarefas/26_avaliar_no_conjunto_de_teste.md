# 26 — Avaliar o melhor modelo no conjunto de teste

## Objetivo

Produzir a avaliação final sem usar o teste durante a seleção do modelo.

## Dependências

Tarefas 17, 24 e 25.

## Procedimento

1. Confirmar que o melhor checkpoint foi restaurado.
2. Executar inferência no loader de teste em modo `eval()` e sem gradientes.
3. Calcular loss, acurácia, precision, recall e F1 da classe positiva.
4. Gerar `classification_report` e matriz de confusão com scikit-learn.
5. Salvar as métricas estruturadas em `artifacts/`.

## Critério de aceite

O projeto gera relatório de teste completo e nenhum valor de teste influencia arquitetura, pesos ou número de épocas.
