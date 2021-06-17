---
description: This tutorial shows how to train a forecasting model with Grid
---

# Coin Market Cap Price Forecasting

[![Grid](https://camo.githubusercontent.com/1b39d1721301ebc3d08db0971e6d4dd96db28d8028daff32eb3918e22cd1fbe0/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f7269645f41492d72756e2d3738464639362e7376673f6c6162656c436f6c6f723d626c61636b266c6f676f3d646174613a696d6167652f737667253262786d6c3b6261736536342c50484e325a79423361575230614430694e4467694947686c6157646f644430694e44676949475a7062477739496d3576626d5569494868746247357a50534a6f644852774f693876643364334c6e637a4c6d39795a7938794d4441774c334e325a79492b50484268644767675a443069545445674d5452324d6a42684d5451674d5451674d4341774d4445304944453061446c574d7a59754f4567784d693432566a4578614449794c6a56324e3267784d533479566a45305154453049444530494441674d44417a4d693430494442494d5456424d5451674d5451674d4341774d4445674d5452364969426d615778735053496a5a6d5a6d4969382b50484268644767675a44306954544d314c6a49674e44686f4d5445754d6c59794e5334315344497a4c6a6c324d5445754d3267784d53347a566a5134656949675a6d6c736244306949325a6d5a694976506a777663335a6e50673d3d)](https://platform.grid.ai/#/runs?script=https://github.com/gridai/gridai-timeseries-forecasting-demo/blob/fa48c4b5ae58f40263ad98d5fbc06fce92db11a4/train.py&cloud=grid&instance=g4dn.xlarge&accelerators=1&disk_size=200&framework=lightning&script_args=grid%20run%20--grid_config%20.grid%2Fconfig.yml%20train.py%20--max_epochs%20100%20--data_path%20%2Fdataset%2Fcryptocurrency_prices.csv%20--learning_rate%20%27uniform%280%2C0.03%2C5%29%27%20--hidden_size%20%27%5B16%2C32%2C64%5D)

## Goal

We show how to create a model that learns how to forecast the next N observations of a timeseries.

In this example, we will be creating a model that predicts future cryptocurrency values.

{% hint style="info" %}
This tutorial uses **PyTorch Forecasting**
{% endhint %}

### Step 1: Create Your Dataset

Our dataset is quite simple: it's a CSV file with the following structure :

```text
time_idx,Symbol,Date,High,Low,Open,Close,Volume,Marketcap
1,ADA,2017-10-02 23:59:59,0.0300877001136541,0.0199692994356155,0.0246070008724927,0.0259317997843027,57641300.0,628899051.78
2,ADA,2017-10-03 23:59:59,0.0274251997470855,0.0206898991018533,0.025756599381566,0.0208158008754253,16997800.0,539692714.905
```

We will training a series of models on Grid. Now, in order to make the process of updating the dataset easier we will be creating a [Grid Datastore](https://docs.grid.ai/products/add-data-to-grid-datastores). Datstores are collections of files that are versioned and can be mounted anywhere in the experiment context.

We'll be creating a new Datastore using the Grid CLI with the following command:

```text
$ grid datastores create --name crypto_prices --source data/
upload ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100.0%
✔ Finished uploading datastore.
```

Then check that your datsatore is ready to use by calling `grid datastores list`:

```text
$ grid datstores list
┏━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━┓
┃ Credential Id ┃                Name ┃ Version ┃     Size ┃          Created ┃    Status ┃
┡━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━┩
│ cc-grv4f      │       crypto_prices │       1 │  12.6 MB │ 2021-05-20 01:17 │ Succeeded │
└───────────────┴─────────────────────┴─────────┴──────────┴──────────────────┴───────────┘
```

Whenever your datastore has `Status` of `Succeeded` you are ready to go on training.

### Step 2: Train Your Model on Grid AI

You are now ready to train your model on Grid.

We'll be using the CLI but you can do the same thing by using the web UI. We have placed a configuration file locally \(`.grid/config.yml`\) that you can use as reference instead of passing all the parameters to the CLI manually.

```text
$ grid run --config .grid/config.yml \
           train.py \
           --max_epochs 100 \
           --data_path /dataset/cryptocurrency_prices.csv \
           --learning_rate "uniform(0,0.03,5)" \
           --hidden_size "[16,32,64]"

No --name passed, naming your run glossy-manatee-255
Using default cloud credentials cc-bwhth to run on AWS.

                Run submitted!
                `grid status` to list all runs
                `grid status glossy-manatee-255` to see all experiments for this run

                ----------------------
                Submission summary
                ----------------------
                script:                  train.py
                instance_type:           g4dn.xlarge
                distributed:             False
                use_spot:                True
                cloud_provider:          aws
                cloud_credentials:       cc-bwhth
                grid_name:               glossy-manatee-255
                datastore_name:          crypto_prices
                datastore_version:       1
                datastore_mount_dir:     /dataset
```

#### Bonus: Run a Hyperparameter Sweep

Grid AI makes it trivial to run a [hyperparameter sweep](https://docs.grid.ai/products/global-cli-configs/cli-api/grid-train#hyperparameter-sweeps) without having to change anything in your scripts. Let's experiment with a number of different learning rates for our model:

```text
$ grid run --config .grid/config.yml \
           train.py --max_epochs 100 \
           --data_path /dataset/cryptocurrency_prices.csv \
           --learning_rate "uniform(0,0.03,5)" \
           --hidden_size "[16,32,64]"
```

That will generate 15 experiments with different learning rate combinations.

### Attribution

This project relies heavily on the [PyTorch Forecasting](https://pytorch-forecasting.readthedocs.io/en/latest/) package. The implementation adapts from their documentation and tutorials.

The dataset used in this demo comes from [CoinMarketCap](https://coinmarketcap.com/), a cryptocurrency price-tracking service. We have downloaded a processed version of the data available on this [Kaggle page](https://www.kaggle.com/sudalairajkumar/cryptocurrencypricehistory).

