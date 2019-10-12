# Nautilus

\#\# Nautilus scripts

[https://help.ubuntu.com/community/NautilusScriptsHowto](https://help.ubuntu.com/community/NautilusScriptsHowto)

[https://www.vivaolinux.com.br/artigos/impressora.php?codigo=2561](https://www.vivaolinux.com.br/artigos/impressora.php?codigo=2561)

$NAUTILUS\_SCRIPT\_SELECTED\_FILE\_PATHS - são listados os arquivos com caminhos absolutos e com quebra de linha entre eles. Essa é a melhor variável a ser usada, mas ela tem um problema, não funciona em arquivos que estejam na área de trabalho e só funciona em arquivos locais, ou seja, só funciona em rede smb:// se você montar a pasta da rede usando o mount e o smbfs.

$NAUTILUS\_SCRIPT\_SELECTED\_URIS - a função dessa variável é idêntica a anterior, com uma diferença, o caminho gerado é sempre no formato file://, smb://, ftp://, http:// etc..., ou seja, ele pode listar qualquer localização no computador, rede ou internet, mas tem um problema crítico, os acentos e espaços são convertidos em códigos, o que impede o seu uso em scripts. Mas porque mencioná-lo? Porque ele é a melhor opção para usar com programas que usem o gnome-vfs, como o gnome-open, Totem, Rhythmbox etc...

$NAUTILUS\_SCRIPT\_CURRENT\_URI - esta variável contém a pasta atual de execução, equivalente ao comando dirname. Como a primeira variável, essa aqui não funciona na área de trabalho.

$NAUTILUS\_SCRIPT\_WINDOW\_GEOMETRY - esta variável é de uso obscuro para mim, pois informa a posição e tamanho da janela do nautilus com o qual foi executado o script. A única função que poderia imaginar para ela seria a criação de um script com o xvidcap.

