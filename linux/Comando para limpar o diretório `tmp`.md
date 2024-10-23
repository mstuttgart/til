#linux #infra

Com o tempo de uso, o diretório `/tmp` pode ficar cheio de arquivos temporários, ocupando um espaço em disco considerável. Isso normalmente é resolvido reiniciando o SO, caso em que o conteúdo da pasta é perdido. Porém em alguns casos, como servidores, não é interessante reiniciarmos o servidor. Nesse caso, podemos apagar o conteúdo mais antigo da pasta `/tmp` através do comando:

```bash
sudo find /tmp -type f -atime +5 -delete
```

No comando acima, apagamos os arquivos mais antigos do que 5 dias.