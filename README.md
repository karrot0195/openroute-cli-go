# openroute-cli-go

A Go CLI that fetches and displays OpenRouter model listings in a benchmark-sorted table.

Built with **Go 1.26.9**. Uses `github.com/karrot0195/go-utils/pkg/openroute` for API integration.

## Directory Structure

```
openroute-cli-go/
├── assets/
│   └── cmd_openroute.png      # CLI diagram
├── bin/                       # build output (./bin/openroute)
├── cmd/
│   └── openroute/
│       └── main.go            # CLI entry point
├── makefile                   # build / clean targets
├── go.mod                     # module openroute-cli-go (Go 1.26.9)
├── go.sum                     # dependency checksums
└── README.md
```

## Binary

- **`openroute`** — fetches model data from `https://openrouter.ai/api/v1/models`, caches results, and prints a sorted table.

## Quick Start

```bash
# Build
make build

# Fetch free models (default)
./bin/openroute --type free

# Fetch all models
./bin/openroute --type all
```

## Usage

```
openroute [--type free|all]
```

| Flag     | Default | Description                                   |
| -------- | ------- | --------------------------------------------- |
| `--type` | `free`  | Filter models: `free` (id ends with `:free`) or `all` |

## Features

- **API fetching** — downloads the model list from OpenRouter.
- **Intelligent caching** — results are saved to a dated cache file in the OS temp directory. If today's cache exists, it is reused with no network call.
- **Filtering** — `free` keeps only models whose id ends with `:free`; `all` keeps everything.
- **Benchmark sorting** — models are ranked by combined `coding_index + intelligence_index` (Artificial Analysis benchmarks), descending.
- **Tabular output** — columns for id, name, coding index, intelligence index, combined sum, and per-million-token pricing.
- **Price formatting** — per-token prices scaled to per-million-token cost.

## Dependencies

- Go 1.26.9+
- `github.com/karrot0195/go-utils` (indirect)
- Network access to `openrouter.ai` on first run (subsequent runs use cache)
