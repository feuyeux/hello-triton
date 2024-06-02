# Hello Triton

<!-- https://github.com/omarabid59/yolov8-triton.git -->

## model(pt to onnx)

```sh
virtualenv triton_env --python=python3.11
source triton_env/bin/activate
```

```ps1
python -m venv triton_env
# git bash
source triton_env/Scripts/activate
# cmd
.\triton_env\Scripts\activate.bat
# powershell
.\triton_env\Scripts\activate.ps1
```

```sh
python -m pip install --upgrade pip
# ultralytics yolo
pip install -U ultralytics==8.0.51
pip install -U tritonclient[all]
```

```sh
yolo export model=yolov8n.pt format=onnx dynamic=True opset=16
mkdir models/yolov8_onnx/1/
mv yolov8n.onnx models/yolov8_onnx/1/
```

## run server

Dockerfile

- The `xx.yy-py3` image contains the Triton inference server with support for Tensorflow, PyTorch, TensorRT, ONNX and OpenVINO models.
- The `xx.yy-py3-sdk` image contains Python and C++ client libraries, client examples, and the Model Analyzer.
- The `xx.yy-py3-min` image is used as the base for creating custom Triton server containers as described in Customize Triton Container.
- The `xx.yy-pyt-python-py3` image contains the Triton Inference Server with support for PyTorch and Python backends only.
- The `xx.yy-tf2-python-py3` image contains the Triton Inference Server with support for TensorFlow 2.x and Python backends only.

```sh
# https://org.ngc.nvidia.com/setup/api-key
docker login nvcr.io
Username: $oauthtoken
Password:
Login Succeeded

DOCKER_NAME="yolov8-triton"
docker build -t $DOCKER_NAME -f Dockerfile .

docker run --rm -p8000:8000 -p8001:8001 -p8002:8002 \
-v $(PWD)/models:/models \
yolov8-triton \
tritonserver --model-repository=/models
```

## run client

```sh
source triton_env/bin/activate
python main.py
open /tmp/yolov_output.jpg
```
