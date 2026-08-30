# 20 — Inicializar componentes de treino

## Objetivo

Criar modelo, critério, otimizador e histórico a partir da configuração.

## Dependências

Tarefas 05, 06 e 19.

## Procedimento

1. Mover a MLP ao `device` escolhido.
2. Instanciar `nn.CrossEntropyLoss` como critério inicial.
3. Instanciar `torch.optim.AdamW` com `LEARNING_RATE` e `WEIGHT_DECAY`.
4. Criar histórico com as chaves `train_loss`, `val_loss`, `val_acc` e `val_f1`.
5. Registrar a configuração efetiva no início da execução.

## Critério de aceite

Todos os parâmetros treináveis estão no dispositivo correto e foram registrados no otimizador.
