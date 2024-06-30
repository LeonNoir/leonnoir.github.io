---
layout: post
title: "Linux"
tags: documents
---
## работа с screen

запустить с node в скрине c именем **appNode**, приложение **app123.js**  (удобно для скриптов автозапуска)

```no-line-numbers
screen -dmS appNode node path-to-folder/app123.js
```

отправить в скрин **appNode** команду от имени пользователя **SomeUser** (в примере случай, когда нужно было в консоль работающей программы отправить команду: **stop** и нажать enter: **\015**

```no-line-numbers
sudo -u SomeUser screen -p 0 -S appNode -X eval 'stuff "stop"\015'
```

посмотреть какие скрины есть:

```no-line-numbers
screen -ls
```

подключиться к скрину c именем **appNode**:

```no-line-numbers
screen -r appNode
```

выйти из скрина, не уничтожая его

```no-line-numbers
ctrl+A, ctrl+D
```

## настройка сети

**по настройке сети [более подробно](/pages/linuxcfg/)**