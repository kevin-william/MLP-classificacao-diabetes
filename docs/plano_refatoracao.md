# Plano de refatoração do notebook

## 1. Objetivo

Manter toda a implementação em `mlp_classificacao.ipynb` e organizar o
notebook para que seu comportamento seja compreendido pela leitura sequencial
das células.

Cada função deve executar uma tarefa única. As funções de alto nível devem
apenas coordenar funções menores cujos nomes revelem cada etapa do fluxo.

O notebook deve oferecer:

- configuração centralizada;
- execução determinística;
- seleção automática entre CPU e CUDA;
- validação do dataset;
- divisão estratificada;
- pré-processamento sem vazamento de dados;
- MLP configurável;
- treinamento, validação, checkpoint e early stopping;
- avaliação final;
- geração de artefatos;
- recarga para inferência;
- validação de reprodutibilidade e CUDA.

## 2. Regras de legibilidade

1. Uma função deve responder a uma pergunta ou executar uma ação.
2. Usar nomes completos para funções, parâmetros e variáveis.
3. Usar variáveis intermediárias para tornar cálculos visíveis.
4. Preferir blocos `if` e `for` explícitos.
5. Não usar compreensões em regras de negócio.
6. Não usar lambdas, funções aninhadas ou ternários embutidos.
7. Não colocar várias decisões na mesma linha.
8. Não retornar tuplas cujo significado dependa da posição.
9. Representar resultados importantes com classes e atributos nomeados.
10. Usar dicionários apenas nas fronteiras de serialização e bibliotecas.
11. Deixar leitura, escrita, impressão e uso de dispositivo visíveis nos nomes.
12. Aceitar repetição pequena quando ela melhora a leitura.
13. Comentar decisões e restrições, não o significado literal da linha.

Recursos necessários das bibliotecas, como `with torch.no_grad()` e a herança
de `nn.Module`, permanecem explícitos no código.

## 3. Organização das células

### 3.1 Configuração

Define `ExperimentConfig` e funções independentes para:

- criar os valores padrão;
- ler variáveis de ambiente opcionais;
- validar proporções;
- validar hiperparâmetros de treino;
- validar hiperparâmetros do modelo;
- calcular caminhos derivados;
- serializar a configuração.

### 3.2 Ambiente e reprodutibilidade

Separa as responsabilidades de:

- configurar a semente do Python;
- configurar a semente do NumPy;
- configurar a semente do PyTorch;
- ativar algoritmos determinísticos;
- validar o dispositivo solicitado;
- selecionar CPU ou CUDA;
- coletar e exibir metadados do ambiente.

### 3.3 Leitura e divisão dos dados

Cada regra do CSV possui uma função própria:

- existência do arquivo;
- leitura;
- colunas obrigatórias;
- dataset vazio;
- valores ausentes;
- alvo binário;
- presença das duas classes;
- seleção das colunas usadas pelo modelo.

A divisão é executada em duas etapas nomeadas: separação do teste e separação
entre treino e validação. Os resultados usam `DatasetSplits`.

### 3.4 Pré-processamento

O fluxo deixa visível que:

- o transformador categórico usa `OneHotEncoder`;
- o transformador numérico usa `StandardScaler`;
- somente os atributos de treino executam `fit_transform`;
- validação e teste executam apenas `transform`;
- todas as matrizes são convertidas para `float32`;
- todas as matrizes possuem a mesma largura;
- apenas o loader de treino embaralha;
- `pin_memory` é ativado em CUDA.

### 3.5 Modelo

A construção da MLP é separada em:

- validação das dimensões ocultas;
- criação de um bloco oculto;
- criação da lista completa de camadas;
- construção do modelo no dispositivo;
- validação da forma e dos valores da saída.

Cada bloco oculto segue a ordem:

```text
Linear → BatchNorm1d → ReLU → Dropout
```

### 3.6 Treinamento

O treinamento possui funções específicas para:

- mover um lote para o dispositivo;
- treinar um lote;
- treinar uma época;
- prever um lote;
- avaliar uma época;
- calcular pesos de classe;
- criar a função de perda;
- criar o otimizador;
- decidir se houve melhoria;
- decidir o early stopping;
- criar, salvar e restaurar checkpoint;
- registrar e imprimir uma época.

Validação e teste compartilham `evaluate_one_epoch`, evitando dois percursos
diferentes para o mesmo comportamento.

### 3.7 Avaliação

Cada métrica é calculada por uma função nomeada. `ClassificationMetrics`
mantém loss, accuracy, precision, recall, F1, relatório de classificação e
matriz de confusão como atributos.

### 3.8 Artefatos

Leitura, escrita, serialização e gráficos são efeitos explícitos. Cada
artefato possui uma função de salvamento própria, e
`save_experiment_artifacts` apenas coordena essas chamadas.

### 3.9 Inferência

`Predictor` mantém modelo, pré-processador e dispositivo já carregados. A
predição é dividida em:

- validação das colunas;
- seleção e ordenação das colunas;
- transformação dos atributos;
- execução do modelo;
- conversão para classes.

Checkpoints com prefixo `net.*` são normalizados explicitamente para o nome
atual `network.*` durante a carga.

### 3.10 Orquestração

`run_experiment` apresenta a sequência completa:

1. preparar ambiente;
2. preparar dados;
3. preparar modelo, loss e otimizador;
4. treinar;
5. avaliar no teste;
6. salvar artefatos;
7. recarregar para inferência;
8. montar e salvar o resultado.

Essa função não contém detalhes de pré-processamento, fórmulas de métricas ou
manipulação direta do checkpoint.

## 4. Estruturas de dados explícitas

O notebook utiliza classes simples para dar nome aos contratos internos:

- `ExperimentConfig`;
- `RuntimeMetadata`;
- `FeaturesAndTarget`;
- `RemainingAndTestData`;
- `DatasetSplits`;
- `TargetSummary`;
- `DatasetSplitSummary`;
- `DatasetDiagnostics`;
- `TransformedSplits`;
- `DataLoaders`;
- `DeviceBatch`;
- `BatchTrainingResult`;
- `BatchPrediction`;
- `EpochResult`;
- `TrainingHistory`;
- `ClassificationMetrics`;
- `Predictor`;
- `PreparedExperiment`;
- `PreparedTrainingData`;
- `TrainingComponents`;
- `ExperimentResult`.

## 5. Validações do notebook

Uma execução de validação deve confirmar:

1. todas as células executam em ordem em um kernel limpo;
2. o dataset é dividido sem índices compartilhados;
3. o pré-processador é ajustado somente no treino;
4. atributos transformados são `float32`;
5. rótulos são `int64`;
6. a MLP retorna uma coluna de logit para cada classe;
7. validação não calcula gradientes;
8. o melhor checkpoint é restaurado;
9. todos os artefatos são gerados;
10. a inferência recarregada produz previsões;
11. duas execuções CPU com a mesma semente são idênticas;
12. a execução CUDA funciona quando uma GPU está disponível.

## 6. Critérios de conclusão

O notebook está concluído quando:

1. contém toda a implementação necessária;
2. pode ser executado do início ao fim sem importar código do projeto;
3. cada seção possui uma responsabilidade clara;
4. não há compreensões, lambdas, funções aninhadas ou ternários nas regras de
   negócio;
5. os contratos internos principais usam atributos nomeados;
6. validação e teste compartilham o mesmo percurso;
7. o pré-processamento não apresenta vazamento de dados;
8. CPU e CUDA são selecionadas corretamente;
9. os artefatos permitem inferência sem novo treinamento;
10. a execução com a mesma semente é reproduzível.
