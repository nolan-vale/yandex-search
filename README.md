<div align="center">

[English](docs/README.en.md)

<!--
  ОБЛОЖКА — сгенерируй по промпту ниже, сохрани как docs/cover.png, затем раскомментируй строку.

  Промпт (Midjourney / DALL-E 3 / Stable Diffusion):
  "A dark terminal window with glowing Cyrillic search results streaming across the screen,
  Moscow skyline blurred in the background at night, deep navy blue and warm orange gradient,
  minimalist developer tool aesthetic, no UI chrome, no text overlay, professional tech product,
  wide cinematic banner, 2:1 aspect ratio"

  <img src="docs/cover.png" alt="yandex-search" width="100%">
-->

# yandex-search

**Яндекс поиск и генеративный ИИ — прямо из терминала.**

[![PyPI](https://img.shields.io/pypi/v/yandex-search?color=ff6a00&label=PyPI)](https://pypi.org/project/yandex-search/)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-ff6a00.svg)](https://python.org)
[![License: MIT](https://img.shields.io/badge/license-MIT-ff6a00.svg)](LICENSE)
[![Stars](https://img.shields.io/github/stars/davidparker7966-design/yandex-search?style=social)](https://github.com/davidparker7966-design/yandex-search)

</div>

---

CLI для [Yandex Search API](https://yandex.cloud/en/services/search-api): веб-поиск со структурированными метаданными и генеративный поиск на YandexGPT с цитированием источников. Идеально для автоматизации, AI-агентов и работы с русскоязычными источниками.

## Зачем yandex-search?

**Русский интернет — в чистом JSON.**  
Домены, даты публикации, сниппеты. Ничего лишнего. Готово для пайплайнов, скриптов и агентов.

**Генеративный поиск с источниками.**  
`yandex-gen` даёт не просто список ссылок — YandexGPT синтезирует ответ и цитирует каждый источник.

**Гибко и без лишнего кода.**  
Фильтр по домену (`--site`), регион, страница, тип поиска. Один флаг `--json` — и вывод идёт в `jq`, скрипт или агент.

## Установка

```bash
uv tool install yandex-search
```

Нужен аккаунт [Yandex Cloud](https://cloud.yandex.ru) с включённым Search API:

```bash
mkdir -p ~/.search-api
echo '{"apiKey": "ваш-ключ", "folderId": "ваш-folder-id"}' > ~/.search-api/config.json
```

## Примеры

```bash
# Поиск по теме
yandex-search "умный город цифровая платформа монография"

# Только с конкретного сайта
yandex-search "async python" --site habr.com

# Генеративный ответ с цитированием
yandex-gen "в чём разница между монолитом и микросервисами"

# JSON для пайплайна — извлечь все URL
yandex-search "запрос" --json | jq -r '.[].url'

# Поиск в .com-индексе Яндекса
yandex-search "machine learning" -t com -n 20
```

## Полная документация

→ **[docs/USAGE.md](docs/USAGE.md)** — все команды, флаги, форматы вывода и примеры скриптов.

---

<div align="center">
<sub>Работает на <a href="https://yandex.cloud/en/services/search-api">Yandex Search API</a> · MIT License · <a href="https://github.com/davidparker7966-design/yandex-search/issues">Сообщить о проблеме</a></sub>
</div>
