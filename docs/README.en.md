<div align="center">

← [Русский](../README.md)

# yandex-search

**Yandex Search API for developers. From your terminal.**

[![PyPI](https://img.shields.io/pypi/v/yandex-search?color=ff6a00&label=PyPI)](https://pypi.org/project/yandex-search/)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-ff6a00.svg)](https://python.org)
[![License: MIT](https://img.shields.io/badge/license-MIT-ff6a00.svg)](../LICENSE)

</div>

---

CLI for [Yandex Search API](https://yandex.cloud/en/services/search-api): web search with structured metadata (domain, date, text snippets) and generative search powered by YandexGPT with cited sources. Built for automation, AI agents, and working with Russian-language sources.

## Why yandex-search?

**The Russian internet in clean JSON.**  
Domains, publication dates, text passages. Nothing extra. Ready for pipelines, scripts, and agents.

**Generative search with citations.**  
`yandex-gen` doesn't just return links — YandexGPT synthesizes an answer and cites each source.

**Flexible, no boilerplate.**  
Domain filter (`--site`), region, page, search type. One `--json` flag and the output goes to `jq`, a script, or an agent.

## Install

```bash
uv tool install yandex-search
```

You need a [Yandex Cloud](https://cloud.yandex.ru) account with Search API enabled:

```bash
mkdir -p ~/.search-api
echo '{"apiKey": "your-key", "folderId": "your-folder-id"}' > ~/.search-api/config.json
```

Or via environment variables:

```bash
export YANDEX_API_KEY=your-key
export YANDEX_FOLDER_ID=your-folder-id
```

## Examples

```bash
# Web search
yandex-search "smart city digital platform monograph"

# Restrict to a domain
yandex-search "async python" --site habr.com

# Generative answer with citations
yandex-gen "explain the difference between monolith and microservices"

# JSON output for pipelines
yandex-search "query" --json | jq -r '.[].url'

# Search the .com Yandex index
yandex-search "machine learning" -t com -n 20
```

## Full documentation

→ **[USAGE.md](USAGE.md)**（RU）— all commands, flags, output formats, and scripting examples.

---

<div align="center">
<sub>Built on <a href="https://yandex.cloud/en/services/search-api">Yandex Search API</a> · MIT License</sub>
</div>
