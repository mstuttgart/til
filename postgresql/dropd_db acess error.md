# Drop Database

Quando tentamos realizar o comando `dropdb <nomebanco>` e ainda existe alguma conexão com o banco, o Postgres nos retorna
a seguinte mensagem:

> dropdb: error: database removal failed: ERROR:  database "nomebanco" is being accessed by other users
DETAIL:  There is 1 other session using the database.

Antes de realizar o `dropdb`, devemos finalizar quaisquer conexões com o banco. Entre com o comando `psql`. O prompt vai mudar para:

```sh
postgres=#
```

# Postgres 13+

A versão 13 do Postgresql adicionou o comando `FORCE` que força o encerramento de todas as conexões e realiza a exclusão
do banco:

```sh
DROP DATABASE nomebanco WITH (FORCE);
```

# Postgres 12 and older

Nas versões anteriores, precisamos temos que impedir o banco de receber futuras conexões (caso contrário, o postgresl irá criar novas conexões assim que encerrarmos as existentes).

```sh
REVOKE CONNECT ON DATABASE nomebanco FROM public;
```

Agora, encerramos todas as conexões:

```sh
SELECT pg_terminate_backend(pg_stat_activity.pid) FROM pg_stat_activity WHERE pg_stat_activity.datname = 'nomebanco';

 pg_terminate_backend
----------------------
 t
(1 row)
```
Após o comando acima, agora podemos apagar o banco normelmente. Sai do `psql` (usando ctrl+d) e execute o comando de drop:

```
dropdb nomebanco
```

Post original: https://stackoverflow.com/questions/17449420/postgresql-unable-to-drop-database-because-of-some-auto-connections-to-db/68982312#68982312

