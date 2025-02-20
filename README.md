# Projeto de Previsão de Aluguéis de Bicicletas

## Passo a Passo

1. **Preparação do Ambiente:**
   - Acessei o [Azure Machine Learning Studio](https://ml.azure.com/) e configurei um workspace chamado `joaofreitaspro`.

2. **Carregamento do Conjunto de Dados:**
   - Utilizei o conjunto de dados `bike-rentals`, disponível no Azure Open Datasets.

3. **Configuração do Experimento de AutoML:**
   - Configurei um experimento de regressão com as seguintes configurações:
     - Coluna alvo: `cnt` (número de aluguéis de bicicletas).
     - Métrica primária: Normalized Root Mean Squared Error (NRMSE).
     - Tempo máximo de execução: 10 minutos.

4. **Registro do Melhor Modelo:**
   - Após a conclusão do experimento, registrei o melhor modelo (`VotingEnsemble`) no workspace.

5. **Criação do Endpoint Online:**
   - Implantei o modelo como um endpoint online do tipo Serverless.
   - Nome do endpoint: `bike-rental-prediction-endpoint`.


## Resultados

- O melhor modelo selecionado foi um `VotingEnsemble` com NRMSE de **0.0889**.
- O endpoint está funcionando corretamente e retornando previsões em tempo real.

---

## Como Usar o Endpoint

Para fazer previsões usando o endpoint, siga estes passos:

1. Copie o REST endpoint fornecido pelo Azure ML.
Exemplo de solicitação:

   ```bash
   curl -X POST https://bike-rental-prediction-endpoint.eastus.inference.ml.azure.com/score \
        -H "Content-Type: application/json" \
        -H "Authorization: Bearer <your-api-key>" \
        -d '{
              "data": [
                {
                  "season": 1,
                  "yr": 0,
                  "mnth": 1,
                  "hr": 0,
                  "holiday": 0,
                  "weekday": 6,
                  "workingday": 0,
                  "weathersit": 1,
                  "temp": 0.24,
                  "atemp": 0.2879,
                  "hum": 0.81,
                  "windspeed": 0.0
                }
              ]
            }'
