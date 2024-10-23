#git

De vez em quando é interessante limpar a referencia de branchs que ja não são mais necessárias, podemos utilizar a flag *prune* do comando **fetch** para limpar referencia a branchs remotas

```bash
git feth --prune
```

ou

```bash
git fetch -p
```

Ainda assim permanecem no repositório branchs locais, que geralmente representam apenas sujeira, para remover tais branchs podemos utilizar a flag **merged**(isto listara todas a branchs 'merged' na branch atual) do comando branch, e utilizar a saida como argumento do mesmo comando (branch) utilizando a flag *-D*(Deleta branchs).

```bash
git branch --merged | tail -n +2 | xargs git branch -D
```

O comando `tail -n +2` serve para excluir da saida a primeira linha, que geralmente é a branch utilizada como referência para o comando.