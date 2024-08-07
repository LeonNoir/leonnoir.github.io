---
layout: page
title: Шпаргалка по PsExec
---

## Примеры

---
<br />
#**Запуск ps скрипта лежащего на шаре:**

```no-line-numbers
psexec -s \\pc-name-01 Powershell -ExecutionPolicy Bypass -File \\192.168.1.1\$scr\uptime.ps1
```

**-s**
Удаленный процесс запускается из системной учетной записи.

**-ExecutionPolicy Bypass**
нужно, что бы забайпассить политику запрещающую запуск скриптов

<br />
#**Отправка компа в ребут, когда иначе не хватает прав:**

```no-line-numbers
psexec \\pc-name-01 -s -d cmd.exe /c shutdown -r -t 0
```
**-s**
Удаленный процесс запускается из системной учетной записи.

**-d**
Указывает, что не нужно ждать завершения приложения. Этот параметр следует использовать только при запуске неинтерактивных приложений.

**cmd.exe /c SomeCommand**
Выполняет **SomeCommand** и затем выходит из обработчика команд



## Теория использования: 
---
```no-line-numbers
psexec [\\компьютер[,компьютер2[,...] | @файл][-u пользователь [-p пароль]][-n s][-l][-s|-e][-x][-i [сеанс]][-c [-f|-v]][-w каталог][-d][-<приоритет>][-a n,n,... ] программа [аргументы]
```

**компьютер**
Указывает программе PsExec, что нужно запустить приложение на заданном компьютере или компьютерах. Если имя компьютера не указано, то программа PsExec запустит приложение в локальной системе, если же вместо имени компьютера задан символ «звездочка» (\\*), то программа PsExec запустит приложение на всех компьютерах текущего домена.

**@файл**
Указывает программе PsExec, что нужно запустить приложение на всех компьютерах, перечисленных в заданном текстовом файле.

**-a**
Процессоры, на которых можно запустить приложение, отделяются запятыми, при этом процессоры нумеруются, начиная с 1. Например, чтобы запустить приложение на процессорах втором и четвертом, введите «-a 2,4»

**-c**
Указанная программа копируется в удаленную систему для выполнения. Если этот параметр не задан, то приложение должно находиться в системной папке удаленной системы.

**-d**
Указывает, что не нужно ждать завершения приложения. Этот параметр следует использовать только при запуске неинтерактивных приложений.

**-e**
Указанный профиль учетной записи не загружается.

**-f**
Указанная программа копируется в удаленную систему, даже если такой файл в удаленной системе уже есть.

**-i**
Запускаемая программа получает доступ к рабочему столу указанного сеанса в удаленной системе. Если сеанс не задан, то процесс выполняется в консольном сеансе.

**-l**
При запуске процесса пользователю предоставляются ограниченные права (права группы администраторов отменяются, и пользователю предоставляются только права, назначенные группе «пользователи»). В ОС Windows Vista процесс запускается с низким уровнем благонадежности.

**-n**
Позволяет задать задержку подключения к удаленным компьютерам (в секундах).

**-p**
Позволяет указать необязательный пароль для имени пользователя. Если этот параметр опущен, то будет выдан запрос на ввод пароля, при этом пароль не будет отображаться на экране.

**-s**
Удаленный процесс запускается из системной учетной записи.

**-u**
Позволяет указать необязательное имя пользователя для входа в удаленную систему.

**-v**
Указанный файл копируется в удаленную систему вместо уже имеющегося только при условии, что номер его версии выше или он более новый.

**-w**
Позволяет указать для процесса рабочий каталог (путь внутри удаленной системы).

**-x**
Отображает интерфейс пользователя на рабочем столе Winlogon (только в локальной системе).

**-приоритет (приоритет)**
Позволяет задавать для процесса различные приоритеты: -low (низкий), -belownormal (ниже среднего), -abovenormal (выше среднего), -high (высокий) или -realtime (реального времени).

**программа**
Имя запускаемой программы.

**аргументы**
Передаваемые аргументы (обратите внимание, что пути файлов должны указываться как локальные пути в целевой системе).

Чтобы задать имя приложения, которое содержит пробелы, используйте кавычки, например psexec \\marklap "c:\длинное имя\app.exe". Введенные данные передаются в удаленную систему при нажатии клавиши «Ввод», для завершения удаленного процесса нужно нажать сочетание клавиш Ctrl-C.
Если имя пользователя не задано, то удаленный процесс запускается из той же учетной записи, что и программа PsExec. Однако поскольку удаленный процесс является олицетворением, то он не будет иметь доступа к сетевым ресурсам удаленной системы. Если имя пользователя задано, то удаленный процесс запускается из указанной учетной записи и получает доступ к тем же сетевым ресурсам удаленной системы, что и данная учетная запись. Учтите, что пароль передается в удаленную систему в виде открытого текста.
При обращении к локальной системе эту версию программы PsExec можно использовать вместо программы Runas, поскольку для программы PsExec не требуются права администратора.

## Пример
Эта команда вызывает интерактивный интерфейс командной строки в системе \\marklap:
**psexec \\marklap cmd**

Эта команда запускает в удаленной системе программу IpConfig с параметром /all и выводит полученные данные на экран локальной системы:
**psexec \\marklap ipconfig /all**

Эта команда копирует программу test.exe в удаленную систему и выполняет ее в интерактивном режиме.
**psexec \\marklap -c test.exe**

Если в удаленной системе такая программа уже установлена и находится не в системном каталоге, укажите полный путь к этой программе
**psexec \\marklap c:\bin\test.exe**

Эта команда запускает в интерактивном режиме из системной учетной записи программу Regedit для просмотра данных разделов реестра SAM и SECURITY:
**psexec -i -d -s c:\windows\regedit.exe**

Эта команда используется для вызова программы Internet Explorer от имени пользователя с ограниченными правами:
**psexec -l -d "c:\program files\internet explorer\iexplore.exe"**