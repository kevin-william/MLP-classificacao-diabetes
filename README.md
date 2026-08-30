# MLP para classificação de diabetes

## Instalação

No PowerShell, crie e ative o ambiente virtual:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
pip install -r requirements-cuda.txt # RTX 3050 / CUDA 13.0
```

Para uma máquina sem GPU, substitua a última linha por
`pip install -r requirements-cpu.txt`. O código escolhe CUDA automaticamente
quando disponível, mas `MLP_DEVICE=cpu` força o fallback para testes.

## Execução

Abra [mlp_classificacao.ipynb](mlp_classificacao.ipynb) no VS Code ou Jupyter
e execute as células na ordem apresentada. O notebook é a única fonte de
código do projeto.

Use a célula `run_experiment()` para o treino completo, ou execute a chamada
curta abaixo na própria célula para uma validação rápida:

```python
run_experiment(device_override='cuda', max_rows=3000, epochs=3)
```

As funções `verify_reproducibility()` e `verify_cuda()` fazem, respectivamente,
a verificação CPU determinística e o teste real de CUDA. Os artefatos —
checkpoint, pré-processador, métricas, relatório e gráficos — são salvos em
`artifacts/`.
