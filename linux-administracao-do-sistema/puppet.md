# Puppet

* **Instalação do puppet-agent**

```text
# Download do pacote
wget http://apt.puppetlabs.com/puppet-release-$(lsb_release -cs).deb

# Instalar o pacote
dpkg -i puppet-release-$(lsb_release -cs).deb

# Atualizar repositórios
apt update

#Instalar puppet-agent
apt install puppet-agent

# Adicionando diretório de binários do puppet ao PATH
echo 'export PATH="$PATH:/opt/puppetlabs/bin"' >> /etc/bash.bashrc
```

* **Instalação do puppetserver**

```text
# Instalar o pacote utilizando 
puppet resource package puppetserver ensure=present

# Ativar o serviço: 
puppet resource service puppetserver ensure=running enable=true

# Ajustar a quantidade de memória utilizada pelo puppetserver

# Memória alocada na inicialização da JVM - 512MB
sed -i '/^JAVA_ARGS/ s/Xms2g/Xms512m/g' /etc/default/puppetserver

# Memória máxima utilizada pela JVM - 1GB
sed -i '/^JAVA_ARGS/ s/Xmx2g/Xmx1g/g' /etc/default/puppetserver
```

* **Instalação do PostgreSQL**

```text
apt install postgresql

# Arquivo: /etc/postgresql/*/main/postgresql.conf (remover comentário em : listen_addresses = 'localhost')
sed -i '/^#listen_address/ s/^#//g' /etc/postgresql/*/main/postgresql.conf

# Arquivo: /etc/postgresql/*/main/pg_hba.conf (substituir peer por trust em: local all all peer)

# Reiniciar serviço: systemctl restart postgresql.service
su - postgres
createdb puppetdb
createuser -a -d -E -P puppetdb
```

* **Instalação e configuração do puppetdb**

```text
 puppet resource package puppetdb ensure=latest
```

```text
# Pacote para gerenciamento do puppetdb remotamente
puppet resource package puppetdb-termini ensure=latest
```

1. Ajuste as configurações:

```text
# Geração de certificados utilizados pelo puppetdb
puppetdb ssl-setup
```

```text
# /etc/puppetlabs/puppetdb/conf.d/database.ini

[database]
classname = org.postgresql.Driver
subprotocol = postgresql
subname = //localhost:5432/puppetdb
username = puppetdb
password = puppetdb
```

```text
# /etc/puppetlabs/puppetdb/conf.d/jetty.ini

[jetty]
host = 0.0.0.0
port = 8080
ssl-host = 0.0.0.0
ssl-port = 8081
```

```text
# /etc/puppetlabs/puppet/puppet.conf
[master]
storeconfigs = true
storeconfigs_backend = puppetdb
reports = puppetdb
report_store = /var/log/puppetlabs/puppet
```

```text
# Criar/Editar o arquivo /etc/puppetlabs/puppet/routes.yaml

master:
  facts:
   terminus: puppetdb
   cache: yaml
```

```text
# Criar arquivo de configuração do puppetdb: /etc/puppetlabs/puppet/puppetdb.conf

[main]
server_urls = https://puppetserver.pp:8081
```

```text
# Ajustar permissões
chown -R puppet:puppet `puppet config print confdir`

# Ativar o serviço
puppet resource service puppetdb ensure=running
```

```text
# Reiniciar serviço
systemctl restart puppetdb.service
```

