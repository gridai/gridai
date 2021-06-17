# GPT 10B+ params \(8 GPUs\)

## GPT

In this tutorial, we'll train the [Min-GPT by Andrej Karpathy](https://github.com/karpathy/minGPT) across 8 GPUs. This model uses PyTorch Lightning + Deepspeed to scale the model up.

This model was adapted by [Sean Naren](https://github.com/SeanNaren) to use PyTorch Lightning + Deepspeed.

Time: **2 minutes**

{% embed url="https://grid-docs.s3.us-east-2.amazonaws.com/min\_gpt.mp4" caption="" %}

## Run via the UI

The tutorial is extremely simple...

1. Find the path of the file we want to train \([https://github.com/SeanNaren/minGPT/blob/stage3/train.py](https://github.com/SeanNaren/minGPT/blob/stage3/train.py)\)
2. Paste it into the run dialog on the UI

![](../../../.gitbook/assets/image%20%2810%29.png)

1. Choose a machine with 8 GPUs \(and make sure you are using all 8 GPUs per experiment\)

![](../../../.gitbook/assets/image%20%2874%29.png)

1. Paste the script arguments 

```bash
--n_layer 15 \
--n_head 16 \
--n_embd 3072 \
--gpus 8 \
--precision 16 \
--batch_size 1
```

![](../../../.gitbook/assets/image%20%2868%29.png)

## Run via the CLI

Make sure you have the grid CLI installed and you've logged in.

```text
pip install lightning-grid
grid login
```

First, clone the repo

```text
git clone https://github.com/SeanNaren/minGPT.git
cd minGPT
```

For 1.7 B params, run this command:

```text
grid run \
--instance_type 8_K80_12gb \
--gpus 8 \
train.py \
--n_layer 15 \
--n_head 16 \
--n_embd 3072 \
--gpus 8 \
--precision 16 \
--batch_size 1
```

## 1.7B params

```bash
grid run \
--instance_type 8_K80_12gb \
--gpus 8 \
train.py \
--n_layer 15 \
--n_head 16 \
--n_embd 3072 \
--gpus 8 \
--precision 16 \
--batch_size 1
```

## **10B params**

```bash
grid run \
--instance_type 8_v100_32gb \
--gpus 8 \
train.py \
--n_layer 15 \
--n_head 16 \
--n_embd 3072 \
--gpus 8 \
--precision 16 \
--batch_size 1
```

## **20B params**

```bash
grid run \
--instance_type 8_v100_32gb \
--gpus 8 \
train.py \
--n_layer 25 \
--n_head 16 \
--n_embd 3072 \
--gpus 8 \
--precision 16 \
--batch_size 1
```

