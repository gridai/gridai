# Create from a Session

## Upload via Interactive Session

For huge datasets that need processing or a lot of manual work, we recommend this flow:

* launch an Interactive Session 
* download the data
* process it
* upload

![](../../../.gitbook/assets/upload_session.gif)

## Screen

When you are in the interactive Session, use Screen to make sure you don't lose your progress.

```bash
# start screen (lets you close the tab without killing the process)
screen -S some_name
```

now do whatever processing you need:

```bash
# download, etc...
curl http://a_dataset
unzip a_dataset

# process
do_something
something_else
bash process.sh
...
```

when you're done, upload to Grid via the CLI \(on the Interactive Session\):

```bash
grid datastores create --source imagenet_folder --name imagenet
```

{% hint style="info" %}
Grid CLI is auto-installed on sessions and logged in under your credentials.
{% endhint %}

## ImageNet Example

To see it in action, check out this tutorial

{% page-ref page="../../examples/vision/image-classification-with-imagenet.md" %}

