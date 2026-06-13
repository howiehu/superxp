# SuperXP

[中文](README.zh-CN.md)

SuperXP is a lightweight workflow framework for agentic software development, shaped by Extreme Programming and Agile practice.

It aims to get useful workflow discipline with fewer rules, less prompt overhead, and faster feedback by relying more on agents and the underlying model capabilities.

## Background

SuperXP pays respect to [Superpowers](https://github.com/obra/superpowers). I have used Superpowers deeply in real work and created a lot of value with it.

At the same time, I realized that Superpowers is a key reason my work takes longer and consumes more tokens.

SuperXP is a rethinking of workflow from that experience.

## Principles

- Use the smallest process that works.
- Keep prompts, rules, and abstractions concise.
- Add constraints only after repeated evidence shows they are needed.
- Prefer working software, simple design, tests, and continuous improvement.
- Rely on agents and model capabilities before adding framework machinery.
- Design every practice for open source collaboration.

## v1 Plugin Preview

SuperXP v1 is a minimal Codex plugin preview centered on two skills:

- `using-superxp`: explicit entrypoint for choosing SuperXP.
- `xp-loop`: the core XP workflow.

The workflow is inspired by Extreme Programming:

```text
Orient -> Clarify -> Slice -> Check -> TDD Cycle -> Verify -> Reflect
```

The goal is not to remove discipline. The goal is to keep only the discipline that creates fast feedback, clear communication, simple design, small increments, and verifiable handoff.

### XP Constraints

- **Communication:** clarify goal, scope, acceptance, and handoff context.
- **Simplicity:** choose the smallest valuable increment that can work.
- **Feedback:** define the acceptance signal before changing work.
- **Test First:** use tests to drive code behavior toward simple design.
- **Courage:** stop when intent, scope, or verification is unclear.
- **Respect:** protect the customer's intent, the current workspace, existing behavior, and the next agent.

### Test First / TDD

TDD is the default coding discipline for testable code changes. It connects XP's Test First practice to simple design: write the next small failing test, implement the smallest code that passes, then refactor while tests stay green.

Use TDD for new behavior, reproducible bug fixes, risky refactors, public interfaces, business logic, state transitions, and data transformations. When strict TDD does not fit, agents must explain why before changing work and define substitute feedback such as build, type check, manual inspection, screenshot, log, review, or generated-output validation.

### Clarification

When intent, scope, trade-offs, or acceptance are unclear, agents should use their host environment's native question mechanism first.

Use divergent questions to discover options when the goal or success criteria are unclear. Use convergent questions to lock scope, approach, acceptance, or workflow decisions. Do not ask questions that repository inspection can answer.

When asking with options, agents should base each option on observed facts, explain the recommendation and trade-off for each option, and put the strongest overall recommendation first with a short reason.

### Spec and Plan

SuperXP separates session work from cross-session process documentation:

- **Plan** is session-local execution tracking. Use the host tool's native Plan Mode when work can finish in one conversation, needs progress tracking, or is urgent.
- **Spec** is lifecycle-bound process documentation for complex work that cannot finish reliably in one conversation and needs cross-session or cross-agent handoff.
- **Incident work** uses Plan Mode first: stabilize, mitigate, verify, then record the incident afterward.

Agents should prompt the customer to switch to native Plan Mode when the current conversation needs multi-step sequencing, agreement before execution, or user-visible progress tracking. When Plan Mode ends and execution begins, agents must create a TODO or checklist with the host tool and keep it updated during execution.

SuperXP does not create a default persistent plan artifact.

### Documentation Structure

SuperXP keeps documentation AI-first and YAGNI-friendly:

- `docs/AGENTS.md` defines documentation governance for agents.
- `docs/templates/` contains reusable templates.
- `docs/decisions/` stores durable MADR-style ADRs.
- `docs/incidents/` stores durable blameless incident records.
- `docs/specs/active/` stores active cross-session Specs.
- `docs/specs/archive/` stores historical Specs only when temporary retention is useful.

Spec process documents use:

```text
Epic -> Feature -> Story -> Scenario -> Task
```

Implementation order comes from User Story Mapping:

```text
Backbone -> Walking Skeleton -> Release Slices
```

Code, tests, and scoped `AGENTS.md` files remain the highest-authority living documentation. Completed Specs should be archived or deleted after lasting knowledge moves into code, tests, scoped `AGENTS.md`, ADRs, or incident records.

### Worktrees and Subagents

Worktrees and subagents are first-class agent engineering practices.

Use worktree isolation when it protects the workspace, enables rollback, supports parallel experiments, or keeps the commit chain clean.

Use subagents when parallel investigation, independent review, role separation, or context isolation reduces risk or shortens feedback time.

## Local Installation

Install the repo marketplace from the repository root:

```bash
codex plugin marketplace add .
```

Then restart Codex or start a new thread, open the plugin directory, choose `SuperXP Local`, and install `superxp`.

## Usage

SuperXP does not use hooks and should not run for every conversation. Use it only when you explicitly choose it:

- `/using-superxp`
- `$using-superxp`
- `$xp-loop`
- Start the user message with `xp!`, case-insensitive, for example `xp! help me slice this change`.

Ordinary requests such as `fix this bug`, `use TDD`, or `make a plan` should not activate SuperXP unless you explicitly choose SuperXP.

## Status

SuperXP is in its initialization stage. The current focus is making the v1 Codex plugin preview small enough to try and concrete enough to evaluate.

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) before opening issues or pull requests.

## License

This project is licensed under the terms in [LICENSE](LICENSE).
