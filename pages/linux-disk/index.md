---
layout: page
title: работа с диском в linux
---

# Работа с диском

## ищем что забивает место в системе

увидеть топ-10 самых тяжелых папок в корне:

```no-line-numbers
sudo du -sh /* 2>/dev/null | sort -rh | head -n 10
```





---
