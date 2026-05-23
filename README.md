# RIPER Workflow Skills

> A single `CLAUDE.md` for the RIPER methodology — Research, Innovate, Plan, Execute, Review. Five-phase systematic development for complex multi-step work.

## Why RIPER

Most coding mistakes happen at phase boundaries. You research a bit, plan a bit, code a bit, all mixed together. The result: plans that miss what research would have caught, code that drifts from the plan, reviews that find nothing because they're done at the same level of context as the writing.

RIPER enforces the boundaries:

- **Research** is read-only. No code changes. The output is understanding.
- **Innovate** is brainstorming. Still read-only. The output is 2-3 viable approaches.
- **Plan** is specification. Approval gate before Execute. The output is a measurable spec.
- **Execute** follows the plan sequentially. The output is working code.
- **Review** is verification. The output is signed-off code + retrospective.

Each phase has a different access mode. Each produces a different artifact. Each is harder to do badly when its constraints are explicit.

## The 5 phases at a glance

| Phase | Access | Output |
|---|---|---|
| Research | Read-only | `~/dev/[task]/research-notes.md` |
| Innovate | Read-only | `~/dev/[task]/approaches.md` |
| Plan | Write to docs | `~/dev/[task]/[task]-plan.md` |
| Execute | Full | Working code |
| Review | Read-only | `~/dev/[task]/review.md` |

Full content: [`CLAUDE.md`](CLAUDE.md). Worked task example: [`EXAMPLES.md`](EXAMPLES.md).

## Install

### As a project CLAUDE.md

```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/HermeticOrmus/riper-workflow-skills/main/CLAUDE.md
```

### As a Claude Code skill

The same content as an installable skill: [`skills/riper-workflow/`](skills/riper-workflow/).

### In Cursor

See [`CURSOR.md`](CURSOR.md). Rule at [`.cursor/rules/riper-workflow.mdc`](.cursor/rules/riper-workflow.mdc).

## When to use RIPER

- Architecture changes
- Multi-file refactors
- New features touching multiple subsystems
- Migrations (DB schema, framework upgrade, language upgrade)
- Anything where mistakes compound (auth, payments, data integrity)

## When NOT to use RIPER

- Typo fixes
- Single-file bug fixes with obvious cause
- Documentation updates
- Prototype exploration where the discipline cost exceeds the discovery value

The trap to avoid: applying RIPER to everything. The phase-separation overhead is real; it pays back on multi-day work, not on a quick fix.

## See also

- [`vibe-engineer-skills`](https://github.com/HermeticOrmus/vibe-engineer-skills) — how to direct AI codegen well
- [`andrej-karpathy-skills`](https://github.com/HermeticOrmus/andrej-karpathy-skills) — how Claude should behave when writing code
- [`six-day-cycle-skills`](https://github.com/HermeticOrmus/six-day-cycle-skills) — sister: sustainable shipping cadence
- [`magnum-opus-skills`](https://github.com/HermeticOrmus/magnum-opus-skills) — alchemy-stage workflow for project transformation

## License

MIT.
