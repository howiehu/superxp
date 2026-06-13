---
name: using-superxp
description: "Explicit SuperXP entrypoint. Use only when the user invokes /using-superxp, $using-superxp, @superxp, explicitly asks to use SuperXP, or starts the user message with xp! in any letter case. Do not use for ordinary feature, bugfix, refactor, TDD, plan, spec, or XP mentions without an explicit SuperXP trigger."
---

# Using SuperXP

Use SuperXP only because the customer explicitly selected it.

Valid triggers:

- `/using-superxp`
- `$using-superxp`
- `@superxp`
- A direct request to use SuperXP.
- A user message that starts with `xp!`, case-insensitive.

Rules:

- Treat `xp!`, `XP!`, `Xp!`, and `xP!` at the start of the user message as the same trigger.
- Do not treat `xp!` in the middle of a message as a trigger.
- Do not activate SuperXP for ordinary requests that mention feature work, bug fixes, refactoring, TDD, plans, specs, or XP unless the customer explicitly selected SuperXP.
- Follow the XP Loop workflow from the bundled `xp-loop` skill: orient, clarify, slice, check, use Test First when appropriate, verify, and reflect.
- Keep the workflow as small as the task allows.
