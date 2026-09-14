# Kinoteatrkg

Онлайн-источник **Kinoteatr.kg**: сайт по умолчанию **`https://kinoteatr.kg`**. В **`Invoke`** используется плагин **`kinoteatrkg`**, отображаемое имя — **`Kinoteatr.kg`**.

## Интерфейс

**`IModuleLoaded`**, **`IModuleOnline`**.

## Условие (`Invoke`)

Источник возвращается для фильмов, если **`args.serial == -1`** или **`args.serial == 0`**. Для сериалов возвращается **`null`**.

## Глобальный поиск

При **`Loaded`** балансер **`kinoteatrkg`** добавляется в **`CoreInit.conf.online.with_search`**.

Поиск выполняется в два этапа: сначала быстрый **`/site/suggest?term=...`**, затем fallback через **`/search?query=...`**. Кандидаты дополнительно проверяются по названию/оригинальному названию и году на странице фильма.

## Подпись качества

**`EventListener.OnlineApiQuality`**: для **`e.balanser == "kinoteatrkg"`** возвращается подпись **` ~ 1080p`**.

## Конфигурация

Секция в `init.conf`: **`Kinoteatrkg`** (`OnlinesSettings`).

По умолчанию: **`enable = true`**, **`displayindex = 570`**, **`streamproxy = true`**. Хост: **`https://kinoteatr.kg`**.

Настройки секции применяются во время работы модуля. В частности, **`enable = false`** отключает источник, а **`streamproxy = false`** отключает проксирование видеопотока через Lampac.

## Воспроизведение

Модуль извлекает прямой **MP4** из страницы фильма и исключает trailer-ссылки. При включённом **`streamproxy`** поток передаётся через **`HostStreamProxy`** с **`Referer`** страницы фильма; при отключённом **`streamproxy`** возвращается прямой MP4 URL.

## HTTP

| Маршрут | Назначение |
|---------|------------|
| **`lite/kinoteatrkg`** | Основная выдача. |

## Файлы

**`ModInit.cs`**, **`Controller.cs`**.
