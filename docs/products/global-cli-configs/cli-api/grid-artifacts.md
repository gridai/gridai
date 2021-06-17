# grid artifacts

Downloading artifacts using CLI is straightforward. you can download one specifying the experiment id or run id

## Run artifacts

Type the name of the run to download the folder of all artifacts

```text
grid artifacts the-run-name
```

which generates a folder with this structure \(assuming the run name is handsome-dog-665\)

![](../../../../.gitbook/assets/image%20%2875%29.png)

## Experiment artifacts

Download the artifacts for a particular experiment

```text
grid artifacts the-run-name-exp0
```

## Command parameters

### --download\_dir

Download all artifacts to a directory, following command  will download to the specified directory

```text
grid artifacts --download_dir the-directory 
```

For example, the command below will download to "dbrun"

```text
grid artifacts imdb-demo2-exp0 --download_dir dbrun
```



