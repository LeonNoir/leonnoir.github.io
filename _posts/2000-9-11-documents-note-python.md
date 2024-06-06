---
layout: post
title: "Python"
tags: documents
---

## Компилируем .py с помощью Nuitka 
- Скачай [Python 3.9.9](https://www.python.org/ftp/python/3.9.9/python-3.9.9-amd64.exe)
- python -m pip install -U nuitka
- python -m pip install ВСЕ НЕОБХОДИМЫЕ БИБЛИОТЕКИ

## Команда для компиляции
- <div>python -m nuitka --mingw64 .\main.py --standalone --onefile</div>

## Команда для компиляции (скрытый запуск)

```no-line-numbers
python -m nuitka --mingw64 --windows-disable-console .\main.py
python -m nuitka --mingw64 --windows-disable-console --standalone --onefile .\main.py
```
- обязательно в PowerShell


## X X X

## X X X

## X X X