---
layout: page
title: мониторинг сети в linux
---

описание разных програм для мониторинга сети в линукс

# SS

```no-line-numbers
ss -tpln
```
(Флаги: t — TCP, u — UDP, l — только слушающие, n — цифрами вместо имен, p — показать процесс/PID)

```no-line-numbers
ss -tpln
tcp      LISTEN      0      100      0.0.0.0:25        0.0.0.0:*      users:(("master",pid=1745,fd=13))

ps -fp 1745
UID          PID    PPID  C STIME TTY          TIME CMD
root        1745       1  0 янв26 ?     00:01:08 /usr/lib/postfix/sbin/master -w
```
(ps -fp позволит увидеть какое приложение открыло порт)
127.0.0.1:порт — сервис доступен только внутри самой машины (безопасно).
0.0.0.0:порт или *:порт — сервис торчит «наружу» и доступен из интернета/локалки


## с помощью ss

**-t** только TCP, **-p** - показать процесс, **-l** - слушающие, **-n** номер порта

```no-line-numbers
ss -tpln
```

Для отображения всех успешных соединений по IPv4:

```no-line-numbers
ss -4 state established
```

## с помощью netstat

Перечислить все порты: 

```no-line-numbers
netstat -a
```

Перечислить все TCP порты: 

```no-line-numbers
netstat -at
```

Перечислить все UDP порты:

```no-line-numbers
netstat -au
```

Вывод непрерывно:

```no-line-numbers
netstat -c
```
