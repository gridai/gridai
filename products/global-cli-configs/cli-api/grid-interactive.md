# grid session

Launch an interactive Session with the hardware and data of your choice.

## create

Creates an interactive Session.

```text
grid session create
```

Allowed parameters:

| flag | description | optional |
| :--- | :--- | :--- |
| --credential | The cloud credential to use with the session | yes |
| --disk\_size | Disk size of the session | yes |
| --instance\_type | Cloud machine type | yes |
| --name | Name of the Session | yes |
| --config | Points to a YAML config file | yes |
| --description | Description of the interactive session | yes |
| --datastore\_\_\_name | Name of datastore to be mounted in interactive session | yes |
| --datastore\_version | Version of datastore to be mounted in interactive session | yes |

\| --datastore\_mount\_dir \| Absolute path to mount Datastore in interactive session \| yes \|

```text
grid session create --instance_type 2_cpu_4gb
```

{% hint style="warning" %}
Interactive sessions cannot be re-used after deletion.
{% endhint %}

## delete

Deletes an interactive session.

```bash
grid session delete the-session-name
```

{% hint style="warning" %}
Deleting a session deletes all files on that machine. To keep the files consider pausing instead.
{% endhint %}

## mount

Mount interactive session directory to local.  
To mount a filesystem use: `ixSession:[dir] mountpoint`

**Example 1:** Mounts the home directory on the interactive session in dir `data`

```bash
grid session mount bluberry-122 ./data
```

**Example 2:** Mounts `~/data` directory on the interactive session to `./data`

```bash
grid session mount bluberry-122:~/data ./data
```

**To unmount the session:**

```bash
fusermount3 -u mountpoint # Linux
umount mountpoint # OS X, FreeBSD
```

## pause

Pauses an interactive session.

```bash
grid session pause bluberry-122
```

## resume

Resumes an interactive session.

```bash
grid session resume bluberry-122
```

## ssh

SSH to interactive session.

First, create an ssh key

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Now add it to grid

```bash
grid ssh-keys add lit_key ~/.ssh/ed25519.pub
```

then ssh into the Session

```bash
grid session ssh happy-owl-123
```

## sync-ssh-config

Sync interactive session's ssh config to the local ssh config.

It manages a section within the ssh config file for all interactive sessions ssh config details.

Afterwards you can use the system's ssh & related utilities \(sshfs, rsync, ansible, etc\) with interactive sessions directly.

The default file is `~/.ssh/config` and can be changed via envvar `GRID_SSH_CONFIG`

