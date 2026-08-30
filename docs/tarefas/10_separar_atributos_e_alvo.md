# 10 — Separar atributos e alvo

## Objetivo

Criar a matriz de preditores `X` e o vetor de rótulos `y` sem vazamento do alvo.

## Dependências

Tarefa 09.

## Procedimento

1. Remover `diabetes` de `X` e mantê-la como vetor unidimensional `y`.
2. Definir explicitamente os atributos categóricos `gender` e `smoking_history`.
3. Definir como numéricos `age`, `hypertension`, `heart_disease`, `bmi`, `HbA1c_level` e `blood_glucose_level`.
4. Verificar se todas as colunas de `X` estão presentes em uma única lista de transformação.

## Critério de aceite

`X` não possui `diabetes`, `y` só possui essa variável e toda coluna preditora tem tratamento definido.
