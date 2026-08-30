# 28 — Persistir pré-processador e metadados

## Objetivo

Permitir inferência futura com a mesma transformação e arquitetura do treino.

## Dependências

Tarefas 15, 24 e 25.

## Procedimento

1. Serializar o `ColumnTransformer` ajustado com ferramenta adequada, como `joblib`.
2. Salvar no checkpoint `state_dict`, `in_dim`, `hidden_dims`, `num_classes` e `dropout`.
3. Salvar configuração efetiva, semente e versões de bibliotecas em JSON ou texto.
4. Não depender de serializar o objeto inteiro do modelo como única estratégia de recarga.

## Critério de aceite

Os artefatos permitem reconstruir a MLP, carregar os pesos e transformar novas entradas.
