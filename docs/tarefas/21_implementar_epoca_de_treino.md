# 21 — Implementar uma época de treino

## Objetivo

Atualizar os parâmetros da MLP percorrendo todos os lotes de treino.

## Dependências

Tarefas 17 e 20.

## Procedimento

1. Colocar o modelo em modo `train()`.
2. Transferir atributos e rótulos de cada lote ao dispositivo.
3. Executar `zero_grad`, forward, perda, `backward` e `optimizer.step`.
4. Acumular `loss.item() * tamanho_do_lote`.
5. Dividir o acumulado pelo total de exemplos de treino.
6. Usar transferência não bloqueante quando CUDA e `pin_memory` estiverem ativos.

## Critério de aceite

A rotina retorna uma perda média ponderada e modifica ao menos um parâmetro da rede.
