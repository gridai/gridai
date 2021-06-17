<div align="center">

<img src="https://github.com/gridai/gridai/blob/main/grid_logo.png" width="200px">
<br>

**Focus on machine learning, NOT infrastructure.    
From the creators of PyTorch Lightning.**

---

<p align="center">
  <a href="https://grid.ai">Website</a> •
  <a href="#runs">Runs</a> •
  <a href="#interactive-sessions">Interactive Sessions</a> •
  <a href="https://docs.grid.ai">Docs</a> •
  <a href="#run-examples">Run Examples</a> •
  <a href="https://join.slack.com/t/gridai-community/shared_invite/zt-ozqiwuif-UYK6rZGVmTTpMfPcVSdicg">Join our Slack</a> •
  <a href="https://github.com/williamFalcon/pytorch-lightning">PyTorch Lightning</a>
</p>

[![PyPI - Python Version](https://img.shields.io/pypi/pyversions/lightning-grid)](https://pypi.org/project/lightning-grid/)
[![PyPI Status](https://badge.fury.io/py/lightning-grid.svg)](https://badge.fury.io/py/lightning-grid)
[![Docs](https://img.shields.io/badge/docs-passing-green)](https://docs.grid.ai)
[![Slack](https://img.shields.io/badge/slack-chat-green.svg?logo=slack)](https://join.slack.com/t/gridai-community/shared_invite/zt-ozqiwuif-UYK6rZGVmTTpMfPcVSdicg)

![](https://img.shields.io/badge/pytorch-lightning-blue.svg?logo=PyTorch%20Lightning)
![](https://img.shields.io/badge/grid-ai-blue.svg?logo=Grid.ai&logoColor=white)
</div>

---

## Grid.AI
Grid.AI lets you seamlessly train hundreds of machine learning models on the cloud from your laptop.

***Note: This repository will host the opensource components of Grid once they are ready. In the meantime
please use this to request features and to get help.***

---

## Grid Philosophy
Grid follows the same philosophy that we use for [PyTorch Lightning](https://github.com/PyTorchLightning/pytorch-lightning):

- Let the user focus on machine learning not engineering.  
- Remove all the infrastructure engineering so the user can focus.
- Focused on reproducibility

## Key features
- [Runs](https://docs.grid.ai/products/run-run-and-sweep-github-files): Run (and sweep) any private or public Github repository.
- [Sessions](https://docs.grid.ai/products/sessions): Interactive machines (with multiple GPUs) optimized for development.
- [Datastores](https://docs.grid.ai/products/add-data-to-grid-datastores): Low-latency, high-performance, auto-versioned datasets.
- Realtime costs + much more

## Create a free account
Visit [Grid.AI](https://www.grid.ai/pricing/)

## Runs
Run (and sweep) any private or public Github repository on the cloud.  

```bash
# install
pip install lightning-grid

# login
grid login

# clone the repo
git clone https://github.com/williamFalcon/cifar5.git
cd cifar5

# start run!
grid run --instance_type 8_v100_32gb project/lit_image_classifier.py --gpus 1 --learning_rate "uniform(1e-5, 1e-1, 8)"
```

The command above generates 8 experiments
```bash
(flash) ➜  project git:(master) grid status gifted-seahorse-83
✔ Fetching experiment status ... done!
┏━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━┳━━━━━━━━━━━━━┳━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━┓
┃ Experiment              ┃                          Command ┃ Status ┃    Duration ┃ gpus ┃        learning_rate ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━╇━━━━━━━━━━━━━╇━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━┩
│ gifted-seahorse-83-exp7 │ /project/lit_image_classifier.py │ queued │ 0d-00:00:21 │    1 │  0.07858944673974376 │
│ gifted-seahorse-83-exp6 │ /project/lit_image_classifier.py │ queued │ 0d-00:00:21 │    1 │   0.0492955135740864 │
│ gifted-seahorse-83-exp5 │ /project/lit_image_classifier.py │ queued │ 0d-00:00:21 │    1 │ 0.005299488022082154 │
│ gifted-seahorse-83-exp4 │ /project/lit_image_classifier.py │ queued │ 0d-00:00:21 │    1 │  0.09214628765569398 │
│ gifted-seahorse-83-exp3 │ /project/lit_image_classifier.py │ queued │ 0d-00:00:21 │    1 │  0.04288827588691595 │
│ gifted-seahorse-83-exp2 │ /project/lit_image_classifier.py │ queued │ 0d-00:00:21 │    1 │  0.02618640734272168 │
│ gifted-seahorse-83-exp1 │ /project/lit_image_classifier.py │ queued │ 0d-00:00:21 │    1 │  0.03269913908273296 │
│ gifted-seahorse-83-exp0 │ /project/lit_image_classifier.py │ queued │ 0d-00:00:21 │    1 │  0.06192848686653007 │
└─────────────────────────┴──────────────────────────────────┴────────┴─────────────┴──────┴──────────────────────┘
```

## Interactive Sessions
Sessions allow you to develop models interactively with direct ssh, VSCode and Jupyter Notebook access already built-in.

![Grid Session](https://grid-docs.s3.us-east-2.amazonaws.com/sess_abc_compressed.gif)

Or via the CLI
```bash
grid session create --instance_type 8_v100_32gb
```
---

## Run Examples

### Vision
[3D Image classification](https://docs.grid.ai/examples/vision/mosmeddata-3d-image-classification)     
[Image classificatin (ImageNet)](https://docs.grid.ai/examples/vision/image-classification-with-imagenet)    
[Object detection (Coco)](https://docs.grid.ai/examples/vision/coco)

### NLP
[GPT 10+ B Params](https://docs.grid.ai/examples/nlp/gpt-10b+-params-8-gpus)    
[Text classification](https://docs.grid.ai/examples/nlp/text-classification)

### Self-supervised learning
[SIMCLR](https://docs.grid.ai/examples/self-supervised-learning-1)

---

## Community

The Grid community is the place to chat about Deep Learning, machine learning and anything about scaling up production or research projects!
[Join our slack](https://join.slack.com/t/gridai-community/shared_invite/zt-ozqiwuif-UYK6rZGVmTTpMfPcVSdicg)

### Asking for help
If you have any questions here are some things you can do:

1. [Read the docs](https://docs.grid.ai).
2. [Start a discussion](https://github.com/gridai/gridai/discussions).
3. [Create a Github issue](https://github.com/gridai/gridai/issues/new).

### Enterprise support
For enterprise tier and support, [register your interest here](https://gridai.wpengine.com/upgrade/)
