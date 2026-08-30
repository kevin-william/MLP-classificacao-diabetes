# 06 — Criar configuração centralizada

## Objetivo

Criar `src/config.py` como fonte única dos hiperparâmetros e caminhos.

## Dependências

Tarefa 01.

## Procedimento

1. Declarar a semente e caminhos do CSV, de `artifacts/` e do checkpoint.
2. Declarar frações de treino, validação e teste e validá-las como soma igual a 1,0.
3. Declarar `BATCH_SIZE`, `EPOCHS`, `LEARNING_RATE` e `WEIGHT_DECAY`.
4. Declarar `HIDDEN_DIMS`, `DROPOUT`, `NUM_CLASSES` e intervalo de log.
5. Declarar métrica monitorada e paciência de early stopping.

## Critério de aceite

Os módulos de dados e treinamento não duplicam hiperparâmetros definidos em `src/config.py`.
