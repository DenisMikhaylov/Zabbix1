
Подключаемся к серверу zabbix

Установка snmp консоли
```
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
Добавить шаблон General template snmp 
Проверить в LAtest data собранные данные по SNMP
