# 15 — Ajustar o pré-processador somente no treino

## Objetivo

Evitar vazamento de estatísticas e categorias de validação ou teste.

## Dependências

Tarefas 11 e 14.

## Procedimento

1. Aplicar `fit_transform` exclusivamente em `X_train`.
2. Registrar a dimensão final dos atributos transformados como `in_dim` do modelo.
3. Guardar o pré-processador já ajustado para persistência.
4. Revisar o código para garantir que não existam chamadas `fit` ou `fit_transform` para validação ou teste.

## Critério de aceite

Há uma única etapa de ajuste do pré-processador, executada apenas nos dados de treino.
