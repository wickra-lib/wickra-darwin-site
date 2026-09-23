# Java

The Java binding links the C ABI via a small JNI shim. Construct a `Darwin` from a
JSON spec and drive it with `command(json) -> json`.

```xml
<!-- Maven Central -->
<dependency>
  <groupId>org.wickra</groupId>
  <artifactId>wickra-darwin</artifactId>
  <version>0.1.4</version>
</dependency>
```

```java
import org.wickra.darwin.Darwin;

String spec =
    "{\"seed\":1,\"population\":8,\"generations\":3,"
  + "\"mutation_rate\":0.2,\"crossover_rate\":0.6,\"fitness\":\"sharpe\","
  + "\"search_space\":{\"indicators\":[{\"name\":\"rsi\",\"param_ranges\":[{\"min\":2,\"max\":30,\"step\":1}]}],"
  + "\"rules\":\"single_threshold\",\"max_conditions\":1},\"elitism\":1,\"top\":5}";

try (Darwin darwin = new Darwin(spec)) {
    String report = darwin.command("{\"cmd\":\"evolve\",\"data\":{ /* symbol -> candles */ }}");
    System.out.println(report);
}
```

## More

- [central.sonatype.com/artifact/org.wickra/wickra-darwin](https://central.sonatype.com/artifact/org.wickra/wickra-darwin)
- [Source & examples](https://github.com/wickra-lib/wickra-darwin/tree/main/examples/java)
