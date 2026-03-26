# Rust Technology Selection

Use Rust when the project needs native performance, predictable resource usage, WebAssembly support, or Node.js native integration.

## Core Tooling

- Use `clippy` and treat its feedback seriously.
- Do not use `rustfmt` as a required part of this workflow.
- Use `insta` for snapshot testing.
- Add benchmarks early and maintain broad benchmark coverage.
- Use Cargo workspaces for multi-crate projects.
- Use `nix` flakes to manage the development environment.
- Use `Vite Task` as the shared task runner and expose repository workflows through `vp run`.

## Interop and Targets

- For Rust to JavaScript or Node.js interop, use `napi-rs`.
- Support `wasm` when browser execution or portable deployment is useful.

## Data Structure Preferences

- Prefer `CompactString` over `String` when a compact owned string is sufficient.
- Prefer `SmallVec` over `Vec` when bounded or stack-friendly storage is appropriate.
- Use `memchr` for byte-oriented search and parsing paths when it fits.
- Use string interning when repeated string values would otherwise allocate heavily.
- Use `FxHashMap` when a fast hash map is appropriate.
- Use `phf` for static lookup tables known at compile time.

## Memory and Performance Rules

- Minimize memory allocation.
- Do not introduce unnecessary heap allocation.
- Prefer arena allocation where it improves ownership simplicity or allocation cost.
- Do not use `.clone()` unless it is clearly necessary.
- Do not use `.to_string()` unless it is clearly necessary.
- Do not use macros unless they are clearly necessary.
- Do not use `format!` unless there is no simpler alternative.
- Design APIs and data flow to avoid incidental copies.

## Code Organization

- Keep files at `250` lines or fewer.
- Split code into separate files aggressively.
- Prefer narrow modules with explicit responsibilities.
- Use `snake_case` for directory names and file names.
- Place examples under `./examples`.
- Keep workspace crates under `./crates`.

## Development Workflow

- Make `nix develop` start the development environment in one command.
- For CLI tools, make `vp run cli` expose the Rust executable through the shared task entry point.
- Back `vp run cli` with a dev build for Rust because release builds are too slow during development.
- Make `vp run fmt` participate in the shared repository workflow without making `rustfmt` a required Rust formatter.
- Make `vp run lint` run the Rust lint workflow from the shared repository entry point.
- Make `vp run check` run the Rust check workflow from the shared repository entry point.
- Make `vp run test` run the Rust test workflow from the shared repository entry point.
- Make `vp run release:patch` update the version and create a release tag.
- Make `vp run release:minor` update the version and create a release tag.
- Make `vp run release:alpha` update the version and create a release tag.
- Make `vp run release:beta` update the version and create a release tag.

## CI and Publishing

- Set up CI with GitHub Actions.
- Trigger release workflows from tag pushes.
- Use trusted publishing for crates.
- Do not store registry tokens in GitHub Actions.
- Publish crates from GitHub Actions through trusted publishing.
