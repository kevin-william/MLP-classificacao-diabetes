# 14 — Compor o pré-processador único

## Objetivo

Unir codificação categórica e padronização numérica em objeto reutilizável.

## Dependências

Tarefas 12 e 13.

## Procedimento

1. Criar um `ColumnTransformer` com os dois transformadores.
2. Declarar explicitamente o tratamento de colunas não listadas, por exemplo `remainder="drop"`.
3. Criar função que retorne atributos densos em `float32`.
4. Verificar que a ordem e o número das colunas de saída são estáveis.

## Critério de aceite

Um único objeto transforma todas as colunas de entrada exigidas pela MLP.
