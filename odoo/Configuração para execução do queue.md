#odoo 

Arquivo `odoo.cfg` deve estar com os seguintes valores para que o modulo queue funcione em ambiente de desenvolvimento:

```
### Rodar QUEUE
db_name = nomebanco
dbfilter = False
list_db = False
server_wide_modules = web,queue_job
```