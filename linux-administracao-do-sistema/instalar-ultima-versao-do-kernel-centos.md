# Instalar última versão do Kernel CentOS

Atualizar repositórios e realizar upgrade de todos os pacotes

```text
yum makecache && yum update -y
```

```text
yum -y install yum-plugin-fastestmirror
```

Visualizar a versão do CentOS

```text
cat /etc/os-release | grep -E '^ID=|^VERSION_ID'
```

Adicionar o repositório

```text
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm
```

Importar a chave GPG do repositório

```text
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
```

Instalar a última versão do Kernel que está no repositório

```text
yum --enablerepo=elrepo-kernel install kernel-ml
```

Colocar o Grub para inicializar pelo novo Kernel

```text
grub2-set-default 0
```

Gerar novo arquivo de configuração do Grub

```text
grub2-mkconfig -o /boot/grub2/grub.cfg
```

Após realizar todos os procedimentos, reinicie o Sistema Operacional e verifique qual a versão do Kernel

```text
uname -r
```

