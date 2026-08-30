# 31 — Testar execução em CPU

## Objetivo

Garantir que o fallback para CPU funciona de ponta a ponta.

## Dependências

Tarefa 25.

## Procedimento

1. Forçar `device="cpu"` por configuração de teste ou mock de disponibilidade CUDA.
2. Executar poucas épocas e, se necessário, um subconjunto explicitamente identificado como teste rápido.
3. Validar loaders, forward, treino, checkpoint, avaliação e artefatos.
4. Conferir a mensagem de uso de CPU no log.

## Critério de aceite

O fluxo completo termina em CPU sem operação exclusiva de CUDA e produz os artefatos esperados.
