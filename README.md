# start

Default technology selection and engineering rules for AI-assisted project creation.

## What is this?

A set of opinionated guidelines that AI agents follow when scaffolding new projects. Covers stack choices, tooling defaults, code style, and CI/CD conventions.

## Key Principles

- Predictable tooling with a single stack-appropriate task entry point
- Minimal incidental complexity
- Strong static guarantees with local and CI verification kept in sync
- Small, focused modules
- Files capped at `300` lines and split by responsibility
- Default deployment to `void.cloud`
- Many strict test cases to improve Agentic Coding iteration accuracy
- Prohibitions encoded as deterministic lint or check rules
- Avoid unnecessary allocations, copies, and convenience abstractions
- In Rust, prefer `SmallVec`, `CompactString`, and `memchr` where they fit
- Low allocation overhead where performance matters

## Repository Conventions

- Place Rust crates under `./crates`.
- Place TypeScript packages under `./npm`.
- Place examples under `./examples`.
- For Rust to JavaScript or Node.js interop, use `napi-rs`.
- Use Node.js stable `--strip-type` for executable TypeScript scripts.
- Use `snake_case` for directory names and file names.
- Keep each file at `300` lines or fewer.
- Split files before responsibilities begin to mix.
- Use named Rust module files instead of `mod.rs`.

## Usage

Fetch individual guideline files via the GitHub API:

```sh
# Tech selection overview
gh api repos/ubugeeei/start/contents/docs/general.md --jq '.content' | base64 -d

# TypeScript
gh api repos/ubugeeei/start/contents/docs/typescript.md --jq '.content' | base64 -d

# Rust
gh api repos/ubugeeei/start/contents/docs/rust.md --jq '.content' | base64 -d

# Vue
gh api repos/ubugeeei/start/contents/docs/vue.md --jq '.content' | base64 -d
```

## Local Development

Use `nix` for the local toolchain in this repository.

```sh
nix develop
vp install
vp fmt
```

The dev shell provides `Node.js 24` and `pnpm`; `packageManager` pins `pnpm 11`.
The project guidelines continue to standardize shared project tasks on `Vite Task` via `vp` and `vp run`.

## License

MIT
