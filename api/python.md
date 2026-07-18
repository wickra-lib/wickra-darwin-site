# Python

The Python package wraps the Rust core over the C ABI. Construct a `Darwin` from a
JSON spec and drive it with `command(json) -> json`.

```bash
pip install wickra-darwin
```

```python
import json
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
print(report["best"][0]["fitness"])
```

## More

- [pypi.org/project/wickra-darwin](https://pypi.org/project/wickra-darwin/)
- [Source & examples](https://github.com/wickra-lib/wickra-darwin/tree/main/examples/python)
