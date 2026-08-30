# 24 — Adicionar checkpoint e early stopping

## Objetivo

Salvar o melhor estado de validação e interromper treino sem melhoria.

## Dependências

Tarefas 06 e 23.

## Procedimento

1. Monitorar a métrica configurada, inicialmente `val_loss` com menor valor como melhor resultado.
2. Ao melhorar, salvar `state_dict`, época, métricas e configuração no checkpoint.
3. Reiniciar o contador de estagnação após cada melhoria.
4. Interromper quando o contador atingir a paciência.
5. Restaurar o melhor `state_dict` antes de retornar do treinamento.

## Critério de aceite

Existe checkpoint do melhor resultado de validação e o modelo retornado já usa os pesos desse checkpoint.
