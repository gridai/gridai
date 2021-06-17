# grid ssh-keys

This allows you to create ssh keys and add them to Grid.

Generate ssh key before adding to Grid.

```yaml
# make the ssh key (if you don't have one)
ssh-keygen -b 2048 -t rsa -f ~/.ssh/grid_ssh_creds -q -N ""

# add the keys to grid
grid ssh-keys add key_1 ~/.ssh/id_rsa.pub
```

