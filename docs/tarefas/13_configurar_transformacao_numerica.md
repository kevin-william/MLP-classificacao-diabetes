# 13 — Configurar transformação numérica

## Objetivo

Padronizar os atributos numéricos sem tocar no alvo.

## Dependências

Tarefa 10.

## Procedimento

1. Instanciar `StandardScaler` para os seis atributos numéricos definidos.
2. Incorporar a política de ausências escolhida na tarefa 09, se necessária.
3. Não chamar `fit` nesta tarefa.

## Critério de aceite

O escalonador recebe somente atributos numéricos e nunca a coluna `diabetes`.
