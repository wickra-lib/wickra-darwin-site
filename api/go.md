# Go

The Go binding links the C ABI via cgo. Construct a `Darwin` from a JSON spec and
drive it with `Command(json) -> (json, error)`.

```bash
go get github.com/wickra-lib/wickra-darwin-go
```

```go
package main

import (
	"fmt"

	wickra "github.com/wickra-lib/wickra-darwin-go"
)

func main() {
	spec := `{"seed":1,"population":8,"generations":3,` +
		`"mutation_rate":0.2,"crossover_rate":0.6,"fitness":"sharpe",` +
		`"search_space":{"indicators":[{"name":"rsi","param_ranges":[{"min":2,"max":30,"step":1}]}],` +
		`"rules":"single_threshold","max_conditions":1},"elitism":1,"top":5}`

	darwin, err := wickra.New(spec)
	if err != nil {
		panic(err)
	}
	defer darwin.Close()

	data := `{"BTCUSDT":[{"time":1700000000,"open":100,"high":101,"low":99,"close":100.5,"volume":10}]}`
	report, err := darwin.Command(`{"cmd":"evolve","data":` + data + `}`)
	if err != nil {
		panic(err)
	}
	fmt.Println(report)
}
```

## More

- [pkg.go.dev/github.com/wickra-lib/wickra-darwin-go](https://pkg.go.dev/github.com/wickra-lib/wickra-darwin-go)
- [Source & examples](https://github.com/wickra-lib/wickra-darwin/tree/main/examples/go)
