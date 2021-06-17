---
description: Some cool Tips and Tricks using Grid Platform
---

# Tips & Tricks

### Interruptible Runs

Interruptible Runs powered by spot instances are **50-90%** cheaper but a machine can be interrupted at anytime. If you are using PyTorch Lightning and a job gets interrupted you can load the checkpoints. 

Grid helps you directly continue your Runs where you left off as follows.

```bash
if __name__ == '__main__':
    parser = ArgumentParser()
    parser.add_argument('--checkpoint_path', type=str)
    args = parser.parse_args()
    if args.checkpoint_path:
        trainer = LitModel.load_from_checkpoint(checkpoint_path=args.checkpoint_path)
grid run --g_use_spot train.py --checkpoint_path "Artifact URL "
```

For more information check out 

* [Interruptible Pricing](https://docs.grid.ai/platform/billing-rates)
* [Grid Artifacts](https://docs.grid.ai/products/run-run-and-sweep-github-files/artifacts)
* [Lightning Loading Checkpoints](https://pytorch-lightning.readthedocs.io/en/latest/common/weights_loading.html)

### AutoStructuring Deep Learning Training

The recent 1.3 Release of PyTorch Lightning provides a new Lightning CLI \[beta\] for [Auto Structuring Deep Learning Training](https://devblog.pytorchlightning.ai/auto-structuring-deep-learning-projects-with-the-lightning-cli-9f40f1ef8b36).

```bash
from pytorch_lightning.utilities.cli import LightningCLI
LightningCLI(MyModel, MyData, trainer_defaults={'max_epochs': 10})
```

When combined with Grid, the Lightning CLI enhances  your train scripts, enabling you quickly take advantage of any hardware configuration and perform Grid Data, Model and Trainer sweeps without having to integrate external libraries or add extra code. For more information check out:

* [Auto Structuring Deep Learning Projects with the Lightning CLI](https://devblog.pytorchlightning.ai/auto-structuring-deep-learning-projects-with-the-lightning-cli-9f40f1ef8b36)
* [Configuring Grid Hyper Parameter Sweeps](https://docs.grid.ai/products/run-run-and-sweep-github-files/sweep-syntax)
* [PyTorch Lightning CLI Docs](https://pytorch-lightning.readthedocs.io/en/latest/common/lightning_cli.html)

### Early Stopping

The recent 1.3 Release of PyTorch Lightning provides 3 New Thresholds for Early Stopping \(Stopping, Divergence, and Check Finite\) that can save you significant money on your Grid Runs.

The [EarlyStopping](https://pytorch-lightning.readthedocs.io/en/latest/common/early_stopping.html) Callback in Lightning allows the Trainer to automatically stop when a given metric stops improving. You can define your own custom metrics or take advantage of our [TorchMetrics package](https://bit.ly/2RxOvVp) to select common metrics to log and monitor. Early Stopping is perfect for  [Grid Runs](https://docs.grid.ai/products/run-run-and-sweep-github-files#runs) because it limits the time spent on experiments that lead to poor convergence or overfitting. 

Using EarlyStopping Thresholds into your PL Runs is a simple as adding the following few lines to your code.

```bash
from pytorch_lightning.callbacks import EarlyStopping
from pytorch_lightning import Trainerearly_stopping = EarlyStopping(
 monitor="val_loss",
 stopping_threshold=1e-4, # Stops training immediately once the monitored quantity reaches this threshold
 divergence_threshold=9.0, # Stops training as soon as the monitored quantity becomes worse than this threshold
 check_finite=True, # Stops training if the monitored metric becomes NaN or infinite.
)
trainer = Trainer(callbacks=[early_stopping])
```

You can then pocket the savings or reinvest  them into more promising configurations to take your model performance and convergence to the next level. For more information check out:

* [Grid Run Docs](https://bit.ly/3fyBRgT)
* [Early Stopping Docs](https://bit.ly/3fnIUZu)
* [Torch Metrics Package](https://bit.ly/2RxOvVp)

### Sessions and data files

Sometimes you need a quick way of copying files from your local machine to your grid session. I recently had to do this in order to configure the Kaggle CLI for a competition I was working on.Grid Sessions provide two clean options for uploading local files.

**Secure Copy SCP**

Once you’ve configured [SSH with the Grid CLI](https://docs.grid.ai/products/sessions/how-to-ssh-into-a-session?utm_source=slack&utm_medium=social&utm_campaign=tip-of-week) you can quickly copy files to your session with the scp command as follows

```text
scp local_file grid_session_name:~path_to_copy_to/
```

 **Using** [**Jupyter Lab**](https://docs.grid.ai/products/sessions/jupyterlab-with-sessions?utm_source=slack&utm_medium=social&utm_campaign=tip-of-week)\*\*\*\*

If the CLI is not your thing;  you can also upload files using jupyter hub

[This video](https://www.youtube.com/watch?time_continue=14&v=1bd2QHqQSH4&feature=emb_title) shows you how to do that. For more information check out:

* [Grid Sessions Docs](https://docs.grid.ai/products/sessions?utm_source=slack&utm_medium=social&utm_campaign=tip-of-week)
* [SSH into a Grid Session](https://docs.grid.ai/products/sessions/how-to-ssh-into-a-session?utm_source=slack&utm_medium=social&utm_campaign=tip-of-week)
* [SCP Command](https://linuxize.com/post/how-to-use-scp-command-to-securely-transfer-files/)
* [JupyterLab with Sessions](https://docs.grid.ai/products/sessions/jupyterlab-with-sessions?utm_source=slack&utm_medium=social&utm_campaign=tip-of-week)
* [JupyterLab Uploading and Downloading Files](https://jupyterlab.readthedocs.io/en/stable/user/files.html#uploading-and-downloading)

### Keeping track of costs

Have you ever wanted to estimate exactly how much a cloud training run will cost you.Well with PyTorch Lightning and Grid now you can.

The recent 1.3 Release of PyTorch Lightning provides a new trainer flag called [max\_time](https://pytorch-lightning.readthedocs.io/en/1.3.1/common/trainer.html?utm_source=social&utm_medium=slack&utm_campaign=tip_of_week#max-time) that can enable you to stop your  [Grid Run](https://docs.grid.ai/products/run-run-and-sweep-github-files#runs) and save a checkpoint when you’ve reached the max allotted time. 

Combined with Grid's ability to estimate how much a run will cost you per an hour you can use this flag to better budget your experiments.

```bash
# Default (disabled)
trainer = Trainer(max_time=None)# Stop after 12 hours of training or when reaching 10 epochs (string)
trainer = Trainer(max_time="00:12:00:00", max_epochs=10)# Stop after 1 day and 5 hours (dict)
trainer = Trainer(max_time={"days": 1, "hours": 5})
```

With this trick you can better manage your training budget and invest it  into more promising configurations to take your model performance and convergence to the next level.For more information check out:

* [Grid Run Docs](https://bit.ly/3fyBRgT)
* [Max Time Docs](https://pytorch-lightning.readthedocs.io/en/1.3.1/common/trainer.html?utm_source=social&utm_medium=slack&utm_campaign=tip_of_week#max-time)

