#postgresql  #linux

```bash
for db in `psql -c '\\l' | grep *prefixo_banco* | cut -d '|' -f 1`; do dropdb $db; done
```

Comando útil para apagar vários bancos de dados de uma vez. Útil para ser utilizado com o runbot.