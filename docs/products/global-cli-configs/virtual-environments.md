# Virtual Environments

## Conda

We recommend you use conda when installing the Grid CLI. This is a best practice to making your project reproducible.

### Install conda

If you don't yet have a conda environment, here's how to set it up

First, [install miniconda](https://docs.conda.io/en/latest/miniconda.html).

Then create the conda environment

```bash
conda create --name pick_a_name python=3.7
```

### Install Grid

To install Grid in your conda environment, use this command:

```bash
# first active the environment
conda activate pick_a_name

# install grid
pip install lightning-grid
```

## Virtual environment

An alternative to conda is to use virtual environment. In the machine learning world, the standard is conda. However, if you still want to use virtual environment, do the following:

```
python3 -m venv ~/gridai
```

```text
source ~/gridai/bin/activate
pip3 install lightning-grid --upgrade
python3 -m pip install --upgrade pip
```

