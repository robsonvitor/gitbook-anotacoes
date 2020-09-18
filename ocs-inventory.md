# OCS Inventory

### Consultas úteis

#### Dispositivos vistos há mais de trinta dias

```text
select NAME,LASTCOME from hardware where DATE(lastcome) < (CURDATE() - interval 30 DAY)
```

#### Computadores sem um determinado software instalado

```text
select hardware_id from softwares where softwares.PUBLISHER like "%bitdefender%"
```

#### Softwares instalados em um determinado computador

```text
select hard.name,soft.name,soft.publisher,soft.version from softwares as soft inner join hardware as hard on soft.hardware_id = hard.id where hard.name like "NOME-PC%" order by soft.publisher;
```



