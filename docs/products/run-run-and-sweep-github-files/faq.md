# FAQ

## The cost changed during a run?

Grid provides estimates of ongoing costs. Once a run terminates we compute the final cost.

## How do I find out what packages are pre-installed in the cloud machine?

Cloud machines are configured in a simple way with only what is needed to run the scripts in the framework of choice.

## What machine learning frameworks does Grid support?

Grid is optimized for PyTorch Lightning. It also supports Tensorflow, Keras any framework built on top of PyTorch.

Try this repository for running Keras example: [https://github.com/gridai/hello\_mnists/blob/443d9522/keras.py](https://github.com/gridai/hello_mnists/blob/443d9522/keras.py)

Grid can also run non-deep learning focused workloads such as plain numpy, sklearn, etc..

## I'm using an in-house ML library. Can I use it with Grid?

Grid can run arbitrary python scripts. You're free to run whatever you want inside a script. However, Grid is optimized for Pytorch, Pytorch Lightning, Tensorflow, Keras, numpy and sklearn.

