---
description: >-
  This tutorial shows how to train Object Detection Models on Grid using
  Lightning Flash and the COCO format.
---

# Coco Object Detection

## Goal

This example covers an object detection deep learning task

1. What is Object Detection  
2. Training the model using `train.py` script
3. Loading Grid Weights in Flash and Running Object Detector

{% hint style="info" %}
This tutorial uses **PyTorch Lightning**
{% endhint %}

## Tutorial time

**5 minutes**

## Task: Object Detection

_Object detection_ is the task of _detecting_ instances of _objects_ of a certain class within an image.

## Dataset: COCO

The COCO \(Common Objects in Context\) _dataset_ \([reference](https://cocodataset.org/)\) is a large-scale object detection dataset with 91 instance classes.

![Example CoCo Images](../../.gitbook/assets/image%20%28124%29.png)

## Step 1: Model

[PyTorch Lightning Flash](https://lightning-flash.readthedocs.io/en/latest/reference/object_detection.html) enables the quick training, fine tuning, and inferencing of SOTA object detection algorithms such as RetinaNet.

For this demo, we're going to be using this [code here](https://github.com/aribornstein/CocoDemo/blob/main/train.py)

Here's a preview of this code.

```python
import flash
from flash.core.data import download_data
from flash.vision import ObjectDetectionData, ObjectDetector

# 1. Download the data
# Dataset Credit: https://www.kaggle.com/ultralytics/coco128
download_data("https://github.com/zhiqwang/yolov5-rt-stack/releases/download/v0.3.0/coco128.zip", 
              "data/")
# 2. Load the Data
datamodule = ObjectDetectionData.from_coco(
    train_folder=os.path.join(args.data_dir, "data/coco128/images/train2017/"),
    train_ann_file=os.path.join(args.data_dir, "data/coco128/annotations/instances_train2017.json"),
    batch_size=2
)
# 3. Build the model
model = ObjectDetector(num_classes=datamodule.num_classes)

# 4. Create the trainer
trainer = flash.Trainer(max_epochs=args.max_epochs, gpus=args.gpus)

# 5. Finetune the model
trainer.finetune(model, datamodule)

# 6. Save it!
trainer.save_checkpoint("object_detection_model.pt")
```

## Step 2: Start a RUN

Training this model on Grid has 4 simple steps:

* Create a **Run**.
* Copy and paste the model script.

```text
https://github.com/aribornstein/CocoDemo/blob/main/train.py
```

* Select  1xT4 \(16 GB\) $0.68/h \(g4dn.xlarge\) as the Accelerator
* Provide the  run arguments `--max_epochs 5` `--gpus 1` 

{% embed url="https://www.loom.com/share/18765b8b4d794c88b93ccbcce6493884" caption="" %}

You can add optional flags to this script:

```text
--train_folder /path/to/dataset
--train_ann_file /path/to/annotations.json
--download False
```

## Step 3: Use the model for predictions

In this step, we load the Grid weights in Flash and run the model to detect objects.

1. Download Artifacts from Grid Run 

![](../../.gitbook/assets/image%20%2883%29.png)

1. Load model to our script and inference in 4 lines of code. 

```python
from flash.vision import ObjectDetector

# 1. Load the model
detector = ObjectDetector.load_from_checkpoint("object_detection_model.pt")

# 2. Perform inference on an image file
predictions = detector.predict("path/to/image.png")
print(predictions)
```

Congratulations you have successfully trained and run inference for your first Object Detection Model with Grid.

## Bonus: CLI equivalent

Here are the equivalent commands for the CLI

First, clone the project

```python
git clone https://github.com/aribornstein/CocoDemo.git
cd CocoDemo
```

Start run

```python
grid run \
--instance_type 1_v100_16gb \
--framework lightning \
--gpus 1 \
train.py \
--max_epochs 5 \
--gpus 1
```

