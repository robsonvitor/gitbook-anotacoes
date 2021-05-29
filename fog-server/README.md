---
description: Servidor de imagens para sistemas operacionais
---

# FOG Server

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



