# AGENTS.md

## Core Constraint

- YAGNI is a core principle: keep every future change to the smallest necessary increment.
- Do not use Superpowers in this project.

## Project

SuperXP is a lightweight workflow framework shaped by Extreme Programming and Agile practice.

Its goal is to achieve effective agent workflows by relying more on Agents and model capabilities, with minimal constraints, minimal prompt overhead, and fast feedback.

## Principles

- Use the smallest process that works.
- Keep prompts, rules, and abstractions concise.
- Add constraints only when repeated evidence shows they are needed.
- Prefer working software, simple design, tests, and continuous improvement.
- Keep all practices aligned with the realities and constraints of an open source project.

## Constraints

- Favor practices that are easy to inspect, discuss, fork, and improve.
- Keep contribution paths small and trade-offs visible.
- Keep `README.md` and `README.zh-CN.md` structurally and semantically aligned.
- Update both README files in the same change whenever either one changes.

## Branches

- Use `main` for releases.
- Use `dev` for daily maintenance and development.
- Target non-release changes at `dev` by default.
- Do not create a stable GitHub Release from `dev`.
- Stable releases must be tagged from `main` after the release commit is present on `main`.
- Development builds and preview installation instructions must point to `dev`.
- Stable installation instructions must point to `main`.
- If a release is accidentally created from the wrong branch, do not move the published tag by default; publish a corrective patch release from `main` instead.

## Contributions

- Keep issue and pull request entry points structured.
- Require clear problem statements, scope, and verification evidence before deep review.
- Treat low-signal or unverifiable submissions as triage work, not implementation work.

## Commits

- Use Commitizen-style Conventional Commits: `<type>(<scope>): <subject>`.
- Prefer these types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`.
- Keep subjects imperative, concise, and useful for release notes.
