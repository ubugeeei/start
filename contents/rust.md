# Rust Technology Selection

Use Rust when the project needs native performance, predictable resource usage, WebAssembly support, or Node.js native integration.

## Core Tooling

- Use `clippy` and treat its feedback seriously.
- Do not use `rustfmt` as a required part of this workflow.
- Use `insta` for snapshot testing.
- Add benchmarks early and maintain broad benchmark coverage.
- Use `mise` to manage the development environment and task entry points.

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
- Place examples under `./examples`.

## Development Workflow

- Make `mise run dev` start the development environment in one command.
- Make `mise run fmt` participate in the shared repository workflow without making `rustfmt` a required Rust formatter.
- Make `mise run lint` run the Rust lint workflow from the shared repository entry point.
- Make `mise run check` run the Rust check workflow from the shared repository entry point.
- Make `mise run test` run the Rust test workflow from the shared repository entry point.
- Make `mise run release patch` update the version and create a release tag.
- Make `mise run release minor` update the version and create a release tag.
- Make `mise run release alpha` update the version and create a release tag.
- Make `mise run release beta` update the version and create a release tag.

## CI and Publishing

- Set up CI with GitHub Actions.
- Trigger release workflows from tag pushes.
- Use trusted publishing for crates.
- Do not store registry tokens in GitHub Actions.
- Publish crates from GitHub Actions through trusted publishing.
