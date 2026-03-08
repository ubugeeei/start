# start

Default technology selection and engineering rules for AI-assisted project creation.

## What is this?

A set of opinionated guidelines that AI agents follow when scaffolding new projects. Covers stack choices, tooling defaults, code style, and CI/CD conventions.

## Stacks

- **TypeScript** — Node.js 24+, pnpm, oxfmt, oxlint, vitest, tsdown
- **Rust** — clippy, insta, napi-rs, wasm support
- **Vue** — Vite v8, component-oriented architecture

## Key Principles

- Predictable tooling with `mise` as the single task runner
- Minimal incidental complexity
- Strong static guarantees
- Small, focused modules
- Low allocation overhead where performance matters

## License

MIT
