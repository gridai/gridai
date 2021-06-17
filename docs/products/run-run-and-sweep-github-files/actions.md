# Actions

## About Actions

Grid Actions give you the flexibility of adding steps to your training workflow without having to change your training script.

Example uses of actions:

* Installing libraries like Apex
* Downloading data
* Processing something
* ...

## Available Actions

### on\_image\_build

These are executed as your project image is built. We cache these commands on every git SHA. This is useful for installing dependencies and other system setup tasks.

```text
compute:
  train:

    actions:
      on_image_build:
        - apt-get install wget -y
        - pip install tqdm
```

{% hint style="info" %}
Commands automatically run as sudo
{% endhint %}

### on\_before\_training\_start

Arbitrary commands that run just before your training process starts. This is useful for downloading and preparing data, etc.

```text
compute:
  train:

    actions:
      on_before_training_start:
        - bash download_dataset.sh
```

### on\_after\_training\_end

Runs after your script stops. This is useful for post-processing data, sending alerts and notifications to your systems, etc.

```text
compute:
  train:

    actions:
      on_after_training_end:
        - apt-get install curl -y
        - curl -X GET http://webhook.com?success=true
```

## Configuring Actions

You can configure Grid Actions by using a Grid YAML file \(see details on [Grid YML\)](yaml-configs/).

Here's a full example of a Grid config YML using actions:

```text
compute:

  provider:
    credentials: cc-wv4l9
    region: us-east-1
    vendor: aws

  train:
    cpus: 1
    disk_size: 200
    gpus: 0
    instance: t2.xlarge
    memory: null
    nodes: 0
    scale_down_seconds: 1800

    # Actions need to be passed as one command
    # per line.
    actions:
      on_image_build:
        - apt-get install wget -y
        - pip install tqdm

      on_before_training_start:
        - bash download_dataset.sh

      on_after_training_end:
        - apt-get install curl -y
        - curl -X GET http://webhook.com?success=true
```

As you can see, you can pass one command per line. You can pass as many commands as you'd like.

