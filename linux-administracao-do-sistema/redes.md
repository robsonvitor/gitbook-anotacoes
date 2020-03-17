# Rede

### Configurar conexão sem fio com wpa\_supplicant

**Gerar configuração**

```text
wpa_passphrase SSID senha > wpa_SSID.conf
```

**Conectar**

```text
wpa_supplicant -i INTERFACE_WIFI -D wext -c wpa_SSID.conf 
```

Após conectado, executar o cliente DHCP ou IP fixo

\*\*\*\*

### Configurar endereço e rota em interface de rede

**Ativar Interface de Rede**

```text
 ip link set interface up
```

**Endereço IP**

```text
 ip addr add IP_address/subnet_mask broadcast broadcast_address dev interface
```

**Gateway**

```text
 ip route add default via default_gateway
```

**DNS**

```text
 echo "nameserver 8.8.8.8" >> /etc/resolv.conf
```

### Monitoramento \(utilização da rede\) de tráfego em uma interface

```text
nethogs INTERFACE
```

### Endereço IP público da conexão atual com a internet

```text
curl ifconfig.me
```

```text
dig +short myip.opendns.com @resolver1.opendns.com
```

## Configuração de VLAN

**Habilitar o módulo para trabalhar com VLAN**

```text
modprobe 8021q
```

**Criar o dispositivo virtual**

```text
ip link add link eth0 name eth0.100 type vlan id 100
```

**Ativar a interface virtual. Caso a interface física esteja desativada é necessária ativá-la primeiro**

```text
ip link set dev eth0.100 up
```

**Configurar um ip estático para a interface virtual**

```text
ip addr add 192.168.100.1/24 brd 192.168.100.255 dev eth0.100
```

**Desativar a interface virtual**

```text
ip link set dev eth0.100 down
```

**Deletar a interface**

```text
ip link delete eth0.100
```

**Caso esteja realizando a instalação do Debian e precise forçar a buscar o ip via DHCP, o comando abaixo resolve.**

```text
udhcpc -i eth0.100
```

## [https://wiki.archlinux.org/index.php/VLAN](https://wiki.archlinux.org/index.php/VLAN)

## Simulando serviços com netcat

Ouvindo na porta 29

```text
netcat -l -p 29
```

Para testar

```text
telnet localhost 29
```

## Desligar/Reiniciar windows via shell Linux

**Reiniciar**

```text
$ net rpc shutdown -r -C 'Reiniciando...' -f -I NomeOuIpDoHost -t 10 -U Usuario%Senha
```

**Desligar**

```text
$ net rpc shutdown -C 'Desligando...' -f -I NomeOuIpDoHost -t 10 -U Usuario%Senha
```

**Parâmetros:**

* -C : Mensagem que será exibida para o usuário
* -f : forçar a execução
* -I : Nome do computador ou endereço IP
* -t : Tempo que irá aguardar para reiniciar/desligar
* -U : Usuário com permissões para executar a ação no host remoto
* -r : Reiniciar o host remoto

## Túnel via SSH

```text
IP Local: 127.0.0.1
```

```text
Porta Local: 55555
IP Remoto: 192.168.18.6
Porta Remota: 8080
Usuário Remoto: user
```

```text
$ ssh -f -L 127.0.0.1:55555:192.168.18.6:8080 user@192.168.18.6 -N
```

Explicando os parâmetros do ssh:

1. **-f :**  Redireciona as saídas para background
2. **-L :** Redireciona o tráfego local para o remoto
3. **-N :** Não executar comando no host remoto

