# 29 — Validar recarga para inferência

## Objetivo

Comprovar que artefatos salvos fazem previsões sem repetir o treinamento.

## Dependências

Tarefa 28.

## Procedimento

1. Criar rotina para carregar pré-processador, metadados e checkpoint.
2. Reconstruir a MLP a partir dos metadados e carregar o `state_dict` no dispositivo selecionado.
3. Selecionar linhas de exemplo com o esquema original do dataset.
4. Transformar entradas apenas com `transform` e executar inferência em `eval()`.
5. Converter `argmax` na classe prevista e registrar o resultado.

## Critério de aceite

Um novo processo produz previsões para entradas válidas usando só os artefatos persistidos.
