# AGENTS.md

## Purpose

This directory is an AI-first documentation workspace. Documents here primarily guide AI agents; humans review, correct, and maintain them.

## Authority

- Code, tests, and current scoped `AGENTS.md` files are the highest-authority living documentation.
- ADRs and incident records are durable historical records.
- Spec documents are lifecycle-bound process documents for cross-session complex work.
- Archived specs are historical context only. Verify them against current code, tests, and scoped `AGENTS.md` before using them.

## Plan vs Spec

- Use the host agent's Plan Mode for work that can finish in one conversation.
- Use Plan Mode first for urgent incident handling. Restore, mitigate, verify, then record the incident afterward.
- Create a spec only when the work cannot be completed reliably in one conversation and needs cross-session, cross-agent, or multi-person handoff.

## Templates

- Use `docs/templates/adr.madr.md` for major decisions.
- Use `docs/templates/incident.md` for incident records.
- Use `docs/templates/epic.md` and `docs/templates/story-map.md` to start a cross-session spec.
- Use the Feature, User Story, Scenario, and Task templates only when the work needs that level of decomposition.

## Lifecycle

- Active specs live under `docs/specs/active/EPIC-YYYYMMDD-short-name/`.
- Completed specs must be archived or deleted after lasting knowledge is moved into code, tests, scoped `AGENTS.md`, ADRs, or incident records.
- Do not keep process documents as permanent execution authority.

