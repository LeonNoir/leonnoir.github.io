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
