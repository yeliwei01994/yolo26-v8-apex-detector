# Apex Legends Player Detector

一个用于检测《Apex Legends》游戏画面中可见人物的个人 YOLO 目标检测项目。

## 数据集说明

- 类别数：1
- 类别 ID：`0`（`person`）
- 当前划分：train 822 张、val 103 张、test 103 张
- 数据集、原始视频、截图和标注文件均为个人使用素材，**不会上传到本仓库**。

数据集应在本地具有以下结构：

```text
apex_person_dataset/
├── images/
│   ├── train/
│   ├── val/
│   └── test/
├── labels/
│   ├── train/
│   ├── val/
│   └── test/
└── data.yaml
```

标签使用 YOLO 格式：

```text
class_id center_x center_y width height
```

所有坐标均归一化到 `0`–`1`。

## 环境安装

建议使用独立的 Python 虚拟环境：

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

## 配置数据集

复制模板并将 `path` 改为你的本地数据集绝对路径：

```powershell
Copy-Item data.example.yaml data.yaml
```

例如：

```yaml
path: E:/yolo data/apex_person_dataset
```

## 训练

以下命令以 Ultralytics YOLOv8n 作为首版基线模型：

```powershell
yolo detect train model=yolov8n.pt data=data.yaml epochs=100 imgsz=640 batch=8 project=runs name=apex-person-v1
```

如果显存允许，可将 `batch=8` 提高；若显存不足则降低为 `batch=4` 或 `batch=2`。

## 验证与测试

```powershell
yolo detect val model=runs/apex-person-v1/weights/best.pt data=data.yaml split=val
yolo detect val model=runs/apex-person-v1/weights/best.pt data=data.yaml split=test
```

## 使用边界

本项目仅用于个人学习、数据标注和模型实验。请遵守游戏、平台和相关内容的使用条款；不要将其用于破坏公平游戏体验的用途。
