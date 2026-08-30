# 01 — Criar a estrutura de diretórios

## Objetivo

Criar a estrutura base prevista no plano, preservando o dataset existente.

## Dependências

Nenhuma.

## Procedimento

1. Criar `src/` para os módulos Python.
2. Criar `artifacts/` para checkpoints, métricas e gráficos.
3. Adicionar `src/__init__.py` para tornar o diretório um pacote Python.
4. Manter `dataset/` exclusivamente para os dados de entrada.

## Critério de aceite

`src/`, `artifacts/` e `dataset/` existem, e o CSV permanece em `dataset/diabetes_prediction_dataset.csv`.
