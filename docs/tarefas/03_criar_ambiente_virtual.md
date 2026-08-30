# 03 — Criar o ambiente virtual local

## Objetivo

Isolar as dependências Python em `.venv` na raiz do projeto.

## Dependências

Tarefa 02.

## Procedimento

1. Confirmar uma versão suportada de Python no computador alvo.
2. Executar `python -m venv .venv` a partir da raiz.
3. Ativar com `.\.venv\Scripts\Activate.ps1` no PowerShell.
4. Atualizar o `pip` dentro do ambiente recém-criado.

## Critério de aceite

O interpretador ativo pertence a `.venv` e `python --version` funciona sem erro.
