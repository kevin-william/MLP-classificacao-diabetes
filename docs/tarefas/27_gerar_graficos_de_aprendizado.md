# 27 — Gerar gráficos de aprendizado

## Objetivo

Visualizar as métricas registradas durante o treinamento.

## Dependências

Tarefas 23 e 25.

## Procedimento

1. Criar função de plotagem que receba o histórico.
2. Gerar curva de perdas de treino e validação por época.
3. Gerar curva de acurácia de validação e, se registrada, de F1.
4. Adicionar título, eixos, legenda e grade legíveis.
5. Salvar as imagens em `artifacts/`, sem depender de interface gráfica.

## Critério de aceite

Após uma execução, `artifacts/` contém gráficos legíveis e consistentes com o histórico salvo.
