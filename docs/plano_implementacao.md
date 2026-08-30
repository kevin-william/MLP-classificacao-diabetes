# Plano de implementação — MLP para classificação de diabetes

## 1. Objetivo

Construir um projeto reprodutível em PyTorch para classificar a variável
`diabetes` do arquivo `dataset/diabetes_prediction_dataset.csv`. O modelo será
uma MLP configurável, treinada preferencialmente em CUDA, com execução
automática em CPU quando uma GPU compatível não estiver disponível.

## 2. Entregáveis

- Ambiente virtual `.venv` na raiz do projeto.
- Arquivo de dependências para reprodução do ambiente.
- Script principal de treinamento com configuração centralizada.
- Classe `MLP` flexível para definir qualquer quantidade e tamanho de camadas
  ocultas.
- Pré-processamento persistido junto com o modelo treinado.
- Métricas, histórico de treino e gráficos de aprendizado.
- Checkpoint do melhor modelo validado e uma avaliação final no conjunto de
  teste.

## 3. Estrutura proposta

```text
mlp-classificacao/
├── .venv/                         # ambiente local, não versionado
├── dataset/
│   └── diabetes_prediction_dataset.csv
├── artifacts/                     # modelos, métricas e gráficos gerados
├── src/
│   ├── config.py                  # constantes e hiperparâmetros
│   ├── data.py                    # leitura, divisão e pré-processamento
│   ├── model.py                   # classe MLP
│   ├── train.py                   # laço de treino e validação
│   └── evaluate.py                # avaliação e relatório final
├── main.py                        # ponto de entrada do treinamento
├── requirements.txt
├── .gitignore
├── ideia.md
└── plano_implementacao.md
```

Os diretórios `artifacts/` e `.venv/` devem ser ignorados pelo Git; o código,
as configurações e as dependências devem ser versionados.

## 4. Ambiente e dependências

1. Criar o ambiente virtual na raiz: `python -m venv .venv`.
2. Instalar PyTorch com a versão CUDA correspondente ao ambiente em uso. O
   ambiente conhecido utiliza `torch==2.13.0+cu130`; a forma de instalação deve
   ficar documentada para essa combinação.
3. Registrar as demais dependências, no mínimo: `pandas`, `numpy`,
   `scikit-learn`, `matplotlib` e `seaborn`.
4. Implementar a seleção de dispositivo com:

   ```python
   device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
   ```

5. Exibir no início da execução o dispositivo e, quando aplicável, o nome da
   GPU. Nenhuma parte do fluxo pode depender exclusivamente de CUDA: tensores,
   modelo e treinamento devem funcionar também em CPU.

## 5. Dados e pré-processamento

O dataset contém as colunas `gender`, `age`, `hypertension`, `heart_disease`,
`smoking_history`, `bmi`, `HbA1c_level`, `blood_glucose_level` e o alvo
binário `diabetes`.

1. Carregar o CSV e validar a presença das colunas esperadas.
2. Separar `diabetes` como alvo e manter as demais colunas como atributos.
3. Fazer divisão estratificada em treino, validação e teste (por exemplo,
   70%/15%/15%), usando uma semente fixa para permitir reprodução.
4. Aplicar `OneHotEncoder(handle_unknown="ignore")` em `gender` e
   `smoking_history`.
5. Aplicar `StandardScaler` aos atributos numéricos. Os transformadores devem
   ser ajustados **somente** no conjunto de treino e reutilizados em validação,
   teste e inferência, evitando vazamento de dados.
6. Converter atributos para `torch.float32` e rótulos para `torch.long`.
7. Criar `TensorDataset` e `DataLoader`; embaralhar somente o loader de treino.
   Quando CUDA estiver disponível, habilitar `pin_memory=True` e transferências
   não bloqueantes quando apropriado.

## 6. Configuração centralizada

Definir em `src/config.py` um bloco de constantes, sem valores espalhados no
código. Ele deve conter ao menos:

- `SEED`, caminhos de dados e de artefatos;
- proporções de treino/validação/teste;
- `BATCH_SIZE`, `EPOCHS`, `LEARNING_RATE` e `WEIGHT_DECAY`;
- `HIDDEN_DIMS` (por exemplo, `[128, 64, 32]`) e `DROPOUT`;
- número de classes (`NUM_CLASSES = 2`);
- critério de melhoria, paciência de early stopping e caminho do checkpoint.

## 7. Modelo

Implementar `MLP(nn.Module)` recebendo `in_dim`, `hidden_dims`,
`num_classes` e `dropout`. Para cada dimensão oculta, a rede deverá acrescentar
na ordem:

```text
Linear → BatchNorm1d → ReLU → Dropout
```

A última camada deve ser `Linear(prev_dim, num_classes)`, sem ativação. Para a
saída binária com duas classes, usar `nn.CrossEntropyLoss`; portanto, o modelo
retorna logits com duas posições e a classe prevista é obtida por
`logits.argmax(dim=1)`. Isso substitui a comparação `pred > 0.5` do exemplo,
que só seria válida para uma única saída com `BCEWithLogitsLoss`.

## 8. Treinamento e validação

1. Inicializar o modelo no `device`, `AdamW` como otimizador e
   `CrossEntropyLoss` como critério inicial.
2. Em cada época, executar o modo `train`, calcular a perda média ponderada
   pelo tamanho dos lotes, fazer `zero_grad`, `backward` e `optimizer.step`.
3. Executar a validação com `model.eval()` e `torch.no_grad()`.
4. Registrar por época: perda de treino, perda de validação, acurácia de
   validação e, preferencialmente, F1 para a classe positiva.
5. Salvar o checkpoint quando a perda de validação melhorar. Aplicar early
   stopping ao exceder a paciência configurada.
6. Imprimir progresso periódico com época, perdas, métricas e dispositivo.
7. Restaurar o melhor checkpoint antes da avaliação final.

## 9. Avaliação e artefatos

No conjunto de teste, que não deve participar de decisões de treinamento,
gerar e salvar:

- loss e acurácia;
- precision, recall e F1 da classe positiva;
- matriz de confusão e relatório de classificação;
- curva de perda de treino/validação e curva de acurácia de validação;
- checkpoint contendo `state_dict`, configuração, dimensões de entrada e o
  pré-processador ajustado.

Como diabetes costuma ser uma classe minoritária nesse dataset, a análise deve
priorizar recall e F1 além de acurácia. Se essas métricas forem insuficientes,
testar pesos de classe em `CrossEntropyLoss`, calculados apenas a partir do
treino.

## 10. Verificação de conclusão

O projeto estará concluído quando:

1. `main.py` executar do início ao fim tanto com CUDA quanto em CPU;
2. o dispositivo selecionado aparecer claramente no log;
3. não houver vazamento entre treino, validação e teste;
4. o checkpoint e o pré-processador permitirem repetir uma inferência;
5. os artefatos de métricas e gráficos forem gerados em `artifacts/`; e
6. uma execução com a mesma semente produzir divisões e resultados compatíveis.
