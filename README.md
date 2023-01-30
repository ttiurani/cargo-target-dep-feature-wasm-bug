# cargo-target-dep-feature-wasm-bug

Replicates bug with cargo and transitive WASM target dependencies activating features
which prevent compilation.

## Reproduce

```bash
cd wasm-compatible
cargo build
# Finished dev [unoptimized + debuginfo] target(s) in 0.06s
cargo build --target=wasm32-unknown-unknown
# Finished dev [unoptimized + debuginfo] target(s) in 0.05s

cd ../top
cargo build
# Finished dev [unoptimized + debuginfo] target(s) in 0.05s
cargo build --target=wasm32-unknown-unknown
   Compiling tokio v1.25.0
error: Only features sync,macros,io-util,rt,time are supported on wasm.
   --> /Users/ttiurani/.cargo/registry/src/github.com-1ecc6299db9ec823/tokio-1.25.0/src/lib.rs:462:1
    |
462 | compile_error!("Only features sync,macros,io-util,rt,time are supported on wasm.");
    | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

error: could not compile `tokio` due to previous error
```
