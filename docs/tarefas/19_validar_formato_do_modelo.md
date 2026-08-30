# 19 — Validar o formato de entrada e saída da MLP

## Objetivo

Detectar incompatibilidades de dimensão, tipo ou dispositivo antes do treino completo.

## Dependências

Tarefas 17 e 18.

## Procedimento

1. Instanciar a MLP com `in_dim` igual à dimensão transformada na tarefa 15.
2. Mover modelo e um lote para o dispositivo selecionado.
3. Executar forward e verificar a forma `[tamanho_do_lote, NUM_CLASSES]`.
4. Confirmar que os logits são finitos.
5. Calcular uma perda de teste com `CrossEntropyLoss` e `yb`.

## Critério de aceite

Forward e cálculo de perda ocorrem sem erro de dimensão, tipo de dado ou mistura de dispositivos.
