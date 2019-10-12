# PostgreSQL

Importar dump.sql

```text
psql -h host -U usuario -d banco < dump.sql
```

Exportando banco

```text
pg_dump -v -Fc -f /tmp/backup_db.dump banco
```

```text
pg_restore -vc -d banco_destino -Fc /tmp/banco_origem.dump
```

Alterar senha de usuário via psql

```text
ALTER USER usuario WITH ENCRYPTED PASSWORD 'senha_nova';
```

Criar cópia de uma base de dados no mesmo servidor:

```text
CREATE DATABASE banco_backup WITH TEMPLATE banco_origem;
```

