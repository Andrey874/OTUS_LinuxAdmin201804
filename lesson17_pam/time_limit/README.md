### Запретить всем пользователям, кроме группы admin логин в выходные и праздничные дни

##### Для лимитирования доступа по времени и дням нидели

/etc/pam.d/login|sshd

`account    requisite    pam_time.so`

/etc/security/time.conf
```
# сервису login или sshd через все терминалы для всех пользователей исключая admin001
# разрешить доступ исключая SaterdaySunday с 00:00-24:00 (admin001 разрешено логиниться в любое время)
login|sshd;*;!admin001;!SaSu0000-2400
```
##### Для проверки по условию

/etc/pam.d/login|sshd

`auth       required     pam_succeed_if.so debug user ingroup admin`
