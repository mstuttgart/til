#linux #infra

Para verificar se uma porta está sendo usada:

```bash
netstat -na | grep tcp | grep -i listen
```

O comando acima vai exibir uma lista das portas que estão ocupadas. Exemplo de saída:

```bash
tcp        0      0 0.0.0.0:8069            0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:2000            0.0.0.0:*               LISTEN
tcp        0      0 192.168.122.1:53        0.0.0.0:*               LISTEN
tcp        0      0 127.0.1.1:53            0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN
tcp        0      0 127.0.0.1:5432          0.0.0.0:*               LISTEN
tcp6       0      0 :::22                   :::*                    LISTEN
tcp6       0      0 ::1:631                 :::*                    LISTEN
tcp6       0      0 :::25                   :::*                    LISTEN
tcp6       0      0 :::8025                 :::*                    LISTEN
```

O próximo passo é descobrir qual serviço está utilizando a porta que desejamos. Por exemplo, temos o Odoo executando na porta `8069`, executamos o comando a seguir:

```bash
netstat -tlpn | grep 8069
```

A saída do comando acima será algo como:

```bash
tcp        0      0 0.0.0.0:8069            0.0.0.0:*               LISTEN      29723/python3
```

Para saber qual o número do processo do serviço, basta verificarmos o número do processo (PID) após a palavra **LISTEN**. Em nosso caso de exemplo é `29723`.

Agora basta matarmos o serviço com:

```bash
sudo kill -9 29723
```