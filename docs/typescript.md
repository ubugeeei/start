# TypeScript Technology Selection

Use TypeScript when the project needs strong compatibility with the JavaScript ecosystem, fast iteration, and reliable Node.js tooling.

## Runtime and Package Management

- Target `Node.js 24+`.
- Use `pnpm` as the package manager.
- Use `pnpm workspace` for monorepos and multi-package projects.
- Place workspace packages under `./packages`.
- Use `mise` to manage the development environment and task entry points.

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

## Development Workflow

- Make `mise run dev` start the development environment in one command.
- For CLI tools, make `mise run cli` expose the TypeScript executable through the shared task entry point.
- Make `mise run fmt` run the TypeScript formatting workflow from the shared repository entry point.
- Make `mise run lint` run the TypeScript lint workflow from the shared repository entry point.
- Make `mise run check` run the TypeScript static check workflow from the shared repository entry point.
- Make `mise run test` run the TypeScript test workflow from the shared repository entry point.
- Make `mise run release patch` update the version and create a release tag.
- Make `mise run release minor` update the version and create a release tag.
- Make `mise run release alpha` update the version and create a release tag.
- Make `mise run release beta` update the version and create a release tag.

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
- Place examples under `./examples`.
- Keep multi-package TypeScript code under `./packages`.

## CI and Publishing

- Set up CI with GitHub Actions.
- Trigger release workflows from tag pushes.
- Use npm trusted publishing.
- Do not store npm tokens in GitHub Actions.
- Make npm publishing workspace-aware using `pnpm publish` with `workspace:` protocol resolution.
- Perform the initial publish from the local CLI, not from CI.
- Authenticate to npm using passkeys (`npm login --auth-type=web`).
- Ensure the publish workflow builds and bundles each package correctly before publishing.
