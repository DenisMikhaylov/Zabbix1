

Cписок того, что надо забэкапить будет таким:

Базу данных в которой zabbix хранит настройки и данные.
Директорию /etc/zabbix с настройками zabbix агента и сервера.
Директорию /usr/share/zabbix с файлами веб-интерфейса и скриптами.
Выборочно или целиком директорию /etc/httpd с настройками apache агента и сервера.
Директорию /etc/letsencrypt c ssl сертификатом.
Экспорт шаблонов и хостов


Скрипт, без учета версионности и без копирования на какой-либо третий сервер.

```
Nano backup.sh
```
```
#!/bin/bash
 
ROPT="-v -az --delete"
 
#RSYNC
rsync $ROPT /etc/zabbix/ /backup/zabbix_server/etc_zabbix
rsync $ROPT /usr/share/zabbix/ /backup/zabbix_server/usr_share_zabbix
rsync $ROPT /etc/httpd/ /backup/zabbix_server/etc_httpd
rsync $ROPT /etc/letsencrypt/ /backup/zabbix_server/etc_letsencrypt
 
#STOP ZABBIX
systemctl stop zabbix-server
sleep 3
 
#MYSQLDUMP
mysqldump -u USERNAME -pPASSWORD zabbix_db > /backup/zabbix_server/zabbix_db.sql
 
#START ZABBIX
systemctl start zabbix-server
 
#TAR 
tar -czvf /backup/zabbix_server.tar.gz -C /backup/ zabbix_server
```
