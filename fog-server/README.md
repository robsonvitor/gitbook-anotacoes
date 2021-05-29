---
description: Servidor de imagens para sistemas operacionais
---

# FOG Server

## Instalação

## Configuração

### pfSense - Caso o servidor DHCP esteja nele

**Menu:** _Services / DHCP Server / Other Options / Network Booting / Show Advanced_

_Enables network booting: **check**_  
_Next server: **Endereço IP do FOG Server**_  
_Default BIOS file name: **undionly.kpxe**_  
_UEFI 32 bit file name: **ipxe32.efi**_  
_UEFI 64 bit file name: **ipxe.efi**_



## API

* **fog-user-token** located in user panel --&gt; API settings --&gt; user API token
* **fog-api-token** located in FOG configuration --&gt; FOG settings --&gt; API system Remember to check in both cases the checkbox: API enabled

## Correção de problemas

#### Erro

> could not verify mount point check if .mntcheck exists

#### Solução

> touch /images/.mntcheck /images/dev/.mntcheck
>
> chown -R fogproject:root /images



