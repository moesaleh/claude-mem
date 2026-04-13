```markdown
# claude-mem Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill covers the core development patterns, coding conventions, and release workflows for the `claude-mem` repository. The project is a TypeScript codebase using React, with a focus on modular plugin architecture and rigorous versioning. You'll learn how to contribute code, manage releases, update documentation, and write tests in a way that aligns with the project's established practices.

## Coding Conventions

- **File Naming:** Use camelCase for all file names.
  - Example: `memoryStore.ts`, `userSessionManager.ts`
- **Import Style:** Use relative imports.
  - Example:
    ```typescript
    import { getMemory } from './memoryStore';
    ```
- **Export Style:** Use named exports.
  - Example:
    ```typescript
    // Good
    export function getMemory() { ... }

    // Avoid default exports
    // export default function getMemory() { ... }
    ```
- **Commit Messages:** Follow [Conventional Commits](https://www.conventionalcommits.org/) with these prefixes:
  - `fix:`, `chore:`, `docs:`, `feat:`, `maestro:`
  - Example: `feat: add persistent memory store for sessions`

## Workflows

### Release Version Bump
**Trigger:** When preparing a new release version.  
**Command:** `/bump-version`

1. Update version numbers in `package.json` and `plugin/package.json`.
2. Update `.claude-plugin/marketplace.json` and `plugin/.claude-plugin/plugin.json`.
3. Rebuild `plugin/scripts/mcp-server.cjs` and `plugin/scripts/worker-service.cjs`.
4. Optionally update `plugin/ui/viewer-bundle.js`.
5. Commit all changes with a conventional commit message.

**Example:**
```bash
# Update versions
vim package.json
vim plugin/package.json
vim .claude-plugin/marketplace.json
vim plugin/.claude-plugin/plugin.json

# Rebuild bundles
npm run build:plugin-scripts
npm run build:viewer-bundle

# Commit
git add .
git commit -m "chore: bump version to vX.Y.Z"
```

### Update Changelog for Release
**Trigger:** When a new version is released or about to be released.  
**Command:** `/update-changelog`

1. Edit `CHANGELOG.md` to add a new section for the release version.
2. Summarize notable changes, bugfixes, and features.
3. Commit the updated changelog.

**Example:**
```markdown
## [1.2.0] - 2024-06-01
### Added
- Persistent memory store for sessions

### Fixed
- Session timeout bug
```

### Feature or Bugfix with Bundle Rebuild
**Trigger:** When a code change in `src/` or `plugin/scripts/` requires updated runtime bundles.  
**Command:** `/feature-with-bundle`

1. Edit or add implementation files in `src/` or `plugin/scripts/`.
2. Update or add tests in `tests/`.
3. Rebuild `plugin/scripts/mcp-server.cjs` and/or `plugin/scripts/worker-service.cjs`.
4. Optionally rebuild `plugin/ui/viewer-bundle.js`.
5. Commit all changes with an appropriate message.

**Example:**
```bash
# Edit code
vim src/memoryStore.ts

# Add tests
vim tests/memoryStore.test.ts

# Rebuild
npm run build:plugin-scripts

# Commit
git add .
git commit -m "feat: add memory expiration logic"
```

### Add or Update Tests for Bugfix or Feature
**Trigger:** When a new feature is added or a bug is fixed.  
**Command:** `/add-tests`

1. Edit or add implementation files in `src/` or `plugin/scripts/`.
2. Create or update corresponding test files in `tests/`.
3. Commit the tests and implementation together.

**Example:**
```typescript
// tests/memoryStore.test.ts
import { getMemory } from '../src/memoryStore';

test('retrieves memory for session', () => {
  expect(getMemory('session1')).toBeDefined();
});
```

### Readme or Documentation Update
**Trigger:** When documentation or project information needs to be updated.  
**Command:** `/update-docs`

1. Edit `README.md` or `docs/public/*.mdx` to reflect new information.
2. Commit documentation changes.

**Example:**
```bash
vim README.md
git add README.md
git commit -m "docs: update usage example for new API"
```

## Testing Patterns

- **Framework:** [Jest](https://jestjs.io/)
- **Test File Pattern:** All test files are named with the `.test.ts` suffix and placed in the `tests/` directory.
  - Example: `tests/memoryStore.test.ts`
- **Test Example:**
    ```typescript
    import { getMemory } from '../src/memoryStore';

    describe('getMemory', () => {
      it('returns memory for valid session', () => {
        expect(getMemory('session1')).toEqual(expect.any(Object));
      });
    });
    ```

## Commands

| Command             | Purpose                                                        |
|---------------------|----------------------------------------------------------------|
| /bump-version       | Bump project and plugin versions for a new release             |
| /update-changelog   | Update `CHANGELOG.md` for a new release                       |
| /feature-with-bundle| Implement feature/bugfix and rebuild runtime bundles           |
| /add-tests          | Add or update tests for new features or bugfixes               |
| /update-docs        | Update `README.md` or documentation files                      |
```