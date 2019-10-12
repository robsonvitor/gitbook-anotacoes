# Git

Termos:

* Branch:
* Issue:
* Tag:
* Merge:
* Fork:
* Pull
* Push
* Rebase
* Commit
* Retirar arquivos da staging area \(git add\)

```text
Remove tudo: git reset . | Remove apenas um arquivo: git reset nome_arquivo
```

* Entrar em uma branch

```text
git checkout nome_branch
```

* Criar branch e alterar para ela

```text
git checkout -b nome_branch
```

* Criar branch com base em outra branch

```text
git checkout -b nova_branch branch_original
```

* Apagar branch

```text
git branch -d nome_branch
```

* Apagar branch remota

```text
git push origin :nome_da_branch
```

* Enviar uma branch local para o remoto

```text
git push origin nome_da_branch_local
```

* Visualizar alterações realizadas por um usuário específico

```text
git log --author="nome" -p /codigos
```

* Realizar merge, entrar na branch que será mantida, ou seja, onde o código receberá o merge

```text
git merge branch_temporaria
```

[https://blogdoatila.wordpress.com/2014/08/23/lista-bem-completa-de-comandos-git/](https://blogdoatila.wordpress.com/2014/08/23/lista-bem-completa-de-comandos-git/)

[https://gist.github.com/leocomelli/2545add34e4fec21ec16](https://gist.github.com/leocomelli/2545add34e4fec21ec16)

[https://githowto.com/pt-BR](https://githowto.com/pt-BR)

