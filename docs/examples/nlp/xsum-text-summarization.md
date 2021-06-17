---
description: >-
  This tutorial shows how to train Text Summarization Models on Grid using
  Lightning Flash on the XSum Dataset.
---

# XSum Text Summarization

## Goal

This example covers an abstractive Text Summarization deep learning task

1. What is Text Summarization  
2. Training the model using `train.py` script
3. Loading Grid Weights in Flash and Running Summarization Model

{% hint style="info" %}
This tutorial uses **PyTorch Lightning**
{% endhint %}

## Tutorial time

**5 minutes**

## Task: Text Summarization

_Text Summarization_ is the task of generating a consise overview of a text's main point into a short sentence/description. For example, taking a web article and describing the topic in a short sentence.

## Dataset: XSum

The [Extreme Summarization \(**XSum**\)](https://paperswithcode.com/paper/dont-give-me-the-details-just-the-summary) dataset is a dataset for evaluation of abstractive single-document summarization systems consisting of 226,711 news articles collected from BBC \(2010 to 2017\) accompanied with a one-sentence summary. The articles cover a wide variety of subjects \(e.g., News, Politics, Sports, Weather, Business, Technology, Science, Health, Family, Education, Entertainment and Arts\)

![Source: https://arxiv.org/pdf/1808.08745.pdf](../../.gitbook/assets/image%20%2818%29%20%281%29%20%281%29%20%282%29%20%282%29%20%282%29%20%282%29.png)

## Step 1: Model

[PyTorch Lightning Flash](https://lightning-flash.readthedocs.io/en/latest/reference/object_detection.html) enables the quick training, fine tuning, and inferencing of SOTA object detection algorithms such as RetinaNet.

For this demo, we're going to be using the [code here](https://github.com/aribornstein/T5-Summarization-Demo)

Here's a preview of this code.

```python
# 1. Download the data
download_data("https://pl-flash-data.s3.amazonaws.com/xsum.zip", "data/")


# 2. Load the data
datamodule = SummarizationData.from_csv(
    "input",
    "target",
    train_file=train_file,
    test_file=test_file,
)

# 3. Build the model
model = SummarizationTask(backbone='google/mt5-small')

# 4. Create the trainer. Run once on data
trainer = Trainer()

# 5. Fine-tune the model
trainer.finetune(model, datamodule=datamodule)

# 6. Save it!
trainer.save_checkpoint("summarization_model_xsum.pt")
```

## Step 2: Start a RUN

You can reproduce with this button

[![Grid](https://camo.githubusercontent.com/1b39d1721301ebc3d08db0971e6d4dd96db28d8028daff32eb3918e22cd1fbe0/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f7269645f41492d72756e2d3738464639362e7376673f6c6162656c436f6c6f723d626c61636b266c6f676f3d646174613a696d6167652f737667253262786d6c3b6261736536342c50484e325a79423361575230614430694e4467694947686c6157646f644430694e44676949475a7062477739496d3576626d5569494868746247357a50534a6f644852774f693876643364334c6e637a4c6d39795a7938794d4441774c334e325a79492b50484268644767675a443069545445674d5452324d6a42684d5451674d5451674d4341774d4445304944453061446c574d7a59754f4567784d693432566a4578614449794c6a56324e3267784d533479566a45305154453049444530494441674d44417a4d693430494442494d5456424d5451674d5451674d4341774d4445674d5452364969426d615778735053496a5a6d5a6d4969382b50484268644767675a44306954544d314c6a49674e44686f4d5445754d6c59794e5334315344497a4c6a6c324d5445754d3267784d53347a566a5134656949675a6d6c736244306949325a6d5a694976506a777663335a6e50673d3d)](https://platform.grid.ai/#/runs?script=https://github.com/aribornstein/T5-Summarization-Demo/blob/05d348b4/train.py&cloud=grid&use_spot&instance=g4dn.xlarge&accelerators=1&disk_size=200&framework=lightning&script_args=--grid_name%20silent-iguana-136%20%5C%0A--grid_strategy%20grid_search%20%5C%0A--grid_disk_size%20200%20%5C%0A--grid_max_nodes%2010%20%5C%0A--grid_instance_type%20g4dn.xlarge%20%5C%0A--use_spot%20true%20%5C%0A--grid_framework%20lightning%20%5C%0A--grid_credential%20cc-vnpnm%20%5C%0A--grid_gpus%201%20%5C%0Atrain.py%20--gpus%201%20--max_epochs%203)

Or manually train this model on Grid has 4 simple steps:

* Create a **Run**.
* Copy and paste the model script.

```text
https://github.com/aribornstein/T5-Summarization-Demo/blob/main/train.py
```

* Select  1xT4 \(16 GB\) $0.68/h \(g4dn.xlarge\) as the Accelerator
* Provide the  run arguments `--max_epochs 5` `--gpus 1` 

You can add optional flags to this script:

```text
--backbone summarization_model_to_train
--train_file /path/to/train.csv
--valid_file /path/to/val.csv
--test_file /path/to/test.csv
--download False
```

## Step 3: Use the model for predictions

In this step, we load the Grid weights in Flash and run the model to detect objects.

1. Download Artifacts from Grid Run 

![](../../.gitbook/assets/image%20%288%29.png)

1. Load model to our script and inference in 2 lines of code. 

```python
from flash.text import SummarizationTask


# 1. Load the model from a checkpoint
model = SummarizationTask.load_from_checkpoint("./summarization_model_xsum.pt")

# 2. Summarize an article!
print(model.predict([
    """
    Camilla bought a box of mangoes with a Brixton Â£10 note, introduced last year to try to keep the money of local
    people within the community.The couple were surrounded by shoppers as they walked along Electric Avenue.
    They came to Brixton to see work which has started to revitalise the borough.
    It was Charles' first visit to the area since 1996, when he was accompanied by the former
    South African president Nelson Mandela.Greengrocer Derek Chong, who has run a stall on Electric Avenue
    for 20 years, said Camilla had been ""nice and pleasant"" when she purchased the fruit.
    ""She asked me what was nice, what would I recommend, and I said we've got some nice mangoes.
    She asked me were they ripe and I said yes - they're from the Dominican Republic.""
    Mr Chong is one of 170 local retailers who accept the Brixton Pound.
    Customers exchange traditional pound coins for Brixton Pounds and then spend them at the market
    or in participating shops.
    """
]))
```

Congratulations you have successfully trained and run inference for your first Text Summarization Model with Grid.

## Bonus: CLI equivalent

Here are the equivalent commands for the CLI

First, clone the project

```python
git clone https://github.com/aribornstein/T5-Summarization-Demo.git
cd T5-Summarization-Demo
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

