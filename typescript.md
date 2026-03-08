# TypeScript Technology Selection

Use TypeScript when the project needs strong compatibility with the JavaScript ecosystem, fast iteration, and reliable Node.js tooling.

## Runtime and Package Management

- Target `Node.js 24+`.
- Use `pnpm` as the package manager.
- Use `pnpm workspace` for monorepos and multi-package projects.

## Formatting, Linting, and Testing

- Use `oxfmt` for formatting.
- Configure formatting with `semi: true`.
- Configure formatting with `trailingComma: true`.
- Use double quotes by default.
- Use `oxlint` with `--type-aware` and `--type-check`.
- Do not use `tsc`.
- Use `oxlint --type-aware --type-check` for static checking.
- Use `vitest` for testing.

## Build and Content Tooling

- Use `tsdown` for builds.
- Let `tsdown` handle compilation.
- Use `ox-content` when content processing is needed.

## Script Execution Rules

- Use `Node.js --strip-type` for scripts.
- Treat `--strip-type` as the standard approach because it is stable.
- Do not use `ts-node`.
- Do not use `tsx`.
- Prefer erasable syntax only for executable scripts.

## TypeScript Compiler Preferences

- Enable `erasableSyntaxOnly`.
- Enable `isolatedDeclarations`.
- Enable `verbatimModuleSyntax`.
- Target `ESNext`.
- Use ESM only.
- Enable `noUncheckedIndexedAccess`.

## Code Organization

- Keep files small.
- Split code into separate files aggressively when responsibilities begin to mix.
- Prefer minimal, focused modules over large multi-purpose files.
