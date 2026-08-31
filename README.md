# MLP para classificação de diabetes

Projeto didático em PyTorch para treinar uma MLP sobre o dataset de diabetes.
Toda a implementação está em `mlp_classificacao.ipynb`.

O notebook prioriza código explícito: funções pequenas, variáveis
intermediárias, estruturas com atributos nomeados e uma responsabilidade por
função.

## Instalação

No PowerShell, crie e ative o ambiente virtual:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
pip install -r requirements-cuda.txt
```

Em uma máquina sem GPU, use `requirements-cpu.txt` no último comando. O
notebook seleciona CUDA automaticamente quando ela está disponível e usa CPU
como fallback.

## Organização do notebook

As células devem ser executadas em ordem. Elas estão divididas em:

1. configuração;
2. ambiente e reprodutibilidade;
3. leitura e divisão dos dados;
4. pré-processamento;
5. modelo;
6. treinamento;
7. avaliação;
8. artefatos;
9. inferência;
10. orquestração;
11. verificações automáticas;
12. estratégia de seleção por F2;
13. configuração da execução;
14. execução do experimento;
15. validações opcionais.

Cada seção apresenta primeiro sua finalidade e depois as classes e funções
correspondentes. Não é necessário importar código do projeto a partir de
outro arquivo.

## Execução

Abra `mlp_classificacao.ipynb` no VS Code ou Jupyter e execute as células na
ordem apresentada.

A configuração da execução final usa o dataset completo e até 200 épocas:

```python
config.maximum_rows = None
config.epochs = 200
config.minimum_epochs = 30
config.use_class_weights = True
config.artifacts_directory = PROJECT_ROOT / "artifacts" / "f2_full_dataset"
```

O early stopping só pode encerrar depois da época 30. Pesos de classe são
calculados a partir dos rótulos de treino como `pos_weight`. A MLP tem a
arquitetura `Entrada → 32 → 16 → 1`: sua saída única é um logit, convertido em
probabilidade positiva por `sigmoid` apenas na validação, teste e inferência.
A validação escolhe o limiar da classe positiva pelo maior F2; o teste e a
inferência usam o limiar salvo no checkpoint.

O dispositivo pode ser fixado antes da execução:

```python
config.requested_device = "cpu"
```

ou:

```python
config.requested_device = "cuda"
```

Quando `requested_device` é `None`, CUDA é usada quando estiver disponível.

## Artefatos

Cada execução gera:

- `best_model.pt`;
- `preprocessor.joblib`;
- `test_metrics.json`;
- `threshold_selection.json`;
- `classification_report.txt`;
- `confusion_matrix.png`;
- `learning_curves.png`;
- `history.json`;
- `imbalance_report.txt`;
- `metadata.json`.

O modelo e o pré-processador podem ser recarregados para inferência sem novo
treinamento.

## Validações

O final do notebook oferece duas chamadas opcionais:

```python
verify_reproducibility(PROJECT_ROOT, maximum_rows=3000, epochs=30)
verify_cuda(PROJECT_ROOT, maximum_rows=3000, epochs=30)
```

A primeira compara duas execuções determinísticas em CPU. A segunda executa
o fluxo em CUDA e informa claramente quando não existe GPU compatível.

O desenho das funções e os critérios de conclusão estão descritos em
`docs/plano_refatoracao.md`.
