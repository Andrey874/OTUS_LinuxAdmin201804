Настроить все без выключения selinux ddns тоже должен работать без выключения selinux
---------------------
Для настройки SELinux используем пакет policycoreutils-python
Просмотрим настройки политик на доступ к файлам и каталогам для расположения конфигов и файлов зон
`semanage fcontext -l | grep '/etc/named'` 
Cоздадим сопоставляющий эквивалент для /etc/named как для /var/named, т.е. путь /var/named = /etc/named
`semanage fcontext -a -e /var/named /etc/named`
Рекурсивно применим новое правило контекста
`restorecon -R -v /etc/named`
После этого сможем обновить зону
Результат
![SE Результат](https://)
[change_ddnsclient_zone.sh](https://)
`#!/bin/bash
/usr/bin/nsupdate -k /etc/named/Kkislovodsk01.ddns.lab.+157+12223.private -v $1`