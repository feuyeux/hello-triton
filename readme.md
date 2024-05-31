# Hello Triton

<!-- https://github.com/omarabid59/yolov8-triton.git -->

## model(pt to onnx)

```sh
virtualenv triton_env --python=python3.11
source triton_env/bin/activate

pip install -U ultralytics==8.0.51 'tritonclient[all]'

yolo export model=yolov8n.pt format=onnx dynamic=True opset=16
mkdir models/yolov8_onnx/1/
mv yolov8n.onnx models/yolov8_onnx/1/
```

## run server

```sh
DOCKER_NAME="yolov8-triton"
docker build -t $DOCKER_NAME .

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