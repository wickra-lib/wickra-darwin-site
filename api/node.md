# Node.js

The Node package is a native napi addon over the Rust core. Construct a `Darwin`
from a JSON spec and drive it with `command(json) -> json`.

```bash
npm install wickra-darwin
```

```javascript
import { Darwin } from 'wickra-darwin'

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
console.log(report.best[0].fitness)
```

## More

- [npmjs.com/package/wickra-darwin](https://www.npmjs.com/package/wickra-darwin)
- [Source & examples](https://github.com/wickra-lib/wickra-darwin/tree/main/examples/node)
