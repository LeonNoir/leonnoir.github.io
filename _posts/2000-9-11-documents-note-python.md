---
layout: post
title: "Note Python"
tags: documents
---

## Compile .py With Nuitka 
- Скачай Python 3.9.9 https://www.python.org/ftp/python/3.9.9/python-3.9.9-amd64.exe
- python -m pip install -U nuitka
- nuitka --version
- py -m nuitka --mingw64 .\main.py --standalone --onefile