# Diversos

## Unificar arquivos PDF

```text
gs -dBATCH -dNOPAUSE -q -sDEVICE=pdfwrite -sOutputFile=Arquivo_Unificado.pdf Arquivo1.pdf Arquivo2.pdf
```

## Compressão de PDF

```text
ghostscript -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/printer -dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf
```

Other options for PDFSETTINGS:

* /screen selects low-resolution output similar to the Acrobat Distiller "Screen Optimized" setting.
* /ebook selects medium-resolution output similar to the Acrobat Distiller "eBook" setting.
* /printer selects output similar to the Acrobat Distiller "Print Optimized" setting.
* /prepress selects output similar to Acrobat Distiller "Prepress Optimized" setting.
* /default selects output intended to be useful across a wide variety of uses, possibly at the expense of a larger output file.

## Visualização de arquivos PDF no terminal

```text
pdftotext -layout Arquivo.pdf -layout - | more
```

## Remover emblemas de ícones de arquivos no gnome

gvfs-info -a metadata::emblems 20170601\_194149.jpg

gvfs-set-attribute -t unset 20161115\_091432.jpg metadata::emblems

find Arquivos/GoogleDrive/ -iname \*.pdf -exec gvfs-set-attribute -t unset {} metadata::emblems \;

/usr/share/nautilus-python/extensions/insync\_plugin.py

## Visualizar tamanho de diretórios e arquivos ocultos

```text
du -sch .[!.]* * | sort -h
```

## Configurar diretórios do usuário

### Via comando

```text
 xdg-user-dirs-update --set DESKTOP $HOME/NewDesktop
```

```text
vim ~/.config/user-dirs.dirs
```

### Exemplo:

```text
# This file is written by xdg-user-dirs-update
# If you want to change or add directories, just edit the line you're
# interested in. All local changes will be retained on the next run
# Format is XDG_xxx_DIR="$HOME/yyy", where yyy is a shell-escaped
# homedir-relative path, or XDG_xxx_DIR="/yyy", where /yyy is an
# absolute path. No other format is supported.
# 
XDG_DESKTOP_DIR="$HOME/Desktop"
XDG_DOWNLOAD_DIR="$HOME/Downloads"
XDG_TEMPLATES_DIR="$HOME/Modelos"
XDG_PUBLICSHARE_DIR="$HOME/Público"
XDG_DOCUMENTS_DIR="$HOME/Documentos"
XDG_MUSIC_DIR="$HOME/"
XDG_PICTURES_DIR="$HOME/Imagens"
XDG_VIDEOS_DIR="$HOME/Vídeos"
```

### Screenshot via SSH

```text
ssh usuario@host -X

export DISPLAY=:0

scrot nome_arquivo.png
```

### Remover página de arquivo PDF

```text
pdftk documento.pdf cat 2-4 11-end output novo_documento.pdf
```

