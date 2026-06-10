# Rust Technology Selection

Use Rust when the project needs native performance, predictable resource usage, WebAssembly support, or Node.js native integration.

## Core Tooling

- Use `clippy` and treat its feedback seriously.
- Use `rustfmt` and make `cargo fmt --all --check` part of verification.
- Use `insta` for snapshot testing.
- Add benchmarks early and maintain broad benchmark coverage.
- Use Cargo workspaces for multi-crate projects.
- Use workspace resolver `3` and Rust edition `2024`.
- Pin the Rust toolchain when the project depends on a specific compiler or CI image.
- Use `nix` flakes to manage the development environment.
- Use `Vite Task` as the shared task runner and expose repository workflows through `vp run`.
- Deny `unsafe_code`, `unused_must_use`, `dbg_macro`, `todo`, and `unwrap_used` by default.
- Encode Rust prohibitions as deterministic `clippy`, `rustc`, formatter, layout, or custom check rules instead of natural-language policy alone.

## Interop and Targets

- For Rust to JavaScript or Node.js interop, use `napi-rs`.
- Support `wasm` when browser execution or portable deployment is useful.
- For Rust-backed JavaScript plugins, expose hot paths through NAPI-RS and keep the JavaScript wrapper thin.
- Prefer one Rust call per file over one Rust call per AST node.
- Keep NAPI payloads small and stable.

## Data Structure Preferences

- Prefer `CompactString` over `String` when a compact owned string is sufficient.
- Prefer `SmallVec` over `Vec` when bounded or stack-friendly storage is appropriate.
- Use `memchr` for byte-oriented search and parsing paths when it fits.
- Use string interning when repeated string values would otherwise allocate heavily.
- Use `FxHashMap` when a fast hash map is appropriate.
- Use `phf` for static lookup tables known at compile time.
- Use arena or bump allocation for short-lived per-file rule state when it reduces allocation overhead.
- Use `GhostCell` or similar ownership patterns when they simplify reusable state without runtime borrowing cost.

## Memory and Performance Rules

- Minimize memory allocation.
- Do not introduce unnecessary heap allocation.
- Prefer arena allocation where it improves ownership simplicity or allocation cost.
- Do not use `.clone()` unless it is clearly necessary.
- Do not use `.to_string()` unless it is clearly necessary.
- Do not use macros unless they are clearly necessary.
- Do not use `format!` unless there is no simpler alternative.
- Design APIs and data flow to avoid incidental copies.
- Do not use `std::collections::HashMap` or `HashSet` in hot rule code unless the slower hash behavior is justified.
- Avoid per-node FFI calls and per-node type-service calls.

## Code Organization

- Keep files at `300` lines or fewer.
- Split code into separate files aggressively.
- Prefer narrow modules with explicit responsibilities.
- Use `snake_case` for directory names and file names.
- Use named module files instead of `mod.rs`.
- Place examples under `./examples`.
- Keep workspace crates under `./crates`.

## Development Workflow

- Make `nix develop` start the development environment in one command.
- For CLI tools, make `vp run cli` expose the Rust executable through the shared task entry point.
- Back `vp run cli` with a dev build for Rust because release builds are too slow during development.
- Make `vp run fmt` run the Rust formatting workflow.
- Make `vp run lint` run the Rust lint workflow from the shared repository entry point.
- Make `vp run check` run the Rust check workflow from the shared repository entry point.
- Make `vp run test` run the Rust test workflow from the shared repository entry point.
- Make `vp run bench:check` compile benchmarks without running them for CI verification.
- For hybrid Rust and TypeScript workspaces, make `pnpm run verify` call Rust formatting, type-aware linting, Clippy, layout checks, builds, tests, benchmark compilation, security audits, license checks, and package readiness checks.
- Make `vp run release <patch|minor|major|alpha|beta|rc>` bump versions, create the corresponding Git tag, and push the tag.
- Release from the tag-push workflow instead of publishing directly from local state.

## CI and Publishing

- Set up CI with GitHub Actions.
- Trigger release workflows from tag pushes.
- Use trusted publishing for crates.
- Do not store registry tokens in GitHub Actions.
- Publish crates from GitHub Actions through trusted publishing.
- Use `voidzero-dev/setup-vp` with `Node.js 24` when Rust checks are coordinated through `vp`.
- Install the Rust toolchain with `clippy` and `rustfmt`.
- Cache Cargo artifacts in CI.
