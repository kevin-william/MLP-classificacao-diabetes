# 16 — Transformar validação e teste

## Objetivo

Aplicar em validação e teste a mesma representação ajustada no treino.

## Dependências

Tarefa 15.

## Procedimento

1. Executar apenas `transform` em `X_val` e `X_test`.
2. Converter a saída para matriz densa se for necessária.
3. Converter atributos para `numpy.float32`.
4. Confirmar que as três partições têm o mesmo número de atributos transformados.

## Critério de aceite

Treino, validação e teste têm dimensões compatíveis; validação e teste não recalculam categorias ou estatísticas.
