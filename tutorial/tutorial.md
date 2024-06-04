# tutorial

## onnx

- <https://github.com/triton-inference-server/tutorials/blob/main/Quick_Deploy/ONNX/README.md>

### start tritonserver

```sh
cd onnx
REPO=$(PWD)/onnx_model_repository
WORKSPACE=$(PWD)/onnx_workspace
SERVER_IMAGE=nvcr.io/nvidia/tritonserver:24.05-py3
docker run --rm -p 8000:8000 -p 8001:8001 -p 8002:8002 -v ${REPO}:/models ${SERVER_IMAGE} tritonserver --model-repository=/models
```

```sh
cd onnx
SDK_IMAGE=onnx_tritonserver_sdk
docker build -t $SDK_IMAGE -f onnx_dockerfile .
```

```sh
SDK_IMAGE=onnx_tritonserver_sdk
docker run -it --rm -e TRITON_SERVER=$(ipconfig getifaddr en0) ${SDK_IMAGE} python client_onnx.py
```
