<p align="center">
  <img src="https://ormus.solutions/mascot/chain_braces_to_swan.gif" alt="RIPER Workflow Skills" width="128" style="image-rendering: pixelated;" />
</p>

<h1 align="center">RIPER Workflow Skills</h1>

<p align="center">
  <em>A CLAUDE.md for the RIPER methodology — Research, Innovate, Plan, Execute, Review. Five-phase systematic development workflow for complex multi-step work with separation of concerns and persistent task knowledge.</em>
</p>

<p align="center">
  <a href="https://github.com/HermeticOrmus/riper-workflow-skills/stargazers"><img src="https://img.shields.io/github/stars/HermeticOrmus/riper-workflow-skills?style=flat-square&color=aa8142" alt="Stars" /></a>
  <a href="https://github.com/HermeticOrmus/riper-workflow-skills/blob/main/LICENSE"><img src="https://img.shields.io/github/license/HermeticOrmus/riper-workflow-skills?style=flat-square&color=aa8142" alt="License" /></a>
  <a href="https://github.com/HermeticOrmus/riper-workflow-skills/commits"><img src="https://img.shields.io/github/last-commit/HermeticOrmus/riper-workflow-skills?style=flat-square&color=aa8142" alt="Last Commit" /></a>
  <img src="https://img.shields.io/badge/Claude_Code-aa8142?style=flat-square&logo=anthropic&logoColor=white" alt="Claude Code" />
</p>

---

> **A single `CLAUDE.md` for the RIPER methodology — Research, Innovate, Plan, Execute, Review. Five-phase systematic development for complex multi-step work.**

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

---

## Part of the Libre Open-Source Stack for Claude Code

This repository is part of a growing family of open-source toolkits for Claude Code.

### Libre suite — comprehensive plugin bundles

- [LibreUIUX-Claude-Code](https://github.com/HermeticOrmus/LibreUIUX-Claude-Code) — UI/UX development (152 agents, 70 plugins, 76 commands, 74 skills)
- [LibreArch-Claude-Code](https://github.com/HermeticOrmus/LibreArch-Claude-Code) — Software architecture and system design
- [LibreCopy-Claude-Code](https://github.com/HermeticOrmus/LibreCopy-Claude-Code) — Technical writing and documentation engineering
- [LibreDevOps-Claude-Code](https://github.com/HermeticOrmus/LibreDevOps-Claude-Code) — DevOps engineering and infrastructure automation
- [LibreEmbed-Claude-Code](https://github.com/HermeticOrmus/LibreEmbed-Claude-Code) — Embedded systems, firmware, and IoT development
- [LibreFinTech-Claude-Code](https://github.com/HermeticOrmus/LibreFinTech-Claude-Code) — Financial technology development
- [LibreGEO-Claude-Code](https://github.com/HermeticOrmus/LibreGEO-Claude-Code) — AI-search optimization (ChatGPT, Perplexity, Gemini, Google AI Overviews)
- [LibreGameDev-Claude-Code](https://github.com/HermeticOrmus/LibreGameDev-Claude-Code) — Game development across Godot, Unity, Unreal
- [LibreMLOps-Claude-Code](https://github.com/HermeticOrmus/LibreMLOps-Claude-Code) — ML engineering and AI operations
- [LibreMobileDev-Claude-Code](https://github.com/HermeticOrmus/LibreMobileDev-Claude-Code) — Mobile app development (Flutter, React Native, native iOS, native Android)
- [LibreSecOps-Claude-Code](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code) — Security operations
- [LibreSessionFlow-Claude-Code](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code) — Session lifecycle: handoff, pickup, absorb, explore, close

### Skills mini-repos — single CLAUDE.md drop-ins

- [vibe-engineer-skills](https://github.com/HermeticOrmus/vibe-engineer-skills) — Direct AI codegen well: hypothesis before help, scoped prompts, validate before accepting
- [markdown-discipline-skills](https://github.com/HermeticOrmus/markdown-discipline-skills) — Strip AI-slop from markdown (no em dashes, no marketing fluff)
- [shell-safety-skills](https://github.com/HermeticOrmus/shell-safety-skills) — `set -euo pipefail` discipline plus 15 failure-mode examples
- [commit-standard-skills](https://github.com/HermeticOrmus/commit-standard-skills) — Ormus Commit Standard v1.0 plus commit-msg hook and commitlint
- [unwoke-skills](https://github.com/HermeticOrmus/unwoke-skills) — Strip AI theater (ten sins to eliminate, symmetric engagement)
- [python-conventions-skills](https://github.com/HermeticOrmus/python-conventions-skills) — Modern Python 3.11+ (types, pathlib, async, ruff, mypy, uv)
- [typescript-conventions-skills](https://github.com/HermeticOrmus/typescript-conventions-skills) — TypeScript strict mode, discriminated unions, Result types
- [hermetic-laws-skills](https://github.com/HermeticOrmus/hermetic-laws-skills) — Seven Hermetic Principles applied to engineering
- [six-day-cycle-skills](https://github.com/HermeticOrmus/six-day-cycle-skills) — Sustainable shipping cadence with mandatory rest
- [token-optimization-skills](https://github.com/HermeticOrmus/token-optimization-skills) — Claude Code token and context optimization
- [osint-skills](https://github.com/HermeticOrmus/osint-skills) — OSINT research methodology (multi-wave investigative spiral)
- [calcinate-skills](https://github.com/HermeticOrmus/calcinate-skills) — Stage 1 of the Magnum Opus (burn project bloat)
- [claude-md-overhaul-skills](https://github.com/HermeticOrmus/claude-md-overhaul-skills) — Audit CLAUDE.md and MEMORY.md against caps
- [session-handoff-skills](https://github.com/HermeticOrmus/session-handoff-skills) — Session handoff and pickup discipline
- [naming-skills](https://github.com/HermeticOrmus/naming-skills) — Product naming methodology (mine the brand's vocabulary)
- [magnum-opus-skills](https://github.com/HermeticOrmus/magnum-opus-skills) — Seven-stage alchemy applied to project transformation
- [mem-search-skills](https://github.com/HermeticOrmus/mem-search-skills) — Search claude-mem cross-session memory: search, filter, fetch
- [hypothesis-debugging-skills](https://github.com/HermeticOrmus/hypothesis-debugging-skills) — Hypothesis-driven debugging: reproduce, isolate, test, fix
- [vibe-proof-skills](https://github.com/HermeticOrmus/vibe-proof-skills) — Security hardening for vibe-coded full-stack apps
- [tdd-skills](https://github.com/HermeticOrmus/tdd-skills) — Test-driven development (Red-Green-Refactor) for JS/TS and Python
- [mars-skills](https://github.com/HermeticOrmus/mars-skills) — Production-readiness audit: the five mortal sins of vibe-coded MVPs
- [git-workflow-skills](https://github.com/HermeticOrmus/git-workflow-skills) — Clean git workflow: branch, atomic commits, reviewable PRs
- [code-review-skills](https://github.com/HermeticOrmus/code-review-skills) — Domain-aware code review: classify the code, then focus
- [explore-code-skills](https://github.com/HermeticOrmus/explore-code-skills) — Understand an unfamiliar codebase fast
- [dx-audit-skills](https://github.com/HermeticOrmus/dx-audit-skills) — Audit developer experience: docs, onboarding, tooling friction
- [setup-env-skills](https://github.com/HermeticOrmus/setup-env-skills) — Set up a project's development environment
- [automate-skills](https://github.com/HermeticOrmus/automate-skills) — Turn repetitive tasks into reliable automation scripts
- [quick-fix-skills](https://github.com/HermeticOrmus/quick-fix-skills) — Fast troubleshooting for common issues
- [prime-context-skills](https://github.com/HermeticOrmus/prime-context-skills) — Prime project context at the start of a session
- [auto-docs-skills](https://github.com/HermeticOrmus/auto-docs-skills) — Generate and maintain project documentation
- [learning-skills](https://github.com/HermeticOrmus/learning-skills) — Learn any technology: roadmaps, explanations, practice, cheatsheets, comparisons
- [linux-sysadmin-skills](https://github.com/HermeticOrmus/linux-sysadmin-skills) — Linux system administration: security, performance, diagnostics, monitoring, maintenance

### Template source

- [andrej-karpathy-skills](https://github.com/HermeticOrmus/andrej-karpathy-skills) — the canonical single-file CLAUDE.md pattern (fork of jiayuan_jy's original)

Star the family, not just one — that's how the suite stays coherent.
