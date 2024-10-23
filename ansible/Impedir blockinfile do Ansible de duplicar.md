#ansible

You should specify `{mark}` keyword in the `marker` parameter:

```yaml
marker: "## {mark} added by ansible (configuration elasticsearch)"
```

This will cause Ansible to insert a line at the beginning and at the end of the block replacing `{mark}` accordingly with `BEGIN` and `END`:

```yaml
## BEGIN added by ansible (configuration elasticsearch)
network.host: 0.0.0.0
path.data: /var/lib
path.logs: /var/log/elasticsearch
path.repo: /home/chris/elastic-backups
## END added by ansible (configuration elasticsearch)
```

Otherwise Ansible has no clue, where the block starts and where it ends, so on every run it considers the block is not present and inserts a new one.