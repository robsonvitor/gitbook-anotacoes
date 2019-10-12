# Recompilar Kernel Debian \(Modo fácil\)

Habilitar backports no sources.list

```text
deb http://http.debian.net/debian stretch-backports main contrib
```

Instalar pacotes necessários para compilação

```text
apt install kernel-package libncurses5-dev fakeroot wget bzip2 build-essential libelf-dev libssl-dev flex bison
```

Criar diretório para compilação

```text
mkdir -p ~/kernel
```

Entrar no diretório

```text
cd ~/kernel
```

Download dos fontes

```text
wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.1.4.tar.xz
```

Descompactar os fontes

```text
tar -xvf linux-5.1.4.tar.xz
```

Criar link simbólico

```text
ln -s linux-5.1.4 linux
```

Entrar no diretório dos fontes

```text
cd linux
```

Copiar configuração atual do kernel

```text
cp /boot/config-$(uname -r) .config
```

Visualizar/Editar configurações

```text
make menuconfig
```

Limpar o ambiente de compilações anteriores

```text
make-kpkg clean
```

Compilar o kernel

```text
fakeroot make-kpkg --initrd --append-to-version=-minhacompilacao kernel_image kernel_headers
```

Compilar módulos

```text
make modules
```

Instalar módulos

```text
make modules_install
```

Se não acontecer erros, prossiga, caso contrário retome no começo

Sair do diretório de fontes

```text
cd ..
```

Visualizar se foram gerados os pacotes .deb

```text
 ls -l *.deb
```

```text
-rw-r--r-- 1 root root 9810532 mai 23 13:12 linux-headers-5.1.4-minhacompilacao_5.1.4-minhacompilacao-10.00.Custom_amd64.deb
-rw-r--r-- 1 root root 44726068 mai 23 13:10 linux-image-5.1.4-minhacompilacao_5.1.4-minhacompilacao-10.00.Custom_amd64.deb
```

Caso os arquivos foram gerados corretamente, instale-os:

```text
dpkg linux*.deb
```

Após instalados os pacotes .deb, reinicie o Sistema Operacional e veja se está com a versão compilada

```text
uname -a
```

