# Rust Technology Selection

Use Rust when the project needs native performance, predictable resource usage, WebAssembly support, or Node.js native integration.

## Core Tooling

- Use `clippy` and treat its feedback seriously.
- Do not use `rustfmt` as a required part of this workflow.
- Use `insta` for snapshot testing.
- Add benchmarks early and maintain broad benchmark coverage.

## Interop and Targets

- Use `napi-rs` for Node.js bindings.
- Support `wasm` when browser execution or portable deployment is useful.

## Data Structure Preferences

- Avoid `String` when a more compact alternative is sufficient. Prefer `CompactString`.
- Avoid `Vec` when bounded or stack-friendly storage is more appropriate. Prefer `SmallVec`.
- Use string interning when repeated string values would otherwise allocate heavily.
- Use `FxHashMap` when a fast hash map is appropriate.
- Use `phf` for static lookup tables known at compile time.

## Memory and Performance Rules

- Minimize memory allocation.
- Prefer arena allocation where it improves ownership simplicity or allocation cost.
- Do not use `.clone()` unless it is clearly necessary.
- Do not use `.to_string()` unless it is clearly necessary.
- Design APIs and data flow to avoid incidental copies.

## Code Organization

- Keep files small.
- Split code into separate files aggressively.
- Prefer narrow modules with explicit responsibilities.
