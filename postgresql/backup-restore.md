## Backup

Para realizar o `backup`, primeiro precisamos logar como usuário `postgres`. No terminal entre com:

```bash
sudo su - postgres
```

É possível visualizar a lista de bancos existentes na sua máquina através do comando abaixo:

```sql
psql -l
```

Agora, vamos realizar o backup do banco com o seguinte comando:

```sql
pg_dump -Fc nome_banco > nome_banco_backup.dump
```

Assim será criado um arquivo com a extensão `.dump` no diretório `/var/lib/postgressql`.

Também podemos incrementar o comando de modo a deixarmos registrado o dia, hora e minuto em que o `backup` foi realizado, algo muito útil caso você precise realizar a restauração do banco.

```sql
pg_dump -Fc nome_banco > nome_banco-backup-`date +%Y-%m-%d-%H-%M`.dump
```

## Restore

A restauração do banco é tão simples quanto o `backup`.
Primeiramente, vamos criar uma entrada para o banco que será restaurado. 

```sql
createdb nome_banco -O nomeusuario 
```
Onde `nome_usuario` é o usuario que sera dono do banco de dados recém-criado.

Apenas uma observação, antes de criar uma entrada para o novo banco, é uma boa prática verificar se já não existe outro banco com o mesmo nome. Isso pode ser feito com o comando `psql -l`.

Finalmente realizamos o `restore` do banco com o comando:

```sql
pg_restore -d banco_do_cliente_x banco_backup.dump
pg_restore -U nome_usuario -d nome_banco nome_banco-backup.dump -h 127.0.0.1 --no-owner

# ou para arquivos .sql

psql -U nome_usuario -d nome_banco -f backupfile.sql -h 172.0.0.1

# ou

psql -U nome_usuario -d nome_banco -f backupfile.sql -h localhost
```

O `nome_usuario` e `--no-pwner` garantem que o postgres não vai tentar restaurar o banco com o mesmo usuario que foi usado no backup. Isso é util em situações onde o usuario do banco é diferente do usuário que sera o novo dono do banco.
