# Node.js Library Template

A minimal, opinionated template for publishing Node.js libraries written in TypeScript.

## Features

- **TypeScript** with strict settings and `NodeNext` module resolution
- **ESM-only** output (`"type": "module"`)
- **Node.js 24+** target
- **Testing** via Node.js built-in test runner (`node:test`) with [tsx](https://github.com/privatenumber/tsx) for TypeScript support
- **Linting** with [oxlint](https://oxc.rs/docs/guide/usage/linter)
- **Formatting** with [oxfmt](https://github.com/nicolo-ribaudo/oxfmt)
- **Type declarations** and source maps included in the build output

## Getting Started

1. Click **Use this template** on GitHub to create a new repository.
2. Clone your new repo and install dependencies:

```sh
npm install
```

3. Replace the contents of [src/index.ts](src/index.ts) with your library code.
4. Update `name`, `version`, and `description` in [package.json](package.json).
5. Update the `exports` field in [package.json](package.json) if you need multiple entry points.

## Project Structure

```
src/           # Library source code
tests/         # Test files (*.test.ts)
dist/          # Compiled output (generated, not committed)
tsconfig.json          # TypeScript config for type-checking
tsconfig.build.json    # TypeScript config for compilation
```

## Scripts

| Command | Description |
|---|---|
| `npm run build` | Compile TypeScript to `dist/` |
| `npm test` | Run tests |
| `npm run test:coverage` | Run tests with coverage report |
| `npm run typecheck` | Type-check without emitting files |
| `npm run lint` | Lint source and tests |
| `npm run lint:fix` | Lint and auto-fix issues |
| `npm run format` | Format all files |
| `npm run format:check` | Check formatting without modifying files |
| `npm run clean` | Remove `dist/` |

## Publishing

Before publishing, the `prepublishOnly` script runs automatically:

```sh
npm publish
```

This will:
1. Type-check
2. Lint
3. Clean `dist/`
4. Build

Only the `dist/` folder and `README.md` are included in the published package (see `files` in [package.json](package.json)).

## Requirements

- Node.js >= 24.0.0
