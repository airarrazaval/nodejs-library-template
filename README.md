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
- **API documentation** generation with [TypeDoc](https://typedoc.org) and TSDoc comments
- **CI/CD** via GitHub Actions: automated checks on PRs and tag-triggered npm publishing with SLSA provenance

## Getting Started

1. Click **Use this template** on GitHub to create a new repository.
2. Clone your new repo and install dependencies:

   ```sh
   npm install
   ```

3. Replace the contents of [src/index.ts](src/index.ts) with your library code.
4. Update `name`, `version`, and `description` in [package.json](package.json).
5. Update the `exports` field in [package.json](package.json) if you need multiple entry points.
6. Update the comparison links at the bottom of [CHANGELOG.md](CHANGELOG.md) to point to your repository.

## Project Structure

```
src/           # Library source code
tests/         # Test files (*.test.ts)
dist/          # Compiled output (generated, not committed)
tsconfig.json          # TypeScript config for type-checking
tsconfig.build.json    # TypeScript config for compilation
```

## Scripts

| Command                 | Description                                                    |
| ----------------------- | -------------------------------------------------------------- |
| `npm run dev`           | Run tests in watch mode                                        |
| `npm run build`         | Compile TypeScript to `dist/`                                  |
| `npm test`              | Run tests                                                      |
| `npm run test:coverage` | Run tests with coverage report                                 |
| `npm run typecheck`     | Type-check without emitting files                              |
| `npm run lint`          | Lint source and tests                                          |
| `npm run lint:fix`      | Lint and auto-fix issues                                       |
| `npm run format`        | Format all files                                               |
| `npm run format:check`  | Check formatting without modifying files                       |
| `npm run clean`         | Remove `dist/` and `docs/`                                     |
| `npm run docs`          | Generate API documentation in `docs/`                          |
| `npm run changelog`     | Regenerate `CHANGELOG.md` from commits (used before releasing) |

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

Only `dist/`, `README.md`, `CHANGELOG.md`, and `LICENSE` are included in the published package (see `files` in [package.json](package.json)).

## GitHub Actions

### CI (`ci.yml`)

Runs on every pull request and push to `main`:

1. Typecheck
2. Lint
3. Test
4. Build

### Publish (`publish.yml`)

Runs when a version tag is pushed (e.g. `v1.2.3`):

1. Runs `prepublishOnly` (typecheck → lint → clean → build)
2. Publishes to npm with [SLSA provenance attestation](https://docs.npmjs.com/generating-provenance-statements)

**Required setup:** add an `NPM_TOKEN` secret to your repository under **Settings → Secrets and variables → Actions**.

To publish a new version:

```sh
# 1. Regenerate CHANGELOG.md from commits (determines next version automatically)
npm run changelog

# 2. Review CHANGELOG.md, then commit
git add CHANGELOG.md && git commit -m "chore: release vX.Y.Z"

# 3. Bump version to match what git-cliff determined
npm version patch  # or minor / major

# 4. Push commit and tag — publish workflow triggers automatically
git push --follow-tags
```

## Requirements

- Node.js >= 24.0.0
