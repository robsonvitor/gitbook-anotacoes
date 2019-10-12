# MySQL

\# ​Remoção de caracteres de registros

update tabela SET numeroCel = replace\(numeroCel ,"-",""\)

\# ​Atualização em campos que estiverem como NULL

update tabela SET campo = "Nenhum" WHERE campo is NULL

\# Deletar todos registros de uma tabela

DELETE FROM tabela

\# Deletar e recriar a tabela

TRUNCATE TABLE tabela

\# Atualizar registros

UPDATE tbl\_usuarios SET nomeCompleto = "Nome do Usuario" WHERE usuario = "usuario123"

\# Exibir registros onde o "campo\_data" for mais antigo do que 30 dias

SELECT \* FROM tabela WHERE campo\_data &lt; DATE\_SUB\(NOW\(\), INTERVAL 30 DAY\);

\# Contar quantidade de registros

SELECT COUNT\(\*\) FROM tabela

-- Conceder permissão no Banco ou Tabela

-- Procedure

\# Criar Trigger

DELIMITER \|

```text
CREATE TRIGGER logCriarUsuario

    AFTER INSERT ON tbl\_usuarios

    FOR EACH ROW BEGIN

        INSERT INTO tbl\_logCriarUsuario SET usuario = NEW.usuario;

    END;
```

\|

DELIMITER ;

\# Apagar Trigger

DROP TRIGGER logCriarUsuario;

## Acesso remoto MySQL

Edite o arquivo **my.cnf**, em Linux e BSD geralmente fica em **/etc/my.cnf** ou **/etc/mysql/my.cnf**

Procure no conteúdo do arquivo de configuração **my.cnf** a opção **bind-address**

```text
bind-address  = 127.0.0.1
```

Altere a linha de configuração para:

```text
bind-address  = 0.0.0.0
```

Caso exista no arquivo de configuração, comente a linha que contenha:

```text
# --skip-networking
```

Acesse o prompt MySQL e conceda permissão de acesso na base de dados:

```text
mysql> GRANT ALL ON banco.* TO usuario@'IP_REMOTO' IDENTIFIED BY 'senha';
```

```text
Caso queira liberar o acesso para qualquer endereço IP, altere onde está 
IP_REMOTO para %
```

Execute o comando a seguir para forçar o reconhecimentos das permissões pelo servidor MySQL

```text
mysql> FLUSH PRIVILEGES;
```

