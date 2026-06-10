# AI Project Technology Selection Guide

This directory contains the default technology choices and engineering rules for new projects created by AI agents.

## Stacks

- [TypeScript](./typescript.md)
- [Rust](./rust.md)
- [Vue](./vue.md)

## Development Environment

- Use a single shared task entry point instead of ad-hoc shell commands.
- For TypeScript projects, use `Vite+` with `vite-task` and run tasks through `vp`.
- For TypeScript type checking, use `tsgo` instead of `tsc`; using `oxlint --type-check` is acceptable when it provides the needed coverage.
- For static sites, choose `vuerend` with a zero JavaScript first approach as the first option.
- For Rust projects, use `nix` flakes for the toolchain. Enter the environment with `nix develop` and expose shared tasks through `Vite Task` with `vp run`.
- Make the stack entry point start the full development environment in one command.
- For CLI tools, expose the executable through the shared task entry point.
- Use Node.js stable `--strip-type` for executable TypeScript scripts.
- Make formatting, lint, check, and test workflows available from the shared task entry point.
- Express prohibitions as deterministic linter or check rules instead of natural-language policy alone.
- For multi-language workspaces, make `pnpm run verify` the CI contract and let it call the shared `vp` tasks plus stack-specific checks.
- Keep workflow YAML thin: set up toolchains, install with `vp install --frozen-lockfile`, then run the verification contract.

## Testing Discipline

- Write many concrete test cases to improve Agentic Coding iteration accuracy.
- Prefer exact full-value assertions over `includes`, `contains`, substring, or partial-object checks.
- Use partial assertions only when the ignored data is intentionally unstable and document that reason in the test.

## Release Workflow

- Use `vp run release <kind>` for releases, where `<kind>` is `patch`, `minor`, `major`, `alpha`, `beta`, or `rc`.
- Make the release command bump versions, create the corresponding Git tag, and push the tag.
- Release from the tag-push workflow instead of publishing directly from local state.

## CI and Release Automation

- Set up CI with GitHub Actions.
- Use `void.cloud` as the default deployment target unless project constraints require a different host.
- Run release workflows from tag pushes.
- Do not store registry tokens in GitHub Actions.
- Use trusted publishing for package publishing.
- Use `voidzero-dev/setup-vp` with `Node.js 24` when a workflow depends on `vp`.
- For repositories under the `ubugeeei-prod` organization, use the strongest available Blacksmith CI runner; use `blacksmith-32vcpu-ubuntu-2404` when it is available.
- For Rust workspaces, install the pinned Rust toolchain with `clippy` and `rustfmt`, then cache Cargo artifacts.
- Require conventional format when creating Issues and Pull Requests, and do not add `[codex]` markers to Pull Request titles.
- Before merge, confirm CI is passing.

## Repository Layout

- Place examples under `./examples`.
- In Rust and TypeScript monorepos, place Rust crates under `./crates`.
- In Rust and TypeScript monorepos, place TypeScript packages under `./npm`.
- For Rust to JavaScript or Node.js interop, use `napi-rs`.
- Use `snake_case` for directory names and file names.
- Use named Rust module files instead of `mod.rs`.
- Use workspace features instead of ad-hoc multi-package layouts.
- For Rust-backed npm packages, keep Rust crates under `./crates` and independently installable packages under `./npm`.

## Implementation Discipline

- Keep each file at `300` lines or fewer.
- Split files before responsibilities begin to mix.
- Prefer small, separable modules with a single clear responsibility.
- Avoid unnecessary allocations, copies, and convenience abstractions.
- In Rust, prefer `SmallVec`, `CompactString`, and `memchr` where they fit.
- For FFI or plugin hot paths, prefer one batched call per file over one call per AST node or item.

## General Principle

When an AI agent creates a new project, optimize for:

- predictable tooling
- minimal incidental complexity
- strong static guarantees
- small, separable modules
- files that stay under `300` lines by splitting early
- unnecessary allocations and copies avoided by default
- Rust code that leans on `SmallVec`, `CompactString`, and `memchr` where appropriate
- low allocation overhead where performance matters
- conventions that are easy for both humans and agents to follow
