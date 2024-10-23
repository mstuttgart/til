#odoo 

Para que a criação ou upload de um novo banco de dados ocorra de forma correta, deve-se desabilitar a conexão do pgboucer, da acordo com os seguites parâmetros:

### Antes
```shell
db_port = 6432
.
.
.
server_wide_modules = web,queue_job,bus_alt_connection
```

### Depois
```shell
db_port = 5432
.
.
.
server_wide_modules = web,queue_job
```

Após a criação/upload do banco e configuração, as configurações do pgbouncer podem ser restauradas normalmente.