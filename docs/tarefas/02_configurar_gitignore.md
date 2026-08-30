# 02 — Configurar arquivos ignorados pelo Git

## Objetivo

Evitar versionar ambiente local e resultados gerados.

## Dependências

Tarefa 01.

## Procedimento

1. Criar ou atualizar `.gitignore` na raiz.
2. Ignorar `.venv/`, `__pycache__/`, `*.pyc` e `.pytest_cache/`.
3. Ignorar o conteúdo de `artifacts/`; usar `.gitkeep` se for necessário preservar a pasta vazia.
4. Não ignorar `dataset/`, `src/` ou `docs/`.

## Critério de aceite

Ambiente virtual e artefatos aparecem como ignorados, enquanto o código, a documentação e o CSV continuam rastreáveis.
