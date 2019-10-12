# VirtualBox

```text
# Importar VM
```

```text
$ vboxmanage import imagem.ova
```

```text
# Instalar Extension Pack

$ vboxmanage extpack install Oracle_VM_VirtualBox_Extension_Pack-4.3.26-98988.vbox-extpack
```

```text
# Subir VM desligada (ouvindo rdesktop na porta 3310)

$ vboxheadless -startvm "NomeVM" -e "TCP/Ports=3310
```

```text
# Status da VM

$ vboxmanage showvminfo "WinXP" | grep "State:" | sed s/\ //g | sed s/\(.*\)//g | cut -f2 -d:'
```

```text
# Reset na VM

$ vboxmanage controlvm "NomeVM" reset
```

```text
# Versão Instalada do VirtualBox 

$ vboxmanage --version
```

```text
# Redimensionar HD (VDI) para 30GB

$ vboxmanage modifyhd disco.vdi --resize 30000
```

```text
# Converter formato de disco antes de redimensionar

$ vboxmanage clonehd "disco.vmdk" "disco.vdi" --format vdi
```

