# 09 — Validar alvo e qualidade básica

## Objetivo

Confirmar que o problema é binário e identificar problemas de qualidade antes do pré-processamento.

## Dependências

Tarefa 08.

## Procedimento

1. Verificar se `diabetes` possui valores ausentes ou fora de `{0, 1}`.
2. Registrar quantidade de linhas, tipos, nulos por coluna e distribuição do alvo.
3. Definir uma política explícita para atributos ausentes: rejeitar o dataset ou imputar valores de forma documentada.

## Critério de aceite

Nenhum rótulo inválido segue para o treinamento e o diagnóstico básico consta no log ou relatório.
