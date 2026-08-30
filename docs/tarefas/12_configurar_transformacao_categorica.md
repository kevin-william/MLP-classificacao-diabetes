# 12 — Configurar transformação categórica

## Objetivo

Preparar codificação segura para `gender` e `smoking_history`.

## Dependências

Tarefa 10.

## Procedimento

1. Instanciar `OneHotEncoder(handle_unknown="ignore")`.
2. Configurar saída densa ou conversão posterior, pois a MLP usa tensores densos.
3. Não ajustar o codificador nesta tarefa.
4. Manter sua configuração para serialização e inferência futura.

## Critério de aceite

O codificador é aplicado somente às colunas categóricas e categorias novas não causam erro durante `transform`.
