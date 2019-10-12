# Samba 4

Informações gerais:

IP do servidor: 192.168.30.1

* Configurar hostname

```text
hostnamectl set-hostname srv-samba
```

* Instalar pacotes

```text
apt install samba smbclient winbind krb5-user dnsutils
```

* Encerrar processos

```text
ps ax | egrep "samba|smbd|nmbd|winbindd" | awk '{ print $1 }' | xargs kill -9
```

* Entrada em /etc/hosts

```text
192.168.30.1        srv-samba.lan    srv-samba
```

* Excluir cache

```text
find /var/{run,lib,cache}/samba -regextype posix-egrep -iregex '.*.(ldb|tdb)' -delete

smbd -b | egrep "LOCKDIR|STATEDIR|CACHEDIR|PRIVATE_DIR" | cut -d: -f2 | while read pasta; do find $pasta -iname *.tdb; done
```

* Remover arquivos de configuração do kerberos

```text
rm /etc/krb5.conf
```

* Configurar opções do disco usado para compartilhamento de dados do samba no /etc/fstab

```text
UUID=9112d516-7bb3-48b4-a4f9-68a415e6a2db /samba ext4 user_xattr,acl,barrier=1        1    1
```

* Provisionar o domínio

```text
samba-tool domain provision --use-rfc2307 --use-xattrs=yes --interactive
```

* Acrescentar diretivas na seção \[global\]  do /etc/samba/smb.conf

```text
vfs objects = acl_xattr
map acl inherit = Yes
store dos attributes = Yes
```

* Editar aquivo de configuração do kerberos /var/lib/samba/private/krb5.conf e acrescentar a seção \[realms\]

```text
[realms]
   DOMINIO.LAN = {
      kdc = srv-samba.lan
      admin_server = srv-samba.lan
   }
```

* Criar link de /var/lib/samba/private/krb5.conf para /etc/krb5.conf

```text
ln -s /var/lib/samba/private/krb5.conf /etc/krb5.conf
```

* Ajustes de serviços no systemd

```text
systemctl stop smbd nmbd winbind

systemctl disable smbd nmbd winbind

systemctl unmask samba-ad-dc

systemctl enable samba-ad-dc
```

* Listar compartilhamentos

```text
smbclient -L localhost -U%
```

* Conectar como usuário administrator

```text
smbclient //localhost/netlogon -UAdministrator%'senha'
```

* Verificar registros do DNS

```text
host -t SRV _ldap._tcp.dominio.lan.

host -t SRV _kerberos._udp.dominio.lan.

host -t A samba.dominio.lan.
```

* Verificar autenticação Kerberos

```text
kinit administrator

klist
```

## samba-tool - Administração via linha de comando

> Usuário fictício: joao.silva

```text
# Resetar senha de um usuario e forçar a troca de senha no próximo logon
samba-tool user setpassword joao.silva --newpassword=Criar_Nova_Senha --must-change-at-next-login

# Deletar usuário
samba-tool user delete joao.silva

# Listar usuários
samba-tool user list

# Desabilitar usuário
samba-tool user disable joao.silva

# Habilitar usuário
samba-tool user enable joao.silva

# Expirar a senha
samba-tool user setexpiry joao.silva --days=10

# Desativar expiração de senha
samba-tool user setexpiry joao.silva --noexpiry

# Visualizar políticas de senhas
samba-tool domain passwordsettings show

# Desabilitar complexidade de senha
samba-tool domain passwordsettings set --complexity=off

# Desabilitar o histórico de senhas
samba-tool domain passwordsettings set --history-length=0

# Desabilitar idade mínima de senha
samba-tool domain passwordsettings set --min-pwd-age=0

# Desabilitar idade máxima da senha
samba-tool domain passwordsettings set --max-pwd-age=0

# Desabilitar tamanho mínimo da senha
samba-tool domain passwordsettings set --min-pwd-length=0

samba-tool group list
samba-tool user list
samba-tool gpo listall
samba-tool group listmembers "Domain Users"
samba-tool group listmembers "Domain Admins"
samba-tool group listmembers Administrators
samba-tool group listmembers <GrupoAD>
samba-tool group removemembers <GrupoAD> <UsuarioAD>
samba-tool user disable <UsuarioAD>
samba-tool user delete <UsuarioAD>
samba-tool user setpassword <UsuarioAD>

# Definir a complexidade das senhas de usuários:
samba-tool domain passwordsettings set --complexity=off

# Desabilitar o histórico de senha:
samba-tool domain passwordsettings set --history-length=0

# Desabilitar idade mínima de senha:
samba-tool domain passwordsettings set --min-pwd-age=0

# Desabilitar idade máxima da senha:
samba-tool domain passwordsettings set --max-pwd-age=0

# Definir o tamanho máximo da senha em caracters:
samba-tool domain passwordsettings set --min-pwd-length=4

# Desabilitar expiração de senha de administrador:
samba-tool user setexpiry Administrator --noexpiry 

# Permitir o gerenciamento remoto das pastas compartilhadas. Informe a senha quando solicitado.
net rpc rights grant '<DominioLocal>\Domain Admins' SeDiskOperatorPrivilege -U'<DominioLocal>\Administrator'
A seguinte mensagem deverá aparecer:
Successfully granted rights.

# Liste as contas do domínio. Informe a senha e uma série de contas deverão ser mostradas.
net rpc rights list accounts -U'<DominioLocal>\Administrator'

# Para o GPO funcionar corretamente, deve-se dar permissões completas em sysvol e netlogon.
chmod 777 -R /usr/local/samba/var/locks/sysvol/<DominioLocal>/scripts
chmod 777 -R /usr/local/samba/var/locks/sysvol

```



| Option | Explanation |
| :--- | :--- |
| `--must-change-at-next-login` | Force password to be changed on next login. |
| `--use-username-as-cn` | Force use of username as user's CN. |
| `--smartcard-required` | Require a smartcard for interactive logons. |
| `--job-title` | User's job title. |
| `--department` | User's department. |
| `--company` | User's company. |
| `--description` | User's description. |
| `--mail-address` | User's email address. |
| `--internet-address` | User's home page. |
| `--telephone-number` | User's phone number. |
| `--physical-delivery-office` | User's office location. |

{% embed url="https://www.mundotibrasil.com.br/gerenciando-usuarios-e-grupos-pelo-shell-no-samba4/" %}

[http://www.comdesk.com.br/blog/item/8-active-directory-com-samba-4-parte-2](http://www.comdesk.com.br/blog/item/8-active-directory-com-samba-4-parte-2)

{% embed url="https://www.mundotibrasil.com.br/gerenciando-usuarios-e-grupos-pelo-shell-no-samba4/" %}

{% embed url="https://wiki.samba.org/index.php/User\_and\_Group\_management" %}

[https://wiki.samba.org/index.php/Adding\_users\_with\_samba\_tool](https://wiki.samba.org/index.php/Adding_users_with_samba_tool)

