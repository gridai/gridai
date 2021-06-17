---
description: >-
  This tutorial shows how to train Video Classification Models on Grid using
  Lightning Flash
---

# Kinetics Video Classification

## Goal

This example covers a video classification deep learning task

1. What is Video Classification  
2. Training the model using `train.py` script
3. Loading Grid Weights in Flash and Running Object Detector

## Tutorial time

**5 minutes**

## Task: Video Classification

_Video Classification_ is the task of _classifying_ _videos_ based on _classes_ of content. _Video_ _Classification_ enables computers to recognize actions, objects, and events in videos. From Retail, Health Care to Agriculture, Video Understanding enables automation of [countless industry use cases](https://www.cio.com/article/3431138/ai-gets-the-picture-streamlining-business-processes-with-image-and-video-classification.html). \_\_

## Dataset: Kinetics

The Kinetics Human Action Video Dataset released by DeepMind \([reference](https://deepmind.com/research/open-source/kinetics)\) is a large-scale video understanding dataset comprised of annotated~10s video clips sourced from YouTube.

![Example Kinetics Video Thumbnails](../../../.gitbook/assets/image%20%28137%29.png)

## Step 1: Model

[PyTorch Lightning Flash](https://lightning-flash.readthedocs.io/en/latest/reference/object_detection.html) enables quick training, fine tuning, and inferencing of SOTA video classification.

For this demo, we're going to be using the [code here](https://github.com/aribornstein/KineticsDemo)

## Step 2: Start a RUN

Training this model on Grid has 4 simple steps or you can click [here](https://platform.grid.ai/#/runs?script=https://github.com/aribornstein/KineticsDemo/blob/4fcf30e1c2fd46247ec0fc1a6cb0886e9838586f/train.py&cloud=grid&instance=g4dn.xlarge&accelerators=1&disk_size=200&framework=lightning&script_args=--grid_name%20transformers-run%20%5C%0A--grid_strategy%20grid_search%20%5C%0A--grid_disk_size%20200%20%5C%0A--grid_max_nodes%2010%20%5C%0A--grid_datastore_mount_dir%20%2Fopt%2Fdatastore%20%5C%0A--grid_instance_type%20p3.2xlarge%20%5C%0A--grid_credential%20cc-b87v8%20%5C%0A--grid_framework%20lightning%20%5C%0A--grid_gpus%201%20%5C%0Atrain.py%20--gpus%201%20--max_epochs%2010) to get started:

* Create a **Run**.
* Copy and paste the model script.

```text
https://github.com/aribornstein/KineticsDemo/blob/main/train.py
```

* Select  1xT4 \(16 GB\) $0.68/h \(g4dn.xlarge\) as the Accelerator
* Provide the  run arguments `--max_epochs 5` `--gpus 1` 

You can add optional flags to this script:

```text
--train_folder /path/to/train_videos
--val_folder /path/to/val_videos
--download False
```

## Step 3: Use the model for predictions

In this step, we load the Grid weights in Flash and run the model to classify videos.

1.Download Artifacts from Grid Run

![](../../../.gitbook/assets/image%20%2834%29.png)

1. Load model to our script and inference in 4 lines of code. 

```python
from flash.core.utilities.imports import _KORNIA_AVAILABLE, _PYTORCHVIDEO_AVAILABLE
from flash.video import VideoClassifier

# 1. Load the model
model = VideoClassifier.load_from_checkpoint("video_classification_model.pts")

# 2. Make a prediction
predictions = model.predict("path/to/video.png")
print(predictions)
```

Congratulations you have successfully trained and run inference for your first Video Classification Model with Grid.

## Bonus: CLI equivalent

Here are the equivalent commands for the CLI

First, clone the project

```python
git clone https://github.com/aribornstein/KineticsDemo.git
cd KineticsDemo
```

Start run

```python
grid run \
--name $1 \
--disk_size 200 \
--instance_type g4dn.xlarge \
--gpus 1 \
train.py \
--gpus 1
--fast_dev_run 1
```

