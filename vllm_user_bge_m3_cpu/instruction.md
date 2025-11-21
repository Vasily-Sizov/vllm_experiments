docker pull openeuler/vllm-cpu:latest

docker run --rm -it \
    --security-opt seccomp=unconfined \
    --cap-add SYS_NICE \
    --cap-add SYS_RESOURCE \
    --cap-add SYS_ADMIN \
    -p 8000:8000 \
    openeuler/vllm-cpu \
    --model deepvk/USER-bge-m3 \
    --task embedding \
    --host 0.0.0.0 \
    --port 8000 \
    --device cpu