# Rust

The native crate. Run an evolution with `evolve`, or drive a `Darwin` handle with
the JSON command protocol every other binding uses.

```bash
cargo add wickra-darwin
```

```rust
use darwin_core::{evolve, EvolveSpec};
use std::collections::BTreeMap;

let spec = EvolveSpec::from_json(SPEC).expect("valid spec");

let mut data = BTreeMap::new();
// ... fill `data` with each symbol's candle history ...

let report = evolve(&spec, &data).expect("evolve");
for ranked in &report.best {
    println!("{}: {}", ranked.rank, ranked.fitness);
}
```

## More

- [crates.io/crates/wickra-darwin](https://crates.io/crates/wickra-darwin) - [docs.rs](https://docs.rs/wickra-darwin)
- [Source & examples](https://github.com/wickra-lib/wickra-darwin/tree/main/examples/rust)
- [EvolveSpec & search space](https://github.com/wickra-lib/wickra-darwin/blob/main/docs/ARCHITECTURE.md)
