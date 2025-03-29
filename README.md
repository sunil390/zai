# zai

## LocalAI Examples

#Cleanup:

1. docker system prune --all
2. dockere ps
3. 

### 2025 AIO Model
1. docker run -p 8080:8080 --gpus all --name local-ai -ti localai/localai:latest-aio-gpu-nvidia-cuda-11
   
### 2024 method

1. https://github.com/mudler/LocalAI-examples.git
2. cd LocalAI-examples/langchain-chroma
3. wget https://huggingface.co/skeskinen/ggml/resolve/main/all-MiniLM-L6-v2/ggml-model-q4_0.bin -O models/bert
4. wget https://gpt4all.io/models/ggml-gpt4all-j.bin -O models/ggml-gpt4all-j
5. mv .env.example .env
6. docker-compose up -d --build
7. docker logs -f langchain-chroma-api-1
8. http://127.0.0.1:8080
```
Go to Settings > Model Providers > LocalAI in Dify.
For the ggml-gpt4all-j model:
Model Type: Text Generation
Model Name: gpt-3.5-turbo
Server URL: http://127.0.0.1:8080 (or the host domain if Dify is deployed via Docker)
For the all-MiniLM-L6-v2 model:
Model Type: Embeddings
Model Name: text-embedding-ada-002
Server URL: http://127.0.0.1:8080 (or the host domain if Dify is deployed via Docker)
Click "Save" to use the models in the application.
Configure the Rerank Model:

Go to the "Model Provider" section in Dify.
Ensure the bge-reranker model is properly set up and accessible.
Set the Rerank Model in the Dataset:

Navigate to "Dataset -> Create Dataset -> Retrieval Settings".
Add the Rerank settings by specifying the bge-reranker model.
You can also change the Rerank configuration in the settings of an already created dataset.
Enable Multi-Path Recall Mode:

Go to "Prompt Orchestration -> Context -> Settings".
Set the recall mode to Multi-Path Recall and enable the Rerank model.
Here is a summary of the steps in code format:

# Step 1: Configure the Rerank Model
model_provider:
  - name: "Local Rerank Model"
    type: "bge-reranker"
    endpoint: "http://localhost:your_reranker_port"

# Step 2: Set the Rerank Model in the Dataset
dataset:
  - name: "Your Dataset"
    retrieval_settings:
      rerank_model: "bge-reranker"
      top_k: 10
      score_threshold: 0.5

# Step 3: Enable Multi-Path Recall Mode
prompt_orchestration:
  context:
    settings:
      recall_mode: "Multi-Path Recall"
      rerank_model: "bge-reranker"
Ensure that your m3e model is also properly integrated and accessible within your application context settings.
```
## Dify

1. git clone https://github.com/langgenius/dify.git --branch 0.15.3
2. cd dify/docker
3. cp .env.example .env
4. docker compose up -d
5. docker compose ps

## Dify Upgrade
1. cd dify/docker
2. docker compose down
3. git pull origin main
4. docker compose pull
5. docker compose up -d

## SSL

1. DIFY_HOST="www.dify.znext.ai"
2. openssl req -x509 -nodes -days 3650 -newkey rsa:4096 -out dify.crt -keyout dify.key -subj "/CN=${DIFY_HOST}/O=${DIFY_HOST}" -addext "subjectAltName = DNS:${DIFY_HOST}"
