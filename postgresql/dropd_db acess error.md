Quando tentamos realizar o comando `dropdb <nomebanco>` e ainda existe alguma conexão com o banco, o Postgres nos retorna
a seguinte mensagem:

> dropdb: error: database removal failed: ERROR:  database "nomebanco" is being accessed by other users
DETAIL:  There is 1 other session using the database.

Antes de realizar o `dropdb`, devemos finalizar quaisquer conexões com o banco. Entre com o comando `psql`. O prompt vai mudar para:

```sh
postgres=#
```
Então execute o comando:

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
