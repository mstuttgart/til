O comando a seguir permite mover todos os arquivos do formato `*.mkv` presente no diretorio atual e subdiretorios e movê-los para um diretiroi chamado `filmes`.

```bash
find . -iname *.mkv | while read f; do mv "$f" filmes; done
```

Remover diretorio `node_modules` de varios submodulos:

```bash
find javascript/ -iname node_modules | while read f; do rm -rf "$f"; done
```