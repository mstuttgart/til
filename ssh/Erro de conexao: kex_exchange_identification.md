Eu conectei no ssh usando o verbose: ssh ubuntu@ip_do_server -vvv

Dai deu o seguinte erro: 

```
debug1: kex_exchange_identification: banner line 0: Exceeded MaxStartups
kex_exchange_identification: read: Connection reset by peer
Connection reset by xxx.yy.zzz.ww port 22

```

Eu dei uma pesquisada sobre o MaxStartups: https://stackoverflow.com/a/63174013/6085378
Eu resolvi alterando o número da config. MaxStartup no arquivo `/etc/ssh/sshd_config` e depois reiniciando o daemon do ssh `sudo service sshd restart`
Fazendo esse procedimento, o ssh voltou a aceitar minhas conexões de primeira. 