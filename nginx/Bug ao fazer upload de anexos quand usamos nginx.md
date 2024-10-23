#nginx #linux #infra 

Este erro ocorre quando anexamos algum arquivo ao Odoo. A tela de loading fila carregando e não retorna mesmo após o anexo ser enviado.

Realizando a inspeção da tela durante o carregamento do anexo, verificou-se que ocorre um erro permissão:

```bash
X-Frame-Options set to Deny
```

Isso é feito para evitar que outros renderizem o conteúdo do nosso site, o que não é o caso do Odoo, logo devemos mudar essa opção para permiti renderizar o frame corretamente após o final do carregamento.
vamos editar o arquivo `/etc/nginx/snippets/ssl.conf`

```bash
sudo nano /etc/nginx/snippets/ssl.conf
```

E comentar a seguinte linha:

```bash
add_header X-Frame-Options DENY;
```

e logo abaixo dela adicionamos

```bash
#add_header X-Frame-Options DENY;
add_header X-Frame-Options SAMEORIGIN;
```

Agora basta reiniciar o nginx

```bash
sudo service nginx restart
```

### Fonte:

- [https://serverfault.com/a/801680](https://serverfault.com/a/801680)