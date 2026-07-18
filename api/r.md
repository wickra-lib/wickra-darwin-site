# R

The R package links the C ABI. Build a search with `wkdarwin_new`, then drive it
with `wkdarwin_command`.

```r
install.packages("wickradarwin", repos = "https://wickra-lib.r-universe.dev")
```

```r
library(wickradarwin)

spec <- '{"seed":1,"population":8,"generations":3,
          "mutation_rate":0.2,"crossover_rate":0.6,"fitness":"sharpe",
          "search_space":{"indicators":[{"name":"rsi","param_ranges":[{"min":2,"max":30,"step":1}]}],
          "rules":"single_threshold","max_conditions":1},"elitism":1,"top":5}'

darwin <- wkdarwin_new(spec)
data <- '{"BTCUSDT":[{"time":1700000000,"open":100,"high":101,"low":99,"close":100.5,"volume":10}]}'
report <- wkdarwin_command(darwin, paste0('{"cmd":"evolve","data":', data, '}'))
cat(report)
```

## More

- [wickra-lib.r-universe.dev](https://wickra-lib.r-universe.dev)
- [Source & examples](https://github.com/wickra-lib/wickra-darwin/tree/main/examples/r)
