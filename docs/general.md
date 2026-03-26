# AI Project Technology Selection Guide

This directory contains the default technology choices and engineering rules for new projects created by AI agents.

## Stacks

- [TypeScript](./typescript.md)
- [Rust](./rust.md)
- [Vue](./vue.md)

## Development Environment

- Use a single shared task entry point instead of ad-hoc shell commands.
- For TypeScript projects, use `Vite+` with `vite-task` and run tasks through `vp`.
- For Rust projects, use `nix` flakes for the toolchain. Enter the environment with `nix develop` and expose shared tasks through `Vite Task` with `vp run`.
- Make the stack entry point start the full development environment in one command.
- For CLI tools, expose the executable through the shared task entry point.
- Make formatting, lint, check, and test workflows available from the shared task entry point.

## Release Workflow

- Provide a single-command workflow for patch releases.
- Provide a single-command workflow for minor releases.
- Provide a single-command workflow for alpha releases.
- Provide a single-command workflow for beta releases.
- Make each release command update the version and create the corresponding Git tag.

## CI and Release Automation

- Set up CI with GitHub Actions.
- Run release workflows from tag pushes.
- Do not store registry tokens in GitHub Actions.
- Use trusted publishing for package publishing.

## Repository Layout

- Place examples under `./examples`.
- Place TypeScript packages under `./packages`.
- Place Rust crates under `./crates`.
- Use workspace features instead of ad-hoc multi-package layouts.

## General Principle

When an AI agent creates a new project, optimize for:

- predictable tooling
- minimal incidental complexity
- strong static guarantees
- small, separable modules
- low allocation overhead where performance matters
- conventions that are easy for both humans and agents to follow
