# 22 — Implementar uma época de validação

## Objetivo

Medir desempenho sem calcular gradientes ou alterar os pesos.

## Dependências

Tarefas 17 e 20.

## Procedimento

1. Colocar o modelo em modo `eval()`.
2. Percorrer os lotes dentro de `torch.no_grad()`.
3. Calcular a perda média ponderada.
4. Obter a previsão de classe por `logits.argmax(dim=1)`.
5. Acumular rótulos e previsões para calcular acurácia e F1 da classe positiva.

## Critério de aceite

A rotina retorna `val_loss`, `val_acc` e `val_f1`, não chama `backward` e não modifica parâmetros.
