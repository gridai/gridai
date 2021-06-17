# grid logs

To view logs for an experiment use:

```text
grid logs the-experiment-name
```

Logs show two sections, build logs and stdout logs.

```bash
# build logs
[build] [2021-04-20T01:42:31.045408+00:00] Task experiments-cd13d646-cf31-486a-a78f-2e4a825e27dd created.
...

# stdout logs
[stdout] [2021-04-20T01:47:59.723077+00:00] Restoring data from /gridai/project/lightning_logs to .
[stdout] [2021-04-20T01:48:06.702111+00:00] --------------------------------------------------
[stdout] [2021-04-20T01:48:06.702137+00:00] GPUS: There are 1 GPUs on this machine
[stdout] [2021-04-20T01:48:06.702144+00:00] --------------------------------------------------
[stdout] [2021-04-20T01:48:06.702150+00:00] PARAMS: I want to eat: 3 pear
[stdout] [2021-04-20T01:48:06.702184+00:00] --------------------------------------------------
[stdout] [2021-04-20T01:48:06.702192+00:00] i can run any ML library like numpy, pytorch lightning, sklearn pytorch, keras, tensorflow
[stdout] [2021-04-20T01:48:06.702199+00:00] torch: tensor([0.6885]) numpy [0.9643539]
```

## Build logs

Sometimes an experiment may fail because a dependency install can be wrong, or something happens during the environment build.

These kinds of failures can be found in the build logs.

```bash
[build] [2021-04-20T01:42:31.045408+00:00] Task experiments-cd13d646-cf31-486a-a78f-2e4a825e27dd created.
```

## Experiment logs

For outputs of the file, look at the stdout logs. If your file throws an exception, that will appear here.

```text
# stdout logs
[stdout] [2021-04-20T01:47:59.723077+00:00] Restoring data from /gridai/project/lightning_logs to .
[stdout] [2021-04-20T01:48:06.702111+00:00] --------------------------------------------------
[stdout] [2021-04-20T01:48:06.702137+00:00] GPUS: There are 1 GPUs on this machine
[stdout] [2021-04-20T01:48:06.702144+00:00] --------------------------------------------------
[stdout] [2021-04-20T01:48:06.702150+00:00] PARAMS: I want to eat: 3 pear
[stdout] [2021-04-20T01:48:06.702184+00:00] --------------------------------------------------
[stdout] [2021-04-20T01:48:06.702192+00:00] i can run any ML library like numpy, pytorch lightning, sklearn pytorch, keras, tensorflow
[stdout] [2021-04-20T01:48:06.702199+00:00] torch: tensor([0.6885]) numpy [0.9643539]
```

## Command arguments

### --n\_lines 

Number of log lines \(from the end\) to return. 

### --page  

When an experiment is finished, logs are given in pages. This specificies which page to fetch from archived logs.

### --max\_lines

Maximum number of lines to print in terminal 

### --use\_pager 

Allows interactive / scrollable logs

