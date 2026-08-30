# 18 — Implementar a classe MLP configurável

## Objetivo

Criar a arquitetura neural flexível definida no plano.

## Dependências

Tarefa 06.

## Procedimento

1. Criar `src/model.py` e a classe `MLP(nn.Module)`.
2. Receber `in_dim`, `hidden_dims`, `num_classes` e `dropout` no construtor.
3. Para cada dimensão oculta, criar o bloco `Linear → BatchNorm1d → ReLU → Dropout`.
4. Acrescentar uma última `Linear(prev_dim, num_classes)`.
5. Implementar `forward` retornando os logits de `self.net(x)`.

## Critério de aceite

Com `hidden_dims=[128, 64, 32]`, a classe possui três blocos ocultos e saída linear com duas posições, sem `sigmoid` ou `softmax` final.
