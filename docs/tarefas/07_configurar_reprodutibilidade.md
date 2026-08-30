# 07 — Configurar reprodutibilidade

## Objetivo

Controlar todas as fontes de aleatoriedade usadas pelo treinamento.

## Dependências

Tarefa 06.

## Procedimento

1. Criar `set_seed(seed)` em módulo apropriado.
2. Inicializar os geradores de `random`, `numpy` e `torch`.
3. Inicializar os geradores CUDA quando estiverem disponíveis.
4. Configurar opções determinísticas do cuDNN quando compatíveis e documentar o eventual custo de desempenho.
5. Executar essa função antes da divisão dos dados e da criação da MLP.

## Critério de aceite

Execuções com a mesma semente produzem a mesma divisão dos dados, sem fonte aleatória não controlada.
