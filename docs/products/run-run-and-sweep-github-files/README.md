---
description: Run (and sweep) any private or public Github repository.
---

# ⚡Serverless Runs

## Runs

Run \(**and sweep**\) any private or public Github repository on the cloud.  

```bash
# clone repo
git clone https://github.com/williamFalcon/hello

# start the sweep
cd hello
grid run hello.py --number "[1, 2]" --food_item "['pizza', 'hotdog']"
```

**⚡️⚡️Forget about infrastructure ⚡️⚡️**

Runs are serverless which means you only pay for the time your scripts are actually running. When running on your own infrastructure this amounts to massive cost savings as well.

## 1 minute overview

In this video we're going to run an arbitrary model \(from the pytorch examples github repo\) across 4 GPUs \(4 experiments each on 2 GPUs\)

{% embed url="https://grid-docs.s3.us-east-2.amazonaws.com/intro\_video\_docs\_run.mp4" %}

## Product Tour

[Click here for a 2-minute tour of RUN](https://platform.grid.ai/#/dashboard?product_tour_id=226810)

![](../../../.gitbook/assets/image%20%2843%29.png)

## Option 1: Run via the CLI

RUN **any** GitHub file with Grid in 4 steps:

```bash
# 1. clone the repo
git clone https://github.com/pytorch/examples

# 2. find the file to run
cd examples/dcgan

# 3. verify it works locally (optional)
python   main.py --dataset cifar10 --lr 0.0002 --dataroot .

# 4. run on a cloud instance via grid
grid run main.py --dataset cifar10 --lr 0.0002 --dataroot .
```

Grid offers advanced syntax for starting a run. With this code:

```bash
grid run hello.py --number "[1, 2]" --food_item "['pizza', 'hotdog']"
```

Grid will run the script 4 times... these are the 4 equivalent script calls \(we call each script call an experiment\)

```bash
python hello.py --number 1 --food_item 'pizza'
python hello.py --number 2 --food_item 'pizza'

python hello.py --number 1 --food_item 'hotdog'
python hello.py --number 2 --food_item 'hotdog'
```

{% hint style="info" %}
A RUN is a collection of experiments \(the run has 4 experiments in this example\).
{% endhint %}

## **Option 2: Start via the web UI**

![](../../../.gitbook/assets/run_start.gif)



