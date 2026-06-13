---
name: xp-loop
description: "Core SuperXP workflow. Use only after the user explicitly invokes $xp-loop, selects using-superxp, explicitly asks to use SuperXP, or starts the user message with xp! in any letter case. Do not use for ordinary feature, bugfix, refactor, TDD, plan, spec, or XP mentions without an explicit SuperXP trigger."
---

# XP Loop

Use the smallest workflow that preserves Extreme Programming discipline.

Activation rules:

- Treat `xp!`, `XP!`, `Xp!`, and `xP!` at the start of the user message as the same explicit trigger.
- Do not treat `xp!` in the middle of a message as a trigger.
- Do not activate SuperXP for ordinary requests that mention feature work, bug fixes, refactoring, TDD, plans, specs, or XP unless the customer explicitly selected SuperXP.
- If SuperXP was not explicitly triggered, use the host agent's normal workflow instead.

Core loop:

```text
Orient -> Clarify -> Slice -> Check -> TDD Cycle -> Verify -> Reflect
```

## XP Grounding

- **Communication:** Make the goal, scope, acceptance, and handoff context explicit.
- **Simplicity:** Choose the smallest valuable increment that can work.
- **Feedback:** Define the acceptance signal before changing work.
- **Test First:** Use tests to drive code behavior toward simple design.
- **Courage:** Stop when intent, scope, or verification is unclear.
- **Respect:** Protect the customer's intent, the current workspace, existing behavior, and the next agent.

## Workflow

1. **Orient** - Inspect the request and local context before asking questions that the repository can answer.
2. **Clarify** - If intent, scope, trade-offs, or acceptance are unclear, use the host agent's native question tool first. Plain conversation is the fallback.
3. **Slice** - Select the smallest valuable increment. State what is out of scope when scope can grow.
4. **Check** - Define the feedback method before changing work. For code behavior changes, prefer a test.
5. **TDD Cycle** - For testable code changes, use `Red -> Green -> Refactor`. For non-code or non-testable work, use the defined substitute feedback.
6. **Verify** - Run or inspect the chosen check. Do not claim completion without evidence.
7. **Reflect** - Report what changed, what was verified, and what risk or follow-up remains.

## Test First / TDD

TDD is the default coding discipline for testable code changes. It is not only a verification technique; in SuperXP, TDD is the coding path to simple design.

Use TDD for:

- New user-visible behavior.
- Reproducible bug fixes.
- Business logic, public interfaces, state transitions, or data transformations.
- Refactoring with behavior risk.

Cycle:

- **Red:** Express the next small behavior with a failing test or locate an existing failing test.
- **Green:** Write the smallest implementation that makes the test pass.
- **Refactor:** Improve design while keeping tests green.

Rules:

- For a bug fix, reproduce the failure before changing production code.
- For a refactor, confirm existing protective tests or add a characterization check before changing structure.
- Keep each TDD cycle small. Do not write broad production changes before feedback exists.
- If strict TDD does not fit, state why before changing work and define substitute feedback.

Strict TDD may not fit pure docs, comments, formatting, metadata changes, exploratory spikes, early setup without a test framework, generated outputs, visual checks, external system checks, or operations work. Substitute feedback can be a build, type check, manual inspection, screenshot, log, review, generated-output validation, or another observable signal.

## Clarification

Ask only when the answer cannot be discovered locally or when the question changes the customer's intent, scope, trade-off, acceptance, or workflow.

Use divergent questions when discovering options:

- The customer goal is unclear.
- Multiple valuable directions exist.
- Success criteria are not known.
- Product, design, or technical trade-offs are hidden.

Use convergent questions when locking decisions:

- Confirm scope.
- Choose one approach.
- Define acceptance.
- Decide whether a persistent Spec is needed.
- Decide whether to use worktree isolation, subagents, or stronger verification.

Rules:

- Prefer the host agent's native question mechanism.
- Do not ask questions that repository inspection can answer.
- Ask one focused question or a small set of meaningful options.
- Base options on observed facts, known constraints, and the current task goal.
- Explain the practical recommendation for each option, including the main trade-off.
- Put the strongest overall recommendation first and label why it is recommended.
- Stop diverging once a clear direction exists.

## Plan vs Spec

Choose by time horizon, urgency, and handoff need.

Use Plan Mode when:

- The work can finish in the current conversation.
- The work is urgent and needs fast stabilization or recovery.
- The work needs session-local ordering, agreement, progress tracking, or acceptance.
- A TODO/checklist can reliably track the work in the current conversation.

Create a Spec only when:

- The work cannot be completed reliably in one conversation.
- The work needs cross-session, cross-agent, or multi-person handoff.
- The work needs Epic, Feature, Story, Scenario, and Task decomposition.
- Implementation order needs a User Story Map.
- Without process documentation, future agents would lose context or drift.

Do not create a heavy Spec for one-session work. Do not use a Spec as a replacement for Plan Mode.

## Spec

A Spec is a lifecycle-bound process documentation system, not a single permanent truth document. It helps agents decompose and order cross-session complex work.

Spec hierarchy:

```text
Epic -> Feature -> Story -> Scenario -> Task
```

Each active Epic lives under:

```text
docs/specs/active/EPIC-YYYYMMDD-short-name/
```

Required Epic files:

- `epic.md` - Goal, context, scope, definition of done, lifecycle, and handoff notes.
- `story-map.md` - Backbone, walking skeleton, release slices, deferred scope, and ordering notes.
- `features/` - Feature documents.
- `stories/` - User Story documents.
- `scenarios/` - Given/When/Then scenarios.
- `tasks/` - Small executable tasks with TDD or substitute feedback.

Read `docs/AGENTS.md` before creating or modifying files under `docs/`.

Use `docs/templates/` when creating docs:

- `adr.madr.md` for major decisions.
- `incident.md` for post-incident records.
- `epic.md` and `story-map.md` to start a cross-session Spec.
- `feature.md`, `user-story.md`, `scenario.md`, and `task.md` for deeper decomposition.

Story Map rules:

- Establish the Backbone first.
- Implement the Walking Skeleton before later slices.
- Use Release Slices to order incremental delivery.
- Map each Story to at least one Scenario.
- Map each Scenario to a test or manual verification.
- Ensure each Task supports a Story/Scenario and names TDD or substitute feedback.

Lifecycle rules:

- Code, tests, and current scoped `AGENTS.md` files are the highest-authority living documentation.
- ADRs and incident records are durable historical records.
- Specs guide active Epic work only.
- When an Epic completes, migrate lasting knowledge into code, tests, scoped `AGENTS.md`, ADRs, or incident records, then archive or delete the process docs.
- Archived Specs are historical context only. Verify them against current code, tests, and scoped `AGENTS.md` before using them.

## Plan

A Plan is session-local execution tracking. Use the host agent's native Plan Mode or planning tool when the current conversation needs sequencing, progress tracking, or coordination.

SuperXP does not create a default persistent plan artifact.

Prompt the customer to switch to Plan Mode when:

- The next work has multiple dependent steps.
- Scope, acceptance, or sequencing needs agreement before execution.
- The work needs customer-visible tracking during the current conversation.
- Execution should not begin until the approach is decision-complete.

When using a native plan, constrain it with XP:

- Each step represents a small increment.
- Each step has a completion condition.
- Important steps have a feedback check.
- Testable code steps follow TDD order: failing test, confirm failure, minimal implementation, confirm pass, refactor if needed.
- The plan reduces risk and uncertainty first.
- The plan changes when feedback shows it should change.

A plan should include:

- **Goal:** What this conversation should complete.
- **Slice:** The smallest valuable increment.
- **Steps:** A short ordered set of actions.
- **Checks:** Verification for key steps.
- **Stop Conditions:** When to pause for the customer, such as unclear acceptance, expanding scope, repeated verification failure, or the need for a persistent Spec.

When Plan Mode ends and execution begins, create an execution tracker with the host agent's TODO or checklist tool before making changes. The tracker must mirror the approved plan at the current useful granularity and be updated as work progresses.

Do not turn activity lists into plans. Do not run long autonomous work without feedback points. Do not execute a multi-step plan without TODO/checklist tracking. Do not skip TDD for testable code unless you name the reason and substitute feedback. Do not write Plan Mode output into the repository unless the customer explicitly asks.

## Incident Work

Incident work uses the shortest reliable Plan flow first:

```text
Detect -> Stabilize -> Diagnose -> Fix / Mitigate -> Verify -> Record
```

During urgent incident handling:

- Use Plan Mode or TODO/checklist tracking.
- Stabilize, mitigate, and verify before writing heavy documentation.
- Preserve key evidence while moving quickly.
- Bind each step to fast feedback such as logs, health checks, tests, monitoring, or user-visible recovery.
- After stabilization, write an incident record under `docs/incidents/` using `docs/templates/incident.md`.

Incident records are durable, blameless records. Focus on systems, process, information conditions, and verifiable follow-up actions.

## Worktrees and Subagents

Use worktree isolation when it protects the workspace, enables rollback, supports parallel experiments, or keeps the commit chain clean.

Use subagents when they reduce risk or latency through parallel investigation, independent review, role separation, or context isolation.

Worktrees and subagents are first-class agent engineering practices. Use them when they serve feedback, isolation, or acceptance. Do not use them only because a ritual says to.

## Completion Gate

Before saying work is complete:

1. Identify the claim.
2. Identify the evidence required for that claim.
3. Run or inspect the evidence.
4. Report the actual result.

If verification was impossible, say what was not verified and why.
