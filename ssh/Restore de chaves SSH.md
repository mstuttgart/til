#ssh #infra #linux 

Copy both `id_rsa` and `id_rsa.pub` to `~/.ssh/`
Change file permissions and ownership of both files.

```bash
$ chown user:user ~/.ssh/id_rsa*
$ chmod 600 ~/.ssh/id_rsa
$ chmod 644 ~/.ssh/id_rsa.pub
```

- Start the ssh-agent.

```bash
$ exec ssh-agent bash
```

- Add your SSH private key to the ssh-agent.

```bash
$ ssh-add ~/.ssh/id_rsa
```

Now you’re ready to use Git and update your repositories.