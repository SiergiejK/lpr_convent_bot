﻿Телеграм-бот для голосований


Голоса тех, кто не проголосовал полностью (т.е. не подтвердил), не учитываются


## Как установить


```
python -m pip install requests bottle
```


## Как запустить


### pythonanywhere

9 из 10 файлов в рабочую папку проекта на paw (/mysite/ по умолчанию)

project_home в файле _wsgi должен совпадать с папкой выше

файл _wsgi в /var/www/ (доступен в paw с вкладки Web)

help.md должен лежать и в /mysite/ и уровнем выше (todo: fix)



### telegram


Создать бота через BotFather, он должен иметь право добавлять людей

Создать группу (ботоадмином)

Превратить группу в супергруппу (добавить, например, админа), у группы изменится id


### pythonanywhere


config.py.example переименовать в config.py, внести переменные (id группы, токен бота...)

Запустить бота (main.py) через WSGI


### telegram


Добавить в группу бота, если id неправильный, то он сразу выйдет

Добавить голосующих

## changelog


### 2023-09-01


Три способа (метода) голосования вместо двух. Было setsimple простое (равновесное),

setpriority преференциальное (в пределах кол-ва мандатов). Добавлены режимы ranklimit

преференциальное (в пределах кол-ва мандатов) и rankall преференциальное (по всем

кандидатам); setpriority теперь синоним rankall, ranklimit остался, но не используется.

rankall использует len(candidates) вместо wincount для ранжира, wincount только отделяет

победителей от прочих. Булева priorityVoting заменена на votingType с тремя значениями.



Введена корректная обработка ситуации, когда количество мандатов и кандидатов совпадает.

Для этого вставлен байпасс проверки ситуации "одинаково голосов" и исправлено сообщение

под ситуацию "losers = None".



Исправлена ссылка на голосование: telegram.me/{BOT_NAME}?/start=start

на telegram.me/{BOT_NAME}?start=start



Исправлена ошибка при удалении/выходе человека из чата (лишний аргумент из старого кода).



В config.py квадратичная прогрессия заменена на обычную.



Уточнён текст некоторых сообщений, в том числе:

Сообщение о баллах при преференциальном голосовании (было ошибочно при равновесном).

Проверка и сообщение, что кандидат уже в списке (было молча).

Сообщение при смене способа (метода) голосования (было молча).


### 2023-08-30


Форк от проекта lpr-voting-bot, версии от 2023-08-30.