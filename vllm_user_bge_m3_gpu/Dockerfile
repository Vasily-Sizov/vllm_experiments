FROM nvidia/cuda:12.1.1-runtime-ubuntu22.04

RUN apt-get update && \
    apt-get install -y python3 python3-pip git && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app

RUN python3 -m pip install --upgrade pip

# PyTorch с CUDA 12.1
RUN python3 -m pip install torch==2.3.1 --index-url https://download.pytorch.org/whl/cu121

# Последняя версия vLLM (с возможностью отключить guided decoding)
RUN python3 -m pip install "vllm[embedding]>=0.8.0"

ENV VLLM_GPU_MEMORY_UTIL=0.6

# Отключаем guided decoding
CMD ["vllm", "serve", "deepvk/USER-bge-m3", "--task", "embedding", "--host", "0.0.0.0", "--port", "8000", "--gpu_memory_utilization", "0.7"]

