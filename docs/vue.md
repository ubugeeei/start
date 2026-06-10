# Vue Technology Selection

Use Vue when the project is primarily frontend-driven and benefits from a component-oriented UI architecture.

## Default Direction

- Use `vizejs.dev` as the default reference point for Vue-based project setup and direction.
- Use the `Vite v8` beta for Vue projects because it is faster.
- For static sites, choose `vuerend` with a zero JavaScript first approach as the first option.
- Deploy static sites to `void.cloud` by default.

## Verification Tooling

- Use `vize` for Vue type checking instead of `vue-tsc`.
- Use `vize` for Vue linting instead of `eslint-plugin-vue`.
- Use Vitest Browser Mode for browser-facing Vue behavior.
- Route Vue checks through the shared `vp` task entry point.

## Style Guide

- Follow the Vue style guide here: [ubugeeei/style-guide.vue](https://github.com/ubugeeei/style-guide.vue)

## Code Organization

- Keep component and composable boundaries clear.
- Keep implementation files at `300` lines or fewer.
- Prefer structures that align with the referenced style guide instead of inventing project-local conventions.
- Use `snake_case` for directory names and file names.
- Place examples under `./examples`.
