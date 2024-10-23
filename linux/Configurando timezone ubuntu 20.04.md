Para verificar a timezone atual:

```shell
$ timedatectl
               Local time: Thu 2019-12-05 23:22:43 UTC
           Universal time: Thu 2019-12-05 23:22:43 UTC
                 RTC time: Thu 2019-12-05 23:22:43
                Time zone: Etc/UTC (UTC, +0000)

System clock synchronized: no
              NTP service: inactive
            RTC in local TZ: no
```

Para definir a timezone, usamos o comando:

```shell
sudo timedatectl set-timezone timezone_escolhida
```

Para verificar as timezones disponiveis, usamos o comando:

```shell
timedatectl list-timezones
```