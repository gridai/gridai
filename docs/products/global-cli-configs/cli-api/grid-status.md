# grid status

## Status of Runs and Sessions

Shows the status of runs and sessions

```text
grid status
```

![](../../../.gitbook/assets/image%20%28123%29.png)

## Status of experiments

See the status of every experiment within a run.

```text
grid status the-run-name
```

![](../../../.gitbook/assets/image%20%281%29.png)

## Command parameters

### `--details`

Use this to view any logs when a run failed.

```text
grid status the-run-name --details
```

### `--export`

Exports all active runs or experiments in select format, either `csv` or `json`. This is useful if you would like to store the CLI output and refer to it later. 

```text
grid status --export csv
✔ Loading Runs...
┏━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━┳━━━━━━━━━━━━━┳━━━━━━━━━━━━━┳━━━━━━━━━┳━━━━━━━━┳━━━━━━━━━━━┳━━━━━━━━┳━━━━━━━━━━━┓
┃ Run                 ┃             Project ┃  Status ┃    Duration ┃ Experiments ┃ Running ┃ Queued ┃ Completed ┃ Failed ┃ Cancelled ┃
┡━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━╇━━━━━━━━━━━━━╇━━━━━━━━━━━━━╇━━━━━━━━━╇━━━━━━━━╇━━━━━━━━━━━╇━━━━━━━━╇━━━━━━━━━━━┩
│ laughing-beagle-647 │ gridai/Demo_Project │ running │ 0d-04:05:23 │           1 │       1 │      0 │         0 │      0 │         0 │
└─────────────────────┴─────────────────────┴─────────┴─────────────┴─────────────┴─────────┴────────┴───────────┴────────┴───────────┘

43 Run(s) are not active. Use `grid history` to view your Run history.

Exported status to file: grid-status-2020-09-09_13:31.csv
```

