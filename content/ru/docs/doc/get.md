---
title: Получение инструмента
weight: 1
---

Получить копию инструмента можно следующими способами:
- ручная сборка из исходного кода
- получение последней стабильной версии из раздела Releases на GitHub
- получение сборки от последнего коммита из артефактов GitHub Actions


## Ручная сборка из исходников
1. Получение исходного кода. Необходимо загрузить архив с исходным кодом программы с репозитория на GitHub, либо воспользоваться утилитой git и склонировать репозиторий себе на компьютер

2. Запуск сборки с помощью команды `./gradlew build`(Linux, MacOS) и `gradlew.bat`(Windows)

3. Теперь по пути `build/distributions` можно найти архивы(в формате `zip` или `tar`) с инструментом


## Раздел Releases на GitHub
1. Открываем [страницу инструмента на GitHub](https://github.com/vobbla16/verchk)
2. Переходим на страницу последнего релиза
3. Скачиваем архив с последней стабильной версией инструмента

## Артефакт GitHub Actions
1. Открываем [страницу инструмента на GitHub](https://github.com/vobbla16/verchk)
2. Переходим на вкладку Actions
3. Переходим на страницу последней сборки
4. Скачиваем артефакт из раздела Artifacts
