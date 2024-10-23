#nginx #linux #infra 

Para configurar o nginx de modo que ela permita acesso apenas para um determinado IP externo e negue acesso aos demais IPS externos, devemos configurar o arquivo de configuração do domínio (que fica no diretório `/etc/nginx/sites-avaliable`). Primeiramente precisamos do IP externo. Caso o IP desejado seja o nosso, podemos obtê-lo conforme o tutorial a seguir: 

[Como obter IP externo da maquina](Como%20obter%20IP%20externo%20da%20maquina%20cbba95ba2a574c49bb05bc2b4893d9ea.md) 

A configuração do arquivo nginx do domínio é feita conforme o exemplo abaixo, dentro da tag `location`:

```bash
  server {
    # listen 80;
    # server_name www.foo.bar;

    location / {
      # Outras configuracoes aqui

      # Adicionar aqui o IP publico que permanece com acesso
      allow   my.public.ip.here;
      deny    all;
    }
  }
```

Por precaução, vamos primeiro verificar se a configuração esta correta com o comando:

```bash
sudo nginx -t
```

Se nenhuma mensagem de erro aparecer, finalmente realizamos o *reload* do nginx:

```bash
sudo service nginx reload
```