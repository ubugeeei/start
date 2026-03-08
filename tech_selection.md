# AI Project Technology Selection Guide

This directory contains the default technology choices and engineering rules for new projects created by AI agents.

## Stacks

- [TypeScript](./typescript.md)
- [Rust](./rust.md)
- [Vue](./vue.md)

## Development Environment

- Use `mise` for environment setup.
- Make `mise run dev` start the full development environment in one command.
- Standardize common project tasks behind `mise` instead of ad-hoc shell commands.
- Make `mise run fmt` run repository formatting workflows in one command.
- Make `mise run lint` run JS, TS, and Rust lint workflows in one command.
- Make `mise run check` run JS, TS, and Rust check workflows in one command.
- Make `mise run test` run JS, TS, and Rust test workflows in one command.

## Release Workflow

- Use `mise run release patch` for patch releases.
- Use `mise run release minor` for minor releases.
- Use `mise run release alpha` for alpha releases.
- Use `mise run release beta` for beta releases.
- Make each release command update the version and create the corresponding Git tag.

## CI and Release Automation

- Set up CI with GitHub Actions.
- Run release workflows from tag pushes.
- Do not store registry tokens in GitHub Actions.
- Use trusted publishing for package publishing.

## Repository Layout

- Place examples under `./examples`.

## General Principle

When an AI agent creates a new project, optimize for:

- predictable tooling
- minimal incidental complexity
- strong static guarantees
- small, separable modules
- low allocation overhead where performance matters
- conventions that are easy for both humans and agents to follow
