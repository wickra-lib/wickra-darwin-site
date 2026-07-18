# C\#

The .NET binding wraps the C ABI. Construct a `Darwin` from a JSON spec and drive
it with `Command(json) -> json`.

```bash
dotnet add package Wickra.Darwin
```

```csharp
using Wickra.Darwin;

const string spec =
    "{\"seed\":1,\"population\":8,\"generations\":3," +
    "\"mutation_rate\":0.2,\"crossover_rate\":0.6,\"fitness\":\"sharpe\"," +
    "\"search_space\":{\"indicators\":[{\"name\":\"rsi\",\"param_ranges\":[{\"min\":2,\"max\":30,\"step\":1}]}]," +
    "\"rules\":\"single_threshold\",\"max_conditions\":1},\"elitism\":1,\"top\":5}";

using var darwin = new Darwin(spec);
var report = darwin.Command("{\"cmd\":\"evolve\",\"data\":{ /* symbol -> candles */ }}");
Console.WriteLine(report);
```

## More

- [nuget.org/packages/Wickra.Darwin](https://www.nuget.org/packages/Wickra.Darwin)
- [Source & examples](https://github.com/wickra-lib/wickra-darwin/tree/main/examples/csharp)
