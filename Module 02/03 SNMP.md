
Подключаемся к серверу zabbix

Добавить репозитарий apt

```
nano /etc/apt/sources.list
```
```
deb http://deb.debian.org/debian/ bullseye main contrib non-free
deb-src http://deb.debian.org/debian/ bullseye main contrib non-free

deb http://security.debian.org/debian-security bullseye-security main contrib non-free
deb-src http://security.debian.org/debian-security bullseye-security main contrib non-free

deb http://deb.debian.org/debian/ bullseye-updates main contrib non-free
deb-src http://deb.debian.org/debian/ bullseye-updates main contrib non-free

```

Установка snmp консоли
```
# apt update
# apt install snmp snmp-mibs-downloader
# :> /etc/snmp/snmp.conf
```


Включение SNMP на Windows 

Добавить компонент Service SNMP и WMI for SNMP

Настроить службу SNMP

На вкладке безопасность добавить имя public

И выставить признак принимать запросы от люого узла

На вкладке Агент SNMP выставить чекбокс для всех служб


Добавить хост в Zabbix по SNMP
Добавить шаблон Generic by SNMP 
Проверить в LAtest data собранные данные по SNMP

В место route напишите ip mikrotik

Перебор всех значений OID устройства
```
server# snmpwalk -On -c public -v2c router 1
```
Определение имени устройства
```
server# snmpget -c public -v2c router .1.3.6.1.2.1.1.5.0

server# snmpget -c public -v2c router SNMPv2-SMI::mib-2.1.5.0

server# snmpget -c public -v2c router SNMPv2-MIB::sysName.0

server# snmpget -c public -v2c router sysName.0

server# snmpwalk -c public -v2c router sysName
```
Определение uptime устройства
```
server# snmpget -c public -v2c router sysUpTime.0

```
Получение mac address table
```
radio$ snmpwalk -On -v2c -c public@101 switch 1.3.6.1.2.1.17.4.3.1.2
```
Определение загрузки CPU устройства
```
server# snmpget -c public -v2c router .1.3.6.1.4.1.9.2.1.56.0
```
Вывод списка интерфейсов устройства
```
server# snmpwalk -c public -v2c -On router ifDescr
```

Вывод количества байт, прошедших через порт устройства с момента его включения
```
FastEthernet0/0

server# snmpget -c public -v2c -On router ifInOctets.1
server# snmpget -c public -v2c -On router ifHCInOctets.1

Port-channel1

server# snmpget -c public -v2c -On router ifOutOctets.5
server# snmpget -c public -v2c -On router ifHCOutOctets.5
```
Информация по протоколу CDP
```
server# snmpwalk -c public -v2c router .1.3.6.1.4.1.9.9.23.1.2.1.1
```
