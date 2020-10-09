# Resolução de Problemas

### Erro ao inicializar o agente no CentOS:

```text
Can't open PID file /run/zabbix/zabbix_agentd.pid
```

### Solução:

```text
yum install policycoreutils-python 

semanage permissive -a zabbix_agent_t
```

