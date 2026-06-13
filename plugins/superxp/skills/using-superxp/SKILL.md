---
name: using-superxp
description: "Explicit SuperXP entrypoint. Use only when the user invokes /using-superxp, /skill:using-superxp, $using-superxp, @superxp, explicitly asks to use SuperXP, or starts the user message with xp! in any letter case. Do not use for ordinary feature, bugfix, refactor, TDD, plan, spec, or XP mentions without an explicit SuperXP trigger."
---

# Using SuperXP

Use SuperXP only because the customer explicitly selected it.

Valid triggers:

- `/using-superxp`
- `/skill:using-superxp`
- `$using-superxp`
- `@superxp`
- A direct request to use SuperXP.
- A user message that starts with `xp!`, case-insensitive.

Rules:

- Allow implicit invocation only to recognize the explicit `xp!` start-of-message keyword and direct SuperXP selection phrases.
- Treat `xp!`, `XP!`, `Xp!`, and `xP!` at the start of the user message as the same trigger.
- Do not treat `xp!` in the middle of a message as a trigger.
- Do not activate SuperXP for ordinary requests that mention feature work, bug fixes, refactoring, TDD, plans, specs, or XP unless the customer explicitly selected SuperXP.
- Do not mix SuperXP with another third-party workflow system. Once SuperXP is selected, do not use Superpowers, OpenSpec, or any other competing third-party workflow unless the customer explicitly cancels SuperXP first.
- This does not forbid the host agent's native or official non-workflow capabilities, such as Plan Mode, TODO/checklist tracking, built-in review tools, official verification tools, or official non-workflow skills, when they are used to execute SuperXP rather than replace it.
- Superpowers, OpenSpec, or other third-party workflows must not replace or run alongside SuperXP, even if they are installed, bundled, curated, or presented as available capabilities.
- Follow the XP Loop workflow from the bundled `xp-loop` skill: orient, clarify, slice, check, use Test First when appropriate, verify, and reflect.
- Keep the workflow as small as the task allows.
