# Windows

## Compartilhamento de diretórios via prompt MS-DOS

```text
net share Nome_Compartilhamento=Caminho_Diretorio_Local
```

**Exemplo de uso do comando**

Compartilhar o diretório **Arquivos** em **C:**

```text
net share Arquivos="C:Arquivos"
```

## Configurações de rede Windows pelo Prompt MS-DOS

Capturando endereços MAC ADDRESS

```text
C:> getmac /V
```

Endereço IP fixo

```text
C:> netsh interface ip set address name="Conexão Local" static 192.168.1.10 255.255.255.0 192.168.1.1 1
```

Endereço IP via DHCP

```text
C:> netsh interface ip set address "Conexão Local" dhcp
```

DNS via DHCP

```text
C:> netsh interface ip set dns "Conexão Local" dhcp
```

Acrescentando endereços DNS

```text
C:> netsh interface ip add dns "Conexão Local" 8.8.8.8 INDEX=1
```

Deletando um endereço DNS

```text
C:> netsh interface ip delete dns "Conexão Local" 8.8.8.8
```

## Alterar o tipo de conexão no Windows 10 \(Pública, Privada\)

[https://www.isunshare.com/windows-10/change-network-from-public-to-private-in-windows-10.html](https://www.isunshare.com/windows-10/change-network-from-public-to-private-in-windows-10.html)

