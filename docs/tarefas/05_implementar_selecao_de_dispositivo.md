# 05 — Implementar seleção de CUDA com fallback para CPU

## Objetivo

Centralizar a escolha de hardware sem tornar CUDA obrigatória.

## Dependências

Tarefa 04.

## Procedimento

1. Criar função ou constante baseada em `torch.cuda.is_available()`.
2. Retornar `torch.device("cuda")` quando disponível e `torch.device("cpu")` nos demais casos.
3. Registrar no início da execução o dispositivo selecionado.
4. Se CUDA estiver ativa, registrar também o nome da GPU, a versão CUDA do PyTorch e a quantidade de dispositivos, quando possível.

## Critério de aceite

O fluxo inicia em máquina sem GPU e torna explícito no log se está usando CPU ou CUDA.
