# tutorial

## onnx

- <https://github.com/triton-inference-server/tutorials/blob/main/Quick_Deploy/ONNX/README.md>

```sh
REPO=$(PWD)/onnx_model_repository
WORKSPACE=$(PWD)/onnx_workspace
SERVER_IMAGE=nvcr.io/nvidia/tritonserver:24.05-py3
docker run --rm -p 8000:8000 -p 8001:8001 -p 8002:8002 -v ${REPO}:/models ${SERVER_IMAGE} tritonserver --model-repository=/models
```

```sh
SDK_IMAGE=onnx_tritonserver_sdk
docker build -t $SDK_IMAGE -f onnx_dockerfile .
docker run -it --rm --net=host -v ${WORKSPACE}:/workspace/ ${SDK_IMAGE} bash

python /workspace/client_onnx.py
```
