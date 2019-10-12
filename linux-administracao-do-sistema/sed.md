# sed

Remoção de linhas em branco de um arquivo

```text
sed '/^$/d' arquivo.txt
```

Substituir string em arquivo

```text
sed -i "s/stringProcurada/stringNova/g" arquivo.txt
```

Substituir conteúdo entre aspas simples

```text
sed -i "/BASH_IT_THEME/s/'.*'/'purity'/" .bashrc
```

Remover quebras de linha

```text
sed ':a;N;$!ba;s/\n/ /g' arquivo.txt
```

[http://terminalroot.com.br/2015/07/30-exemplos-do-comando-sed-com-regex.html](http://terminalroot.com.br/2015/07/30-exemplos-do-comando-sed-com-regex.html)

