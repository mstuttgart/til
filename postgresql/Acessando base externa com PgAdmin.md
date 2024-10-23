#postgresql 
Podemos divir esta tarefa em 3 etapas

### Primeira etapa

Primeiro fazemos o PostgreSQL ouvir conexões externas. Para isso precisamos abrir o arquivo `postgresql.conf`:

```bash
sudo nano /etc/postgresql/9.6/main/postgresql.conf
```

**NOTA**: 9.6 representa  a versão do PostgreSQL instalado.

Substitua a seguinte linha do arquivo

```bash
listen_addresses = 'localhost'
```

por

```bash
listen_addresses = '*'
```

### Segunda etapa

Permitir o PostgreSQL receber conexões externas. Abra o arquivo `pg_hba.cong`

```bash
/etc/postgresql/9.6/main/pg_hba.conf
```

**NOTA**: 9.6 representa  a versão do PostgreSQL instalado.

Adicione a seguinte regra no arquivo:

```bash
host    all    all    0.0.0.0/0    md5
```

Isso permite qualquer IP de se logar no PostgreSQL através da senha definida do usuario do banco.

### Terceira etapa

Reiniciar o PostgreSQL com o comando:

```bash
sudo /etc/init.d/postgresql restart
```