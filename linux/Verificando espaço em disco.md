### Comando `df`: espaço em um sistema de arquivos

Para mostrar informações sobre os sistemas de arquivo nos quais cada ARQUIVO
reside ou, por padrão, sobre todos os sistemas de arquivos, podemos utilizar o comando  `df`.

Para checar o espaço em disco ocupado pelo diretório `/tmp` e `/opt`, usamos o comando `du`:

```bash
$ sudo df -h /opt /tmp

Sist. Arq.      Tam. Usado Disp. Uso% Montado em
/dev/nvme0n1p2  468G   86G  359G  20% /
/dev/nvme0n1p2  468G   86G  359G  20% /
```

O parâmetros são:

* `h` retorna os valores de um modo legível, usando 'KB', 'MB' e 'GB', por exemplo.

### Comando `du`: espaço do disco ocupado por um diretório

Para checar o espaço em disco ocupado pelo diretório `/tmp` e `/opt`, usamos o comando `du`:

```bash
sudo du -chs /opt /tmp
```

O parâmetros são:

* `h` retorna os valores de um modo legível, usando 'KB', 'MB' e 'GB', por exemplo.
* `s` lista todos os arquivos e nos mostra um resumo do resultado.
* `c` Exibe o tamanho total (quando pegamos mais de um diretorio ou um diretório com sub-diretórios).

```bash
$ sudo du -hs /opt /tmp

745M	/opt
404K	/tmp
745M	total
```