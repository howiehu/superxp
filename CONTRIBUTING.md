# Contributing

SuperXP welcomes focused contributions that are easy to review and maintain.

## Before Opening an Issue

- Check whether the problem is already reported.
- Use the matching issue form.
- Include enough context for maintainers to reproduce, evaluate, or discuss the request.

## Before Opening a Pull Request

- Prefer opening or joining an accepted issue before making non-trivial changes.
- Keep the pull request small and focused.
- Explain the problem, the change, and the verification performed.
- Disclose AI-assisted work and describe the human review performed.

## Branches

- `main` is for releases.
- `dev` is for daily maintenance and development.
- Target regular pull requests at `dev`.
- Project administrators may push maintainer-owned changes directly to `dev` after local verification.

## Commits

Use Commitizen-style Conventional Commits:

```text
<type>(<scope>): <subject>
```

Common types:

- `feat`: user-facing feature
- `fix`: bug fix
- `docs`: documentation
- `refactor`: behavior-preserving code change
- `test`: tests
- `chore`: maintenance
- `ci`: continuous integration

Good commit subjects are concise, imperative, and useful for release notes.
