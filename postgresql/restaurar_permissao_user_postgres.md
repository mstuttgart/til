Se o usuário `postgres` criado pelo Postgresql não tiver a permissão  `SUPERUSER`, ou se a mesma tiver sido removida por algum motivo, podemos restaurá-la
seguindo os passos abaixo:

Primeiro encerramos o servido do postgres

> sudo service postgres stop

Em seguida, mudamos para o usuario `postgres` do sistema (não confundir com usuário `postgresq` do banco):

> sudo su - postgres

Agora iniciamos o `postgres` em modo `single-user`. Esse modo não tem restrições de permissão, o que vai nos permitir colocar o usuario `postgres` como `SUPERUSER`.
Isso é realizado com o seguinte comando (postgresql 14 e ubuntu 22.04):

```sh
/usr/lib/postgresql/14/bin/postgres --single -D /var/lib/postgresql/14/main  -c "config_file=/etc/postgresql/14/main/postgresql.conf" postgres
```
Assim que o serviço iniciar, entre com o seguinte comando:

```sh
ALTER ROLE postgres SUPERUSER
```
Após confirmar o comando, sai do prompt do single user com `ctrl+d`.

Feito isso, podemos reiniciar o Postgresql novamente

> sudo service postgres start

Fonte: https://dba.stackexchange.com/questions/61781/restoring-the-superuser-account-on-the-postgres-server
