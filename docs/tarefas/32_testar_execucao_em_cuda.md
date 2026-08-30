# 32 — Testar execução em CUDA quando disponível

## Objetivo

Confirmar que GPU compatível é detectada e utilizada corretamente.

## Dependências

Tarefas 05 e 25.

## Procedimento

1. Executar em máquina com `torch.cuda.is_available()` verdadeiro.
2. Conferir no log o dispositivo e o nome da GPU.
3. Verificar que modelo, atributos e rótulos são movidos para CUDA nos loops.
4. Confirmar que `pin_memory` está habilitado nos loaders apropriados.
5. Concluir treino e avaliação sem erro de dispositivo misto.

## Critério de aceite

A execução usa CUDA de ponta a ponta e gera os mesmos tipos de artefato da execução em CPU.
