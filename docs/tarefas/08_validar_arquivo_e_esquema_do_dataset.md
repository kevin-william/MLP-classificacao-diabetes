# 08 — Validar o arquivo e o esquema do dataset

## Objetivo

Falhar cedo e com mensagem clara se o CSV estiver ausente ou incompatível.

## Dependências

Tarefa 06.

## Procedimento

1. Criar em `src/data.py` uma função de leitura.
2. Verificar a existência de `dataset/diabetes_prediction_dataset.csv` antes da leitura.
3. Carregar o CSV com `pandas`.
4. Conferir `gender`, `age`, `hypertension`, `heart_disease`, `smoking_history`, `bmi`, `HbA1c_level`, `blood_glucose_level` e `diabetes`.
5. Informar quais colunas obrigatórias faltam e quais foram encontradas, quando houver incompatibilidade.

## Critério de aceite

Um CSV válido é carregado e arquivo inexistente ou coluna ausente produz exceção explicativa antes do treinamento.
