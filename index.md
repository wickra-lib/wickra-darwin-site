---
layout: home
title: Wickra Darwin — evolutionary strategy search
titleTemplate: false

hero:
  name: "Wickra Darwin"
  text: "AlphaZero for trading strategies."
  tagline: "Evolutionary strategy search at millions of backtests per second — mutate and cross JSON strategy specs to brute-force alpha across the indicator space. The search is data, not code — deterministic and byte-identical across ten languages."
  image:
    src: /wickra-mark.svg
    alt: Wickra Darwin
  actions:
    - theme: brand
      text: View on GitHub
      link: https://github.com/wickra-lib/wickra-darwin
    - theme: alt
      text: EvolveSpec & search space
      link: https://github.com/wickra-lib/wickra-darwin/blob/main/docs/ARCHITECTURE.md
    - theme: alt
      text: API
      link: /api/rust

features:
  - icon: 🧬
    title: The genome is JSON
    details: A population of StrategySpec genomes — the same spec wickra-backtest runs — is evolved with genetic operators, mutation and crossover, over the indicator search space. Because the genome is data, the exact same search crosses the C ABI and WASM unchanged.
  - icon: ⚡
    title: Millions of backtests per second
    details: "Each candidate is scored by the O(1)-per-tick wickra-backtest engine, so the evolutionary loop sustains a very high backtests-per-second rate — orders of magnitude faster than pandas-based tooling."
  - icon: 📈
    title: The whole indicator space
    details: "The search space ranges over the 514 indicators of the Wickra core and their parameter ranges, so evolution explores real strategies, not toy signals."
  - icon: 🌐
    title: Ten languages, one search
    details: "The core is a JSON-over-C-ABI data API (Darwin::command_json) in Rust, Python, Node.js, WASM, C, C++, C#, Go, Java and R. A developer in any language runs the same evolution."
  - icon: 🎲
    title: Seeded and reproducible
    details: "A fixed portable PRNG drives mutation and crossover, so a given seed produces the byte-identical report — the same winners, the same fitness, every run and every platform."
  - icon: 🧪
    title: Deterministic, proven
    details: The report is byte-identical across all ten bindings for a given seed, pinned by a golden corpus replayed through each binding in CI — the exact cross-language golden invariant.
---

<script setup>
const installTabs = [
  { label: 'Python', lang: 'bash', code: 'pip install wickra-darwin' },
  { label: 'Node',   lang: 'bash', code: 'npm install wickra-darwin' },
  { label: 'Rust',   lang: 'bash', code: 'cargo add wickra-darwin' },
  { label: 'WASM',   lang: 'bash', code: 'npm install wickra-darwin-wasm' },
  { label: 'C',      lang: 'bash', code: '# prebuilt header + library from GitHub releases:\n# github.com/wickra-lib/wickra-darwin/releases' },
  { label: 'C#',     lang: 'bash', code: 'dotnet add package Wickra.Darwin' },
  { label: 'Go',     lang: 'bash', code: 'go get github.com/wickra-lib/wickra-darwin-go' },
  { label: 'Java',   lang: 'xml',  code: '<!-- Maven Central -->\n<dependency>\n  <groupId>org.wickra</groupId>\n  <artifactId>wickra-darwin</artifactId>\n  <version>0.1.0</version>\n</dependency>' },
  { label: 'R',      lang: 'r',    code: 'install.packages("wickradarwin", repos = "https://wickra-lib.r-universe.dev")' },
]

const pyCode = `import json
from wickra_darwin import Darwin

spec = json.dumps({
    "seed": 1, "population": 8, "generations": 3,
    "mutation_rate": 0.2, "crossover_rate": 0.6, "fitness": "sharpe",
    "search_space": {
        "indicators": [{"name": "rsi", "param_ranges": [{"min": 2, "max": 30, "step": 1}]}],
        "rules": "single_threshold", "max_conditions": 1,
    },
    "elitism": 1, "top": 5,
})

darwin = Darwin(spec)
data = {"BTCUSDT": [{"time": 1700000000, "open": 100, "high": 101, "low": 99, "close": 100.5, "volume": 10}]}
report = json.loads(darwin.command(json.dumps({"cmd": "evolve", "data": data})))
print(report["best"][0]["fitness"])`

const nodeCode = `import { Darwin } from 'wickra-darwin'

const spec = JSON.stringify({
  seed: 1, population: 8, generations: 3,
  mutation_rate: 0.2, crossover_rate: 0.6, fitness: 'sharpe',
  search_space: {
    indicators: [{ name: 'rsi', param_ranges: [{ min: 2, max: 30, step: 1 }] }],
    rules: 'single_threshold', max_conditions: 1,
  },
  elitism: 1, top: 5,
})

const darwin = new Darwin(spec)
const data = { BTCUSDT: [{ time: 1700000000, open: 100, high: 101, low: 99, close: 100.5, volume: 10 }] }
const report = JSON.parse(darwin.command(JSON.stringify({ cmd: 'evolve', data })))
console.log(report.best[0].fitness)`

const cliCode = `# Evolve strategies over a directory of <SYMBOL>.csv candle files:
wickra-darwin --spec evolve.json --data ./data

# Same seed, same winners — deterministic across runs:
wickra-darwin --spec evolve.json --data ./data --format json`

const snippetTabs = [
  { label: 'Python', lang: 'python',     code: pyCode },
  { label: 'Node',   lang: 'javascript', code: nodeCode },
  { label: 'CLI',    lang: 'bash',       code: cliCode },
]
</script>

## The search is JSON, not code

An evolution is an `EvolveSpec`: a `seed`, a `population` and `generations`,
mutation and crossover rates, a `fitness`, and a `search_space` over indicators
and their parameter ranges. The engine evolves `StrategySpec` genomes and returns
the ranked survivors.

```json
{
  "seed": 42,
  "population": 64,
  "generations": 20,
  "mutation_rate": 0.15,
  "crossover_rate": 0.6,
  "fitness": "sharpe",
  "search_space": {
    "indicators": [
      { "name": "rsi", "param_ranges": [{ "min": 2, "max": 30, "step": 1 }] },
      { "name": "ema", "param_ranges": [{ "min": 5, "max": 200, "step": 5 }] }
    ],
    "rules": "single_threshold",
    "max_conditions": 2
  },
  "elitism": 2,
  "top": 10
}
```

## Install

The same search from every language — native Rust, Python, Node.js and WASM, plus
a C ABI for C, C++, C#, Go, Java and R.

<InstallTabs :tabs="installTabs" />

## Run it from any language

Construct a `Darwin` from the JSON spec, then drive it with
`command(json) -> json`. A given seed produces the same ranked survivors in every
binding.

<InstallTabs :tabs="snippetTabs" />

## Built on the Wickra core

Wickra Darwin is part of the [Wickra](https://wickra.org) ecosystem. Every
candidate is scored by [`wickra-backtest`](https://github.com/wickra-lib/wickra-backtest)
over the 514 indicators of [`wickra-core`](https://github.com/wickra-lib/wickra),
so an evolved strategy sees exactly the same numbers a live chart would.

> Wickra Darwin is a software library, not a trading system, and comes with no
> warranty — an evolved strategy is not financial advice. Use at your own risk.
