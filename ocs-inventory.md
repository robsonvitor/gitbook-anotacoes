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

