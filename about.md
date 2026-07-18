# About Wickra Darwin

Wickra Darwin evolves trading strategies with a genetic search — mutating and
crossing JSON strategy specs, scoring each candidate with the Wickra backtest
engine at millions of backtests per second. An evolution is a JSON document —
**data, not code** — so the search runs in every one of ten languages and, for a
given seed, returns a byte-for-byte identical report.

## What makes it different

- **The genome is data.** A population of `StrategySpec` genomes — the same spec
  `wickra-backtest` runs — is evolved with genetic operators (mutation + crossover
  across the indicator search space). Because it is data, it crosses the C ABI and
  WASM unchanged.
- **Millions of backtests per second.** Each candidate is scored by the O(1)-per-tick
  engine, so the loop sustains a very high backtests-per-second rate — orders of
  magnitude faster than pandas-based tooling. "AlphaZero for trading strategies."
- **The whole indicator space.** The search ranges over the 514 indicators of the
  Wickra core and their parameter ranges — real strategies, not toy signals.
- **Seeded and reproducible.** A fixed portable PRNG drives mutation and crossover,
  so a given seed produces the byte-identical report on every platform, pinned by a
  golden corpus in CI.

## Why it exists

Strategy search is usually one language, one bespoke loop, and rarely reproducible.
Wickra Darwin defines the search **once**, in Rust, and exposes it as a
JSON-over-C-ABI data API to Rust, Python, Node.js, WASM and — over a C ABI — C, C++,
C#, Go, Java and R. The spec is portable JSON, so the same evolution runs anywhere.

## Open source

Released under the **MIT OR Apache-2.0** license — permissive, OSI-approved, free
for any use including commercial. Source, issues and releases on
[GitHub](https://github.com/wickra-lib/wickra-darwin).

## Disclaimer

Wickra Darwin is a software library, **not** a trading system, and is provided
**as-is with no warranty**. An evolved strategy is a search result over historical
data, not financial advice, and past fitness does not predict future returns. Use
it at your own risk.
