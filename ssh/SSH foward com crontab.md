#ssh #infra #linux #ansible

Fonte: [https://stackoverflow.com/questions/2205282/ssh-agent-and-crontab-is-there-a-good-way-to-get-these-to-meet](https://stackoverflow.com/questions/2205282/ssh-agent-and-crontab-is-there-a-good-way-to-get-these-to-meet)

Assuming that you already configured SSH settings and that script works fine from terminal, using the **keychain** is definitely the easiest way to ensure that script works fine in crontab as well.

Since keychain is not included in most of Unix/Linux derivations, here is the step by step procedure.

**1.** Install the package:

```bash
sudo apt install keychain
```

2**.** Generate keychain files for your SSH key, they will be located in ~/.keychain directory. Example for id_rsa:

```bash
keychain ~/.ssh/id_rsa
```

3**.** Add the following line to your script anywhere before the first command that is using SSH authentication:

```bash
source ~/.keychain/$HOSTNAME-sh
```

I personally tried to avoid to use additional programs for this, but everything else I tried didn't work. And this worked just fine.

#linux 