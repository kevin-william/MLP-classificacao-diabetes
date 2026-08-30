# 33 — Validar execução reproduzível e entregáveis

## Objetivo

Executar a checagem final de todos os critérios do plano.

## Dependências

Tarefas 26 a 32.

## Procedimento

1. Rodar o treinamento duas vezes com mesma semente e configuração.
2. Comparar tamanho das partições, histórico e métricas, considerando pequenas variações CUDA documentadas.
3. Confirmar checkpoint, pré-processador, metadados, métricas, relatório e gráficos em `artifacts/`.
4. Executar a rotina de inferência com os artefatos de uma das execuções.
5. Registrar versões de Python, PyTorch e dispositivo nos testes.

## Critério de aceite

Todos os entregáveis existem, a inferência é reproduzível pelos artefatos e a execução está comprovada em CPU e, se houver GPU, em CUDA.
