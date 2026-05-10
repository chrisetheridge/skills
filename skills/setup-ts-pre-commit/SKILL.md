 ---
name: setup-pre-commit-biome
description: Set up Husky pre-commit hooks with lint-staged using Biome, plus type checking and tests. Use when user wants to add pre-commit hooks, set up Husky, configure lint-staged, or add commit-time
---

# Setup Pre-Commit Hooks with Biome

## What This Sets Up

- **Husky** pre-commit hook
- **lint-staged** running **Biome** on staged files
- **typecheck** and **test** scripts in the pre-commit hook, if present
- **Biome config** if missing

Do not add Prettier. Biome owns formatting and linting.

## Steps

### 1. Detect package manager

Check for lockfiles:

- `pnpm-lock.yaml` → `pnpm`
- `package-lock.json` → `npm`
- `yarn.lock` → `yarn`
- `bun.lockb` → `bun`

Use whichever is present. Default to `npm` if unclear.

Command equivalents:

| Package manager | Add dev deps | Run binary |
|---|---|---|
| npm | `npm install -D ...` | `npx ...` |
| pnpm | `pnpm add -D ...` | `pnpm exec ...` |
| yarn | `yarn add -D ...` | `yarn ...` |
| bun | `bun add -d ...` | `bunx ...` |

### 2. Inspect existing scripts

Read `package.json`.

Look for:

- `lint`
- `format`
- `typecheck`
- `test`

Prefer existing scripts over inventing new ones.

If the repo already has a CI script such as `check`, `check:ci`, or `ci`, note what it runs. Do not blindly put the whole CI command in pre-commit if it includes slow builds or integration tests.

### 3. Install dependencies

Install as devDependencies:

```sh
husky lint-staged @biomejs/biome
```

Skip @biomejs/biome if already installed.

### 4. Initialize Husky

Use the detected package manager:

```sh
  npx husky init
```

or:

```sh
  pnpm exec husky init
```

or equivalent.

This creates .husky/ and usually adds this script to package.json:

```json
  {
    "scripts": {
      "prepare": "husky"
    }
  }
```

If prepare already exists, preserve existing behavior and append Husky safely, for example:

```json
  {
    "scripts": {
      "prepare": "husky"
    }
  }
```

If unsure, ask before overwriting a non-Husky prepare script.

### 5. Create .husky/pre-commit

Write this file. No shebang needed for Husky v9+.

For pnpm:

```sh
  pnpm exec lint-staged
  pnpm typecheck
  pnpm test
```

Adapt commands for the detected package manager.

Rules:

- Include typecheck only if package.json has a typecheck script.
- Include test only if package.json has a test script.
- If either script is missing, omit it and tell the user.
- Do not run build by default. CI should usually own build verification.

Examples:

npm:

```sh
  npx lint-staged
  npm run typecheck
  npm run test
```

pnpm:

```sh
  pnpm exec lint-staged
  pnpm typecheck
  pnpm test
```

yarn:

```sh
  yarn lint-staged
  yarn typecheck
  yarn test
```

bun:

```sh
  bunx lint-staged
  bun run typecheck
  bun run test
```

### 6. Create lint-staged config

Prefer .lintstagedrc.json.

Use Biome, not Prettier:

```json
  {
    "*.{js,jsx,ts,tsx,json,jsonc,css,graphql,md,mdx,yml,yaml}": "biome check --write --no-errors-on-unmatched"
  }
```

If the repo’s biome.json restricts included files, align the lint-staged globs with that config.

If the repo has unsupported file types, remove them from the glob.

### 7. Create biome.json if missing

Only create this file if no Biome config exists.

Use:

```json
  {
    "$schema": "https://biomejs.dev/schemas/2.0.0/schema.json",
    "formatter": {
      "enabled": true,
      "indentStyle": "space",
      "indentWidth": 2,
      "lineWidth": 100
    },
    "javascript": {
      "formatter": {
        "semicolons": "always",
        "quoteStyle": "double"
      }
    },
    "linter": {
      "enabled": true,
      "rules": {
        "recommended": true
      }
    }
  }
```

If the project already has formatting conventions, match them instead of using these defaults.

### 8. Ensure package scripts exist

If missing, add only scripts that make sense for the repo.

Common defaults:

```json
  {
    "scripts": {
      "format": "biome format --write .",
      "format:check": "biome format .",
      "lint": "biome check ."
    }
  }
```

Do not add typecheck unless TypeScript is configured.

Do not add test unless the test runner is already installed or the user asked to set one up.

### 9. Verify

Check:

- .husky/pre-commit exists
- .husky/pre-commit is executable
- .lintstagedrc.json exists
- prepare script in package.json runs husky
- biome.json exists or the repo already had Biome config
- package.json contains needed devDependencies

Run:

```sh
  npx lint-staged
```

or package-manager equivalent.

Then run any hook commands directly:

```sh
  npm run typecheck
  npm run test
```

Adapt for package manager.

### 10. Commit

Stage changed files and commit:

```sh
  git add package.json package-lock.json pnpm-lock.yaml yarn.lock bun.lockb biome.json .lintstagedrc.json .husky/pre-commit
  git commit -m "Add pre-commit hooks with Husky and Biome"
```

Only stage lockfiles that exist and changed.

The commit should trigger the hook. If it fails, fix the reported issue and retry.

Notes

- Husky runs Git hooks.
- lint-staged limits formatting/linting to staged files.
- Biome owns formatting and linting.
- CI remains the source of truth.
- Keep pre-commit fast. Avoid full builds unless the user explicitly wants slower commits.