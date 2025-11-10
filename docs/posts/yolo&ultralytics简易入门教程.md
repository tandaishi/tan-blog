---
date: 2025-11-10
category:
  - ai
tag:
  - ai
archive: false
---


# yolo&ultralytics简易入门教程




## 01.开场白，安装MiniConda

## 02.环境管理命令

## 03.安装依赖包

[https://pytorch.org/get-started/previous-versions/](https://pytorch.org/get-started/previous-versions/)

[https://docs.ultralytics.com/usage/cli/](https://docs.ultralytics.com/usage/cli/)

```Shell
$ pip install torch torchvision torchaudio jupyterlab
```

## 04.安装ultralytics

[https://github.com/ultralytics/ultralytics/releases](https://github.com/ultralytics/ultralytics/releases)

## 05.基础术语简介，简单了解一下ai
### ai大概的流程（mode）
训练，验证，预测/推理，导出部署
[Train](https://docs.ultralytics.com/modes/train/)，Validation，[Predict](https://docs.ultralytics.com/modes/predict/)，[Export](https://docs.ultralytics.com/modes/export/)
### yolo的功能（Task）
[Detection](https://docs.ultralytics.com/tasks/detect/)
[Instance Segmentation](https://docs.ultralytics.com/tasks/segment/)
[Pose/Keypoints](https://docs.ultralytics.com/tasks/pose/)
[Oriented Detection](https://docs.ultralytics.com/tasks/obb/)
[Classification](https://docs.ultralytics.com/tasks/classify/)

## 06初体验

```Python
from ultralytics import YOLO
yolo = YOLO('yolov8n.pt',task='detect')
result = yolo(source='detect_footage.png',save=True)
# .\ultralytics\cfg\default.yaml这个文件里面包含了所有的参数
# source=video.mp4
# source='screen'检测屏幕
# source=0检测摄像头
# save=True就会将检测结果存出来，存到run里
# conf=0.05置信区间
```

## 07参数

## 08jupyterlab

## 09结果

```Shell
display(result[0].names)
display(result[0].boxes.cls)
display(result[0].boxes.xywh)
```

## 10数据准备

[https://rename.jgrass.xyz/](https://rename.jgrass.xyz/)

## 11数据标注

[https://github.com/HumanSignal/labelImg/releases/tag/v1.8.1](https://github.com/HumanSignal/labelImg/releases/tag/v1.8.1)

```Shell
ultralytics-8.1.0
|__datasets
      |__icon
          |__images # 存放图片
          |  |__train # 训练集 注意要和labels里的对应
          |  |__val # 验证集 注意要和labels里的对应
          |
          |__labels # 存放标注信息
             |__train # 注意要和images里的对应
             |__val # 注意要和images里的对应
```

## 12训练

```YAML
# Train/val/test sets as 1) dir: path/to/imgs, 2) file: path/to/imgs.txt, or 3) list: [path/to/imgs1, path/to/imgs2, ..]
path: icon  # dataset root dir
train: images/train  # train images (relative to 'path') 118287 images
val: images/val  # val images (relative to 'path') 5000 images
test:   # 20288 of 40670 images, submit to https://competitions.codalab.org/competitions/20794

# Classes
names:
  0: geek
  1: trash
```

```Python
from ultralytics import YOLO
# Load model
model = YOLO('yolov8n.pt')
# Train model
model.train(data='icon.yaml',workers=0, epochs=300, batch=16)
```

## 13验证与预测试用自己的模型

训练的结果好不好用，主要看loss曲线是否收敛，一般来说，预测后发现还是不好用的话，那就提高数据集质量，再就是增加训练轮次。

## 14简易应用_拿到坐标

## 15简易应用_小程序

## 16用venv安装ultralytics,体验一下跟踪

## 17opencv读图片

## 18opencv读视频

## 19opencv播放视频

## 20抽帧 & 训练

## 21打地鼠功能实现



