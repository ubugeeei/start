# start

Default technology selection and engineering rules for AI-assisted project creation.

## What is this?

A set of opinionated guidelines that AI agents follow when scaffolding new projects. Covers stack choices, tooling defaults, code style, and CI/CD conventions.

## Key Principles

- Predictable tooling with a single stack-appropriate task entry point
- Minimal incidental complexity
- Strong static guarantees
- Small, focused modules
- Low allocation overhead where performance matters

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

The dev shell provides `Node.js 24` and `pnpm 10`.
The project guidelines continue to standardize shared project tasks on `Vite Task` via `vp` and `vp run`.

## License

MIT
