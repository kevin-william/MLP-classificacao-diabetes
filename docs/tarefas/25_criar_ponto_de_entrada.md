# 25 — Criar o ponto de entrada do treinamento

## Objetivo

Orquestrar o fluxo completo por meio de `main.py`.

## Dependências

Tarefas 05 a 24.

## Procedimento

1. Aplicar semente e selecionar o dispositivo.
2. Carregar, validar, dividir e transformar o dataset.
3. Criar loaders, modelo, critério e otimizador.
4. Rodar treinamento com checkpoint e early stopping.
5. Entregar melhor modelo, histórico, dados de teste e pré-processador às rotinas posteriores.
6. Proteger a chamada com `if __name__ == "__main__":`.

## Critério de aceite

`python main.py` executa o fluxo de preparação e treino sem chamadas manuais a módulos internos.
