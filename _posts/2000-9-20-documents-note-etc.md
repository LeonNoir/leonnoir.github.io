---
layout: post
title: "etc"
tags: documents
---

# openssl s_client -connect target.doma.in:55555

## Что делает команда:
- openssl s_client: запускает инструмент OpenSSL, который работает как универсальный клиент для соединений, защищенных шифрованием.
- -connect: указывает адрес, к которому нужно подключиться.
- target.doma.in:55555: адрес сервера (target.doma.in) и номер порта (55555).

## Зачем это нужно::
- Проверка сертификата: Посмотреть, действителен ли SSL-сертификат сервера, кем он выдан и не истек ли его срок действия.
- Диагностика почты: Порт 64993 — это нестандартный порт (вероятно, измененный стандартный IMAP через SSL, который обычно использует 993). Команду используют, чтобы понять, отвечает ли почтовый сервер вообще.
- Отладка TLS: Узнать, какие версии протоколов (TLS 1.2, 1.3) и шифры поддерживает сервер.

## Какой будет результат:
Если соединение успешно, в консоли отобразится детальная информация о цепочке сертификатов и надпись CONNECTED(00000003). Если порт закрыт или заблокирован брандмауэром, вы увидите ошибку Connection refused или Operation timed out.


# docker
- docker ps    # список активных контейнеров
- docker exec -it КОНТЕЙНЕР bash  # войти внутрь запущенного контейнера
- docker compose logs -f          # для просмотра логов всех сервисов вашего приложения в реальном времени, можно обратиться к конкретному сервису
- docker logs [ TAB ] -f
- 
- docker stats  # мониторинг ресурсов, потребляемых запущенными контейнерами
- docker compose up -d   # up: Читает файл docker-compose.yml, на его основе скачивает необходимые образы (если их нет), создает и запускает все описанные в нем сервисы (контейнеры, сети и тома) ХОСТ:КОНТЕЙНЕР
                         # -d (detached): Запускает контейнеры в фоновом режиме.
                         # Если контейнеры уже существуют, поведение команды docker compose up зависит от того, меняли ли вы файл docker-compose.yml или используемые образы:
                         # Если конфигурация изменилась: Если вы отредактировали docker-compose.yml (например, изменили порты, переменные окружения или образ),
                         #   Docker автоматически остановит и пересоздаст только те контейнеры, которых коснулись изменения
                         # Данные в томах (Volumes): При пересоздании контейнеров данные, хранящиеся в именованных томах, сохраняются.
                         #   Удаляются только данные, которые находились внутри файловой системы самого контейнера и не были вынесены в volumes
  
- docker compose stop    # Только останавливает запущенные контейнеры сервисов, описанных в docker-compose.yml
- docker compose start   # Eсли нужно запустить ранее остановленные контейнеры без проверки изменений в проекте, иначе: docker compose up -d
- docker compose down    # Останавливает контейнеры и сразу удаляет их, а также удаляет внутренние сети, созданные для этого проекта
- docker system prune -f # предназначена для быстрой и автоматической очистки системы Docker от неиспользуемых ресурсов без необходимости подтверждать каждое действие (убедись, что все нужное запущенно)






# Windows копируем ВСЕ сторонние драйвера для дальнейшего переноса 
- dism /online /export-driver /destination:"C:\Drivers"  # Все сторонние драйверы будут скопированы в указанную папку, каждый в свою подпапку с .inf файлом.



# nmcli полезные команды
- nmcli device wifi list
- nmcli device wifi connect "YourSSID" password "YourPassword"  #
- nmcli device wifi connect "YourSSID" --ask                    # более секьюрно

- nmcli connection show
- nmcli connection delete "YourSSID"

- Подключение к сети:  nmcli device wifi connect "SSID" password "пароль"
- Обновить список сетей:  nmcli device wifi rescan
- Показать сетевые устройства:  nmcli device status
- 

# ETc

## что если нужно в hotspot попасть на страницу редиректа, а она автоматом не случилась после подключения к сети
http://fixwifi.it/ (универсальный ресурс для вызова страницы авторизации).
http://captive.apple.com (особенно эффективно для macOS).
http://neverssl.com (сайт без шифрования, который легко перехватывается

# смена раскладки linux (когда хочешь нажать Yes но можешь только Да)
sudo localectl set-keymap us

# удалить историю (только текущую)
history -c && history -w

# Репозитории
```no-line-numbers
DEB12
# Debian Main Repositories
deb http://deb.debian.org/debian/ bookworm main contrib non-free-firmware
# Debian Security Updates
deb http://security.debian.org/debian-security bookworm-security main contrib non-free-firmware
# Debian Updates
deb http://deb.debian.org/debian/ bookworm-updates main contrib non-free-firmware

DEB13
deb http://deb.debian.org/debian/ trixie main non-free-firmware
deb-src http://deb.debian.org/debian/ trixie main non-free-firmware
deb http://security.debian.org/debian-security trixie-security main non-free-firmware
deb-src http://security.debian.org/debian-security trixie-security main non-free-firmware
# trixie-updates, to get updates before a point release is made;
# see https://www.debian.org/doc/manuals/debian-reference/ch02.en.html#_updates_and_backports
deb http://deb.debian.org/debian/ trixie-updates main non-free-firmware
deb-src http://deb.debian.org/debian/ trixie-updates main non-free-firmware

DEB8
deb http://archive.debian.org/debian/ jessie main contrib non-free
```

# sudo
```no-line-numbers
apt install sudo
usermod -aG sudo имя_вашего_пользователя
```

# ssh
```no-line-numbers
apt install openssh-server
# по умолчанию root не может подключится но всегда проверяй
```

# Проверка неожиданных выключений при загрузке
```no-line-numbers
sudo journalctl -b -1 | grep -i "kernel panic\|segfault\|oom\|hard reset"
```

# Место на HDD (когда случайно скачал все сезоны мухтар в 8к и место заканчивается)

## 
```no-line-numbers
sudo du -xh / --max-depth=1 | sort -rh | head -n 10
```

* **du (disk usage):** Основной инструмент для оценки веса файлов и папок.
* **-x (one-file-system):** Критически важный флаг. Он говорит команде: «Считай только то, что лежит на этом конкретном разделе». Без него du полезет в /dev, /run и другие виртуальные папки, насчитав лишнего.
* **-h (human-readable):** Выводит размер в понятных Кб, Мб и Гб, а не в бездушных байтах.
* **/:** Указываем точку старта — корень системы.
* **--max-depth=1:** Говорит «не зарывайся слишком глубоко». Мы увидим общие веса папок верхнего уровня (/var, /home, /usr). Если Мухтар лежит в /home/user/downloads, мы увидим, что «потяжелела» папка /home.
* **| (pipe):** Конвейер. Передает результат работы du следующей команде.
* **sort -rh:** Сортировка.
    * **-r (reverse):** Сначала самое тяжелое (вверху).
    * **-h (human-numeric-sort):** Сортирует с учетом «человеческих» букв (чтобы 2 Гб были больше, чем 100 Мб).
* **head -n 10:** Оставляет только первые 10 строк, чтобы экран не завалило мусором.



---
```no-line-numbers
```
