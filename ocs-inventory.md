# OCS Inventory

### Consultas úteis

#### Dispositivos vistos há mais de trinta dias

```text
SELECT name,lastcome FROM hardware WHERE DATE(lastcome) < (CURDATE() - interval 30 DAY);
```

#### Informações sobre softwares instalados

```text
SELECT * FROM softwares WHERE name LIKE "%vnc%" GROUP BY name; 
```

#### Computadores sem um determinado software instalado

```text
SELECT h.name,DATE_FORMAT(h.lastcome,'%d/%m/%Y %H:%m') FROM hardware as h WHERE h.id NOT IN (SELECT hardware_id FROM softwares as s WHERE s.PUBLISHER like "nome-software%") GROUP BY h.uuid ORDER BY h.name;
```

#### Softwares instalados em um determinado computador

```text
SELECT hard.name,soft.name,soft.publisher,soft.version FROM softwares as soft INNER JOIN hardware as hard on soft.hardware_id = hard.id WHERE hard.name LIKE "NOME-PC%" ORDER BY soft.publisher;
```



