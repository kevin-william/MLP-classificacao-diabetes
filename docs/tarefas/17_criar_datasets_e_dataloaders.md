# 17 — Criar TensorDatasets e DataLoaders

## Objetivo

Preparar lotes com formato e tipos corretos para o PyTorch.

## Dependências

Tarefas 05, 11 e 16.

## Procedimento

1. Converter atributos para `torch.float32` e rótulos para `torch.long`.
2. Criar um `TensorDataset` para cada partição.
3. Criar loaders usando `BATCH_SIZE` da configuração.
4. Usar `shuffle=True` somente no treino.
5. Ativar `pin_memory` somente quando CUDA estiver disponível.
6. Inspecionar um lote e validar tipos e formatos.

## Critério de aceite

Os três loaders entregam lotes compatíveis com `CrossEntropyLoss`, e apenas o loader de treino embaralha exemplos.
