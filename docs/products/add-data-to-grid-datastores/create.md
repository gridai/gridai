---
description: How to create datastores.
---

# Create

## Small datasets

You can use the UI to create datastores for datasets smaller than 1GB \(files or folder\).

Select the file or folder and click upload.

![](../../../.gitbook/assets/ds_upload%20%283%29%20%281%29%20%281%29.gif)

{% hint style="info" %}
You can still use the CLI for these datastores!
{% endhint %}

## Large datasets \(1 GB+\)

For datasets larger than 1 GB, use the CLI.

{% hint style="info" %}
If you have a datastore that is 1Gb+, we suggest creating an Interactive Session and uploading the datastore from there. Internet speed is much faster in Interactive Sessions, so upload times will be shorter.
{% endhint %}

First, install the grid CLI and login

```bash
pip install lightning-grid --upgrade
grid login
```

Next, use the datastores command to upload any folder:

```bash
grid datastore create --source imagenet_folder --name imagenet
```

This method can work from:

* A laptop.
* An interactive session.
* Any machine with an internet connection and Grid installed.
* A Corporate cluster.
* An Academic cluster.

## Datastores from .zip

For any datasets from a .zip, .tar or tar.gz that DO NOT require any post-processing, feel free to use the Web UI.

The link will be downloaded, extracted and automatically mounted for you. You can use an interactive Session to verify for yourself.

![](../../../.gitbook/assets/zip_ds%20%281%29.gif)

{% hint style="info" %}
You can still use the CLI for these datastores!
{% endhint %}

