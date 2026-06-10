# TypeScript Technology Selection

Use TypeScript when the project needs strong compatibility with the JavaScript ecosystem, fast iteration, and a unified modern web toolchain.

## Runtime and Package Management

- Target `Node.js 24+`.
- Use `Vite+` as the default TypeScript toolchain.
- Use `pnpm 11+` as the package manager.
- Use `pnpm` workspaces for monorepos and multi-package projects.
- Let `Vite+` manage the runtime, package manager, and frontend workflow.
- Use `vite-task` as the task runner.
- Standardize all day-to-day commands behind `vp`.
- Use `vp install` instead of calling `pnpm install` directly.
- Place workspace packages under `./npm`.

## Formatting, Linting, and Testing

- Use `oxfmt` for formatting.
- Configure formatting with `semi: true`.
- Configure formatting with `trailingComma: true`.
- Use single quotes by default for TypeScript configuration and task scripts.
- Use `vp check` as the default verification entry point.
- Prefer `vp check` over `vp fmt` and `vp lint` for normal development work.
- Keep `vp fmt` and `vp lint` available only for focused troubleshooting or exceptional narrow runs.
- Enable type-aware linting by default.
- Enable type checking by default.
- Make both `vp lint` and `vp check` run `oxlint` with both `--type-aware` and `--type-check`.
- Encode TypeScript prohibitions as deterministic `oxlint`, formatter, type-check, or custom check rules instead of natural-language policy alone.
- Use `tsgo` instead of `tsc` when a standalone TypeScript type-check command is needed.
- Using `oxlint --type-check` is acceptable when it provides the needed type-checking coverage.
- Use `vitest` for testing.
- Use Vitest Browser Mode for browser-facing behavior.
- Use `vp test` to run the test suite.
- Write many concrete test cases to improve Agentic Coding iteration accuracy.
- Prefer exact full-value assertions over `includes`, `contains`, substring, or partial-object checks.

## Build and Content Tooling

- Use `Vite+` for the default dev and build workflow.
- Use `vp dev` for local development.
- Use `vp build` for production builds.
- Use `vp pack` when packaging TypeScript libraries.
- Let `tsdown` handle library packaging when `vp pack` delegates to it.
- Use `ox-content` when content processing is needed.

## Development Workflow

- Make `vp dev` start the development environment in one command.
- For CLI tools, make `vp run cli` expose the TypeScript executable through the shared task entry point.
- Make `vp check` the primary local and CI verification command.
- Make `vp check --fix` handle the default formatting and static verification autofix workflow.
- Make `vp check` run the repository formatting, lint, and type-check workflow from the shared entry point.
- For multi-package or multi-runtime workspaces, make `pnpm run verify` call formatting, type checking, linting, builds, tests, audits, and package-readiness checks.
- Use Vite+'s built-in staged-file workflow instead of a separate `lint-staged` setup when possible.
- Configure `staged: { '*': 'vp check --fix' }` in `vite.config.ts` so staged files are checked through Vite+'s staged workflow.
- Run the staged-file hook through `vp staged`.
- Make `vp test` run the TypeScript test workflow from the shared entry point.
- Make `vp build` run the production build workflow from the shared entry point.
- Make `vp pack` run the library packaging workflow from the shared entry point.
- Make `vp run release <patch|minor|major|alpha|beta|rc>` bump versions, create the corresponding Git tag, and push the tag.
- Release from the tag-push workflow instead of publishing directly from local state.

## Script Execution Rules

- Use Node.js stable `--strip-type` for executable TypeScript scripts.
- Treat `--strip-type` as the standard approach because it is stable in Node.js.
- Do not use `ts-node`.
- Do not use `tsx`.
- Prefer erasable syntax only for executable scripts.
- Prefer invoking project scripts through `vp run`.

## TypeScript Compiler Preferences

- Enable `erasableSyntaxOnly`.
- Enable `isolatedDeclarations`.
- Enable `verbatimModuleSyntax`.
- Target `ESNext`.
- Use ESM only.
- Enable `noUncheckedIndexedAccess`.
- Do not use `tsc` as the default verification command.

## Code Organization

- Keep files at `300` lines or fewer.
- Split code into separate files aggressively when responsibilities begin to mix.
- Prefer minimal, focused modules over large multi-purpose files.
- Use `snake_case` for directory names and file names.
- Place examples under `./examples`.
- Keep multi-package TypeScript code under `./npm`.

## CI and Publishing

- Set up CI with GitHub Actions.
- Trigger release workflows from tag pushes.
- Use npm trusted publishing.
- Do not store npm tokens in GitHub Actions.
- Make npm publishing workspace-aware using `vp pm publish` with `workspace:` protocol resolution.
- Perform the initial publish from the local CLI, not from CI.
- Authenticate to npm using passkeys (`npm login --auth-type=web`).
- Ensure the publish workflow builds and bundles each package correctly before publishing.
- Use `setup-vp` in CI when the workflow depends on `vp`.
- Install with `vp install --frozen-lockfile` in CI.
- For publishable workspaces, verify package files with a dry-run or package-readiness task before publishing.
- Publish from GitHub Actions with provenance when trusted publishing is configured.
