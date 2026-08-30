# 11 — Dividir dados em treino, validação e teste

## Objetivo

Criar partições independentes para ajuste, seleção e avaliação final.

## Dependências

Tarefas 06, 07 e 10.

## Procedimento

1. Separar o teste por divisão estratificada usando `TEST_SIZE` e a semente configurada.
2. Dividir o restante, também de forma estratificada, em treino e validação.
3. Ajustar as proporções para que o resultado final respeite a configuração global, como 70%/15%/15%.
4. Registrar tamanhos e proporção de positivos nas três partições.

## Critério de aceite

Treino, validação e teste não compartilham linhas, respeitam as proporções configuradas e preservam aproximadamente a distribuição de `diabetes`.
