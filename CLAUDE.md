# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

A **skills/prompt library** for AI-assisted Node.js development. The primary deliverables are Markdown files under `skills/`, not compiled code. `src/index.ts` is a one-liner that exports `version` only.

## Commands

```bash
npm install          # install dependencies
npm run typecheck    # TypeScript check (noEmit — no build output is generated)
npm run lint         # ESLint
npm test             # run all tests via `node --test`
node --test path/to/file.test.ts                    # run a single test file
node --test --test-name-pattern "pattern"           # run tests by name
```

## Architecture

Each skill lives at `skills/<skill-name>/`:
- `SKILL.md` — the entrypoint (YAML frontmatter with `name`/`description`/`metadata.tags`, when-to-use, links to rules)
- `rules/*.md` — detailed rule documents, each referenced explicitly from `SKILL.md`

Current skills: `documentation`, `fastify`, `init`, `linting-neostandard-eslint9`, `node`, `nodejs-core`, `oauth`, `octocat`, `snipgrapher`, `typescript-magician`.

TypeScript config (`tsconfig.json`) includes both `src/` and `skills/` so `.ts` files inside skill `rules/assets/` are type-checked.

## Key editing rules

1. **Every `rules/*.md` must be explicitly linked from its skill's `SKILL.md`.** Adding, renaming, or removing a rule file requires updating `SKILL.md` links in the same change.
2. **Preserve YAML frontmatter** (`name`, `description`, `metadata.tags`) in all `SKILL.md` and `rules/*.md` files.
3. **New guidance** goes under an existing skill's `rules/` unless creating an entirely new skill.
4. Run `npm run typecheck` and `npm test` after any substantial edits.

## Tooling notes

- `.githuman/` directory is intentionally gitignored project tooling state — do not modify or commit it.
- `.claude/settings.local.json` permits `npx githuman:*` commands for Claude-specific workflows.
