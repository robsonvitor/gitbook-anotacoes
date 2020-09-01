# find

\#Encontrar arquivos com menos de 7 dias

find . -iname "\*.gz" -type f -ctime -7 \|sort

\# Encontrar arquivos com mais de 7 dias

find . -iname "\*.gz" -type f -ctime +7 \|sort

\# Encontrar arquivos e mover eles para outro diretório

find . -iname "\*.gz" -type f -ctime +7 -exec mv -t ../../../OLD\_Backup/ {} +

\# Encontrar todos os arquivos que não possuem dono em nosso sistema.

find . -nouser

\# Encontrar todos arquivos que são do usuário

find . -user USUARIO

\# Encontrar arquivos vazios

find . -type f -empty

\# Encontrar diretórios vazios

find . -type d -empty

\# Limitar a quantidade de subdiretórios que o find irá buscar, neste caso, até 2 níveis

find . -maxdepth 2 -iname "expressaoDeBusca"

\# Encontrar todos arquivos no diretório, exceto os .jar

find . -maxdepth 1 ! -name \*.jar

#### Renomear arquivos substituindo ou removendo uma string do nome

```text
find ./ -type f -iname "String*" -exec rename 's/String//g' {} \;
```

## Expressões regulares

find /diretorio -regextype posix-egrep -iregex '.\*.\(mp3\|wma\)'



