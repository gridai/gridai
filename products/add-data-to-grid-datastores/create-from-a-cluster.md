# Create from a cluster

## Upload from a cluster

Use these instructions to upload from:

* Corporate cluster.
* Academic cluster.

First, start screen on the jump node \(to run jobs in the background\).

```bash
screen -S upload
```

If your jump node allows a memory-intensive process, then skip this step. Otherwise, request an interactive machine. Here's an example using SLURM.

```bash
srun --qos=batch --mem-per-cpu=10000 --ntasks=4 --time=12:00:00 --pty bash
```

Once the job starts, install and log into Grid \(get your username and ssh keys from the [settings page](https://platform.grid.ai/#/settings)\).

```bash
# install
pip install lightning-grid --upgrade

# login
grid login --username YOUR_USERNAME --key YOUR_KEY
```

Next, use the Datastores command to upload any folder:

```bash
grid datastores create --source imagenet_folder --name imagenet
```

You can safely close your ssh connection to the cluster \(the screen will keep things running in the background\).

