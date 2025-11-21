# Информация о карте
- NVIDIA-SMI 580.88
- Driver Version: 580.88
- CUDA Version: 13.0
- NVIDIA GeForce RTX 3070 8 Gb

# Сборка и запуск
docker build --no-cache -t vllm-user-bge .
docker run --gpus all -p 8000:8000 vllm-user-bge

docker build -t vllm-user-bge .

# После старта vLLM будет доступен по адресу:

http://localhost:8000/v1/

# Проверка: получение эмбеддингов

curl -X POST http://localhost:8000/v1/embeddings \
  -H "Content-Type: application/json" \
  --data-binary @request.json

# Сложности и полезности

1. С uv вообще не собралось, пошел в упрощение
2. Если версия cuda меньше той, которая на видеокарте, то проблем не будет. В этом ошибки нет.
3. Изначально ставил vllm[embedding]==0.5.4, не завелось. Вот так завелось: vllm[embedding]>=0.8.0
4. Кажется, что есть проблема с версией здесь: python3 -m pip install torch==2.3.1. Обратил внимание, что при сборке удаляет и ставит другую версию. Надо разбираться.
5. Этот параметр вроде бы бесполезен, но нет времени уже проверять: ENV VLLM_GPU_MEMORY_UTIL=0.6
6. Так как карта маленькая, то vllm хотел много памяти, вот этот параметр помог: "--gpu_memory_utilization", "0.7"
7. Говорят, что vllm не работает на CPU, но есть https://docs.vllm.ai/en/latest/getting_started/installation/cpu/#build-wheel-from-source и https://hub.docker.com/r/openeuler/vllm-cpu. Надо отдельно исследовать!