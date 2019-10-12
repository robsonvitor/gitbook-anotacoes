# bash

## **Renomear arquivos e diretórios, alterando as fontes de caixa alta para baixa**

```text
 for f in * ; do mv -v $f `echo $f | tr '[A-Z]' '[a-z]'`; done
```

## Visualizar tamanho de arquivos ocultos

```text
du -sch .[!.]* * |sort -h
```

## Texto colorido terminal

```text
#Normal
```

```text
txtblk='e[0;30m' # Preto
txtred='e[0;31m' # Vermelho
txtgrn='e[0;32m' # Verde
txtylw='e[0;33m' # Amarelo
txtblu='e[0;34m' # Azul
txtpur='e[0;35m' # Roxo
txtcyn='e[0;36m' # Cyan
txtwht='e[0;37m' # Branco

#Negrito
bldblk='e[1;30m' # Preto
bldred='e[1;31m' # Vermelho
bldgrn='e[1;32m' # Verde
bldylw='e[1;33m' # Amarelo
bldblu='e[1;34m' # Azul
bldpur='e[1;35m' # Roxo
bldcyn='e[1;36m' # Cyan
bldwht='e[1;37m' # Branco

#Underline
unkblk='e[4;30m' # Preto
undred='e[4;31m' # Vermelho
undgrn='e[4;32m' # Verde
undylw='e[4;33m' # Amarelo
undblu='e[4;34m' # Azul
undpur='e[4;35m' # Roxo
undcyn='e[4;36m' # Cyan
undwht='e[4;37m' # Branco

#Fundo
bakblk='e[40m'   # Preto
bakred='e[41m'   # Vermelho
bakgrn='e[42m'   # Verde
bakylw='e[43m'   # Amarelo
bakblu='e[44m'   # Azul
bakpur='e[45m'   # Roxo
bakcyn='e[46m'   # Cyan
bakwht='e[47m'   # Branco

#Limpar formatação
txtrst='e[0m'
```

**Como usar**

Inclua as variáveis no arquivo: ~/.bashrc

Essas variáveis são ativadas no login do usuário, para forçar a ativação delas execute o comando: source ~/.bashrc

```text
echo -e "${txtred} Um texto em Vermelho ${txtrst}"
```

