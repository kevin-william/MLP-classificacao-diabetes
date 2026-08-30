# 23 — Orquestrar loop de épocas e histórico

## Objetivo

Repetir treino e validação pelo número configurado de épocas, mantendo histórico consistente.

## Dependências

Tarefas 06, 21 e 22.

## Procedimento

1. Criar `train` ou `treinar` em `src/train.py`.
2. Em cada época, chamar uma vez a rotina de treino e uma vez a de validação.
3. Adicionar as métricas retornadas ao histórico na mesma posição.
4. Exibir periodicamente época, perdas, acurácia e F1 de validação.
5. Retornar o histórico ao encerrar.

## Critério de aceite

Há uma entrada de cada métrica por época executada, e os logs permitem acompanhar a convergência.
