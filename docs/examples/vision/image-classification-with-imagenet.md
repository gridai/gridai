# ImageNet classification

## Goal

This tutorial shows scalable workflows motivated by building a classifier to train on the ImageNet dataset

In this tutorial you'll:

* Create an ImageNet **DATASTORE**
* Use a **SESSION** for creating the datastore and to prototype the model
* **RUN** a sweep of a classifier over ImageNet

{% hint style="info" %}
This tutorial uses **PyTorch Lightning**
{% endhint %}

## Tutorial time

There's a lot of waiting around for data downloads and uploads, but everything else takes just a few minutes.

* **2 minutes**   if you have an ImageNet Datastore
* * 2 hours    if you need to create an ImageNet datastore \(depends on the speed of your internet connection\)
* +6 hours     if you need to download and process ImageNet

## ImageNet

ImageNet is a dataset of natural images \(1000 classes\) with over 1.3 million images. It is about 100GB in size.

![](../../../.gitbook/assets/image%20%2862%29.png)

The challenges of working with ImageNet are:

* Scaling huge datasets across distributed workloads
* Prototyping models interactively with such a large dataset
* Scaling up models to run through ImageNet quickly

## Step 1: Get ImageNet

If you already have ImageNet, **SKIP THIS STEP**

{% hint style="warning" %}
Make sure you have permission to use ImageNet
{% endhint %}

### A: Start an Interactive Session

{% embed url="https://grid-docs.s3.us-east-2.amazonaws.com/screen\_3.mp4" caption="" %}

We'll use Jupyter Lab for simplicity but you can also directly link VSCode or ssh into the session from your laptop.

### B: Open Jupyter lab on the Session

It's a good practice to use screen for long-running processes.

Open a new terminal

![](../../../.gitbook/assets/image%20%2842%29.png)

Start screen so you can do the download in the background.

```bash
# install screen
sudo apt-get install screen

# start screen
screen -S train_download
```

### **C: Download ImageNet**

Make sure you first have access to ImageNet \(request access [here](http://www.image-net.org/signup.php?next=download-images)\).

Now login [here](http://www.image-net.org/login), and navigate [here](http://www.image-net.org/challenges/LSVRC/2012/2012-downloads) to see the download links. Download those links:

```bash
# download training data
wget http://PASTE_REAL_URL_HERE/ILSVRC2012_img_train.tar

# download validation data
wget http://PASTE_REAL_URL_HERE/ILSVRC2012_img_val.tar
```

You can safely close the Jupyter browser tab while the download happens. Once it's done, come back here.

{% hint style="info" %}
Download takes about 4 hours
{% endhint %}

### **C: Process ImageNet**

ImageNet needs to be processed. Use the following script \([source](https://gist.github.com/BIGBALLON/8a71d225eff18d88e469e6ea9b39cef4)\).

```bash
# downloads and starts a script to process ImageNet
wget -O - http://bit.ly/imagenet_process | bash
```

This will create two folders \(train, val\). Put them both under a single folder

```bash
# create a folder with the train and val splits
mkdir imagenet_2012
mv train imagenet_2012/
mv val imagenet_2012/
```

Download the meta.bin file and move it to the imagenet\_2012 folder

```bash
# get the meta.bin (an index of files) and move to the dataset folder
wget https://grid-docs.s3.us-east-2.amazonaws.com/meta.bin

# copy into each folder
cp meta.bin imagenet_2012/train
cp meta.bin imagenet_2012/val
```

that's it! In the next step we'll upload ImageNet.

## Step 2: ImageNet Datastore

Now let's upload and optimize ImageNet. We'll create a datastore that will make the dataset available at low-latency to every job we ever run using the dataset.

### From a Session

If you followed the previous step, you now have a folder with ImageNet processed. Uploading is trivial. Simply type:

make sure you're in a screen Session

```bash
screen -S upload
```

now upload the datastore

```bash
grid datastores create --source imagenet_2012 --name imagenet-2012
```

### From cluster or own machine

Most likely your copy of ImageNet lives on a cluster or your local machine. Either way, the process is the same.

#### Open your terminal and start a screen session.

Screen will let this job run in the background.

```bash
screen -S upload
```

If you're on a cluster, request an interactive machine \(**after** starting screen\). Here's an example using SLURM.

```bash
srun --qos=batch --mem-per-cpu=10000 --ntasks=4 --time=12:00:00 --pty bash
```

Install and log into grid \(get your username and ssh keys from the [settings page](https://platform.grid.ai/#/settings)\).

```bash
# install
pip install lightning-grid --upgrade

# login
grid login --username YOUR_USERNAME --key YOUR_KEY
```

Create the ImageNet Datastore

```bash
grid datastores create --source PATH/TO/imagenet --name imagenet-2012
```

You can safely disconnect from the cluster \(make sure you are using screen\) while the upload happens. This will take a few hours depending on your cluster's internet connection.

## The Model

You can do hyperparameter sweep over different model backbones to find the best one for ImageNet.

The hardest part here is getting the data into the system. Using Lightning with Grid makes it trivial to scale up on ImageNet.

Grid supports other machine learning frameworks as long as your code supports multi-GPU and multi-node training. Let us know if you would like to contribute sample code for Imagenet training

