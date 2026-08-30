# 04 — Definir as dependências reproduzíveis

## Objetivo

Registrar as bibliotecas necessárias para executar o projeto em outro ambiente.

## Dependências

Tarefa 03.

## Procedimento

1. Criar `requirements.txt` com `pandas`, `numpy`, `scikit-learn`, `matplotlib` e `seaborn` em versões compatíveis.
2. Documentar separadamente a instalação de PyTorch quando ela usar um índice CUDA específico.
3. Registrar a combinação conhecida `torch==2.13.0+cu130`, sem impedir uma instalação PyTorch compatível para CPU.
4. Instalar as dependências no `.venv` e validar todos os imports.

## Critério de aceite

Um ambiente virtual limpo consegue instalar as dependências documentadas e importar todas as bibliotecas usadas pelo projeto.
