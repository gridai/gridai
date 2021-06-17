---
description: >-
  This tutorial shows how to train 3D Image Classification Models on Grid using
  the Keras API in the TensorFlow 2.2.2 Library and the MosMedData CT Scan
  Dataset.
---

# MosMedData 3D Image Classification

## Goal <a id="goal"></a>

This example covers a 3D Image Classification task using Keras‌

1. What is 3D Image Classification from CT Scans
2. Training the Keras model using `train.py` script from the CLI
3. View Artifacts and Grid Weights in Keras and Inference Model

{% hint style="info" %}
This tutorial shows how to perform a Grid Run with the [**Tensorflow 2.2.2**](https://github.com/tensorflow/tensorflow/releases/tag/v2.2.2) **library from the Grid CLI.** 
{% endhint %}

## Tutorial time <a id="tutorial-time"></a>

**15 minutes**‌

## Task: 3D Image Classification <a id="task-3d-image-classification"></a>

‌_3D Image Classification_ is the task of classifying volumetric data such as 3D Models or Medical CT Scans from collections of 2D images.

The example shows the steps needed to build a 3D convolutional neural network \(CNN\) to predict the presence of viral pneumonia in computer tomography \(CT\) scans. 2D CNNs are commonly used to process RGB images \(3 channels\). A 3D CNN is simply the 3D equivalent: it takes as input a 3D volume or a sequence of 2D frames \(e.g. slices in a CT scan\), 3D CNNs are a powerful model for learning representations for volumetric data. It uses a subset of the [MosMedData: Chest CT Scans with COVID-19 Related Findings](https://arxiv.org/abs/2005.06465). This dataset consists of lung CT scans with COVID-19 related findings, as well as without such findings.

{% hint style="info" %}
For more information please see the [original Keras tutorial](https://keras.io/examples/vision/3D_image_classification/).‌
{% endhint %}

## Dataset: MosMedData <a id="dataset-mosmeddata"></a>

The MosMedData: Chest CT Scans with COVID-19 Related Findings Dataset \([_reference_](https://www.medrxiv.org/content/10.1101/2020.05.20.20100362v1)\) consists of lung CT scans with COVID-19 related findings, as well as without such findings.‌

![Image Source: https://keras.io/examples/vision/3D\_image\_classification/\#introduction&#x200C;](../../../.gitbook/assets/image%20%2871%29.png)

## Step 1: Keras/Tensorflow Model Script <a id="step-1-model"></a>

Grid supports Keras/Tensorflow runs from the CLI. For this demo, we're going to be using the code [here](https://github.com/aribornstein/Keras-3D-Image-Classification/blob/main/train.py) sourced from the Keras 3D Image Classification from CT Scans demo by [Hasib Zunair](https://hasibzunair.github.io/) from the Keras IO examples [repo](https://github.com/keras-team/keras-io/tree/master/examples) with minor modifications for [TensorBoard](https://www.tensorflow.org/tensorboard) integration. \[[Reference](https://keras.io/examples/vision/3D_image_classification/)\]

{% hint style="info" %}
When using the Keras Tensorboard callback make sure to set the log\_dir to './lightning\_logs/keras'
{% endhint %}

```python
tb_callback = tf.keras.callbacks.TensorBoard(log_dir='./lightning_logs/keras')
```

## Step 2: Start a RUN from the CLI <a id="step-2-start-a-run"></a>

Training this model on Grid has 4 simple steps:‌

### 1. Install and Sign into the Grid CLI

```text
pip install -U lightning-grid
grid login
```

### 2. Clone the repo

```text
‌git clone https://github.com/aribornstein/Keras-3D-Image-Classification.git
cd Keras-3D-Image-Classification
```

### 3. Use the CLI to start a Grid Run

```text
grid run train.py 
--instance_type g4dn.xlarge 
--framework tensorflow 
--gpus 1 
--max_epochs 5‌
```

This command tells grid to run our train script with the following configurations

* A 1xT4 \(16 GB\) $0.68/h \(g4dn.xlarge\) Accelerator `--instance_type g4dn.xlarge`
* Use the built-in GPU on the Accelerator`--gpus 1`
* Tensorflow as the grid framework `--framework tensorflow`
* Provide the run arguments `--max_epochs 5`

After running the CLI command above you should see this message.‌

![](../../../.gitbook/assets/image%20%2891%29.png)

## Step 3: View Model Run Metrics and Artifacts in Grid Web <a id="step-3-use-the-model-for-predictions"></a>

In this step, we log into the Grid Web Account to see our Metrics and Download the Grid weights

### 1. Login to [Grid.ai](https://www.grid.ai/) and Click "Get Started with Grid"

![](../../../.gitbook/assets/image%20%28117%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%282%29%20%283%29.png)

### 2. Select our Run and view Experiment Metrics

![](../../../.gitbook/assets/image%20%28110%29.png)

### 3. Download Artifacts from Grid Run

![](../../../.gitbook/assets/image%20%283%29.png)

Congratulations you have successfully run your first Tensorflow/Keras script with Grid.

{% hint style="info" %}
If using the Web UI to run this tutorial, simply copy and paste the [github script](https://github.com/aribornstein/Keras-3D-Image-Classification/blob/main/train.py) and choose "tensorflow" in the framework selection drop down
{% endhint %}

Here's a video of using Keras/TF example in Web UI

[https://www.loom.com/share/f00e6b67df9a49709886bc9beebff3dd](https://www.loom.com/share/f00e6b67df9a49709886bc9beebff3dd)

## Advanced Keras/TF Cuda Version Configuration <a id="bonus-cli-equivalent"></a>

Grid currently supports native Cuda integration for TensorFlow version 2.2.0. Support for more versions is on the roadmap however if you need to train with a different version of TensorFlow or Keras and use Cuda you can configure your run as follows using an [Actions](../../products/run-run-and-sweep-github-files/actions.md) YAML configuration as follows.

### 1. Identify the Corresponding Compatible Tensorflow/Keras Cuda Version

You can look at the updated table maintained by google [here](https://www.tensorflow.org/install/source#gpu).

### 2. Create a YAML Action Config in the same directory as your Train Script

```yaml
# Main compute configuration.
compute:

  # Add cloud configuration here.
  provider:

    credentials: PUT-GRID-KEY-HERE # Cloud key ID
    region: us-east-1              # Cloud region
    vendor: aws                    # Vendor, only aws

  # Training configuration.
  train:

    cpus: 1                        # Number of CPUs
    disk_size: 200                 # Disk size
    gpus: 1                        # Number of GPUs
    instance: g4dn.xlarge          # AWS instance type
    memory: null                   # RAM memory
    nodes: 0                       # Nodes to start with
    scale_down_seconds: 1800       # Second in between every scaling down evaluation
    datastore_name: null           # Datastore name to use 
    datastore_version: null        # Datastore version number
    datastore_mount_dir: null      # Where to mount the datastore

    actions:
      on_before_training_start:
        - conda install tensorflow-gpu==tensorflow-version-number cudatoolkit=corresponding-cuda-version-number -c anaconda -y 
        - pip install tensorflow-gpu==tensorflow-version-number
```

{% hint style="warning" %}
Be sure to specify the following parameters in the Yaml Config above

1. Grid API Key
2. Tensorflow Version Number
3. Corresponding Cuda Version Number
{% endhint %}

### 3. Pass the YAML Config to the Grid Run Command

```bash
grid run train.py --config config.yml
```

