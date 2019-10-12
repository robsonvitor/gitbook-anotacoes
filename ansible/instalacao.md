# Instalação

## Instalação no Debian

Configurar repositório

```text
echo 'deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main' >> /etc/apt/sources.list.d/ubuntu_trusty.list
```

Instalar as chaves do repositório

```
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
```

Atualizar a lista de pacotes

```text
apt update
```

Instalar o Ansible

```bash
apt install ansible
```

$$
a = b * c
$$

## Instalação no Ubuntu 18.04

```text
sudo apt-add-repository ppa:ansible/ansible
```

```text
apt install ansible
```

