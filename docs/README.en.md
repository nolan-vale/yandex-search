<div align="center">

← [Русский](../README.md)

# yandex-search

**CLI for [Yandex Search API](https://yandex.cloud/en/services/search-api) — web search and YandexGPT generative search from your terminal.**

[![PyPI](https://img.shields.io/pypi/v/yandex-search?color=ff6a00&label=PyPI)](https://pypi.org/project/yandex-search/)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-ff6a00.svg)](https://python.org)
[![License: MIT](https://img.shields.io/badge/license-MIT-ff6a00.svg)](../LICENSE)

</div>

---

`yandex-search` wraps the [Yandex Search API](https://yandex.cloud/en/services/search-api) in two terminal commands. `yandex-search` returns structured web results (title, URL, domain, date, text snippets). `yandex-gen` answers questions using YandexGPT with cited sources. Both commands support `--json` for scripts and AI agents.

## Start in 60 seconds

**Step 1 — Install:**
```bash
uv tool install yandex-search
```

> No `uv`? Run `curl -LsSf https://astral.sh/uv/install.sh | sh`, or use `pip install yandex-search`.

**Step 2 — Set up Yandex Cloud:**
1. Register at [cloud.yandex.ru](https://cloud.yandex.ru)
2. Create a service account and API key under **IAM**
3. Enable **Yandex Search API** for your folder ([quickstart](https://yandex.cloud/en/docs/search-api/quickstart))
4. Copy your **API key** and **Folder ID** from the console

**Step 3 — Set credentials:**
```bash
mkdir -p ~/.search-api
echo '{"apiKey": "your-key", "folderId": "your-folder-id"}' > ~/.search-api/config.json
```

> Or via env vars: `export YANDEX_API_KEY=... && export YANDEX_FOLDER_ID=...`

**Step 4 — Search:**
```bash
yandex-search "smart city digital platform"
```

## Commands

| Command | What it does |
|---|---|
| `yandex-search <query>` | Web search: returns title, URL, domain, date, text passages. |
| `yandex-gen <query>` | Generative search: YandexGPT writes an answer with cited sources. |

Both commands accept `--json` for `jq`, scripts, and AI agents.

## Examples

```bash
# Web search
yandex-search "smart city digital platform monograph"

# Restrict to a domain
yandex-search "async python" --site habr.com

# Search the .com Yandex index, more results
yandex-search "machine learning" -t com -n 20

# Generative answer with citations
yandex-gen "explain the difference between monolith and microservices"

# JSON output — extract all URLs
yandex-search "query" --json | jq -r '.[].url'

# Filter by domain pattern
yandex-search "regulations" --json \
  | jq '[.[] | select(.domain | test("gov\\.ru"))]'
```

## Options reference

**`yandex-search`**

| Flag | Default | Description |
|---|---|---|
| `-n` / `--num-results` | `10` | Number of results |
| `-t` / `--type` | `ru` | Index: `ru` · `com` · `tr` · `kk` · `be` · `uz` |
| `-r` / `--region` | — | Region code (e.g. `213` for Moscow) |
| `-p` / `--page` | `0` | Page number (zero-indexed) |
| `--site` | — | Restrict results to this domain |
| `--json` | off | JSON array: `[{title, url, domain, date, passages}]` |

**`yandex-gen`**

| Flag | Default | Description |
|---|---|---|
| `--site` | — | Restrict sources to this domain |
| `--json` | off | Raw JSON from Yandex |

## For AI agents and scripts

`yandex-search` is designed to be called by AI coding assistants (Claude Code, Codex, Cursor, etc.). All commands are stateless and read-only.

```bash
# Agent pattern: search → extract URLs
yandex-search "monographs on topic" --json | jq -r '.[].url' | head -5

# Collect multiple pages
for page in 0 1 2; do
  yandex-search "query" -p $page --json
done | jq -s 'add'
```

→ **[Full documentation](USAGE.md)**（RU）

---

<div align="center">
<sub>Built on <a href="https://yandex.cloud/en/services/search-api">Yandex Search API</a> · MIT License</sub>
</div>
