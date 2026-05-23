# CLAUDE.md

The RIPER methodology — Research, Innovate, Plan, Execute, Review. Five-phase systematic development for complex multi-step work.

**Tradeoff**: bias toward separation of concerns over speed. For trivial bug fixes, use judgment.

## Philosophy

- **Separation of concerns**: Research ≠ Planning ≠ Execution. Mixing phases corrupts each.
- **Context efficiency**: Each phase uses minimal tokens for its purpose.
- **Persistent knowledge**: Work documented in `~/dev/[task]/` for resumability.
- **Conscious progression**: Intentional phase transitions, not reactive coding.

## The five phases

### 1. Research — read-only investigation

```
Output: ~/dev/[task]/research-notes.md
Access: Read-only (no code changes)
```

- Examine current implementation
- Understand data flow and dependencies
- Document findings systematically
- Identify constraints and opportunities
- Ask questions, don't assume

**Done when**: clear understanding of "what exists now."

### 2. Innovate — optional brainstorming

```
Output: ~/dev/[task]/approaches.md
Access: Read-only (still no changes)
```

- Brainstorm multiple approaches
- Compare trade-offs (complexity, performance, maintainability)
- Consider edge cases
- Document rationale per approach

**Done when**: 2-3 viable approaches with trade-offs documented.

### 3. Plan — specification and design

```
Output: ~/dev/[task]/[task]-plan.md
Access: Can write to memory/docs
```

- Choose the best approach from Innovation
- Define **measurable** success criteria
- Break into implementable steps with estimates
- Identify tests needed
- Document API/interface changes
- **Get approval before proceeding**

**Done when**: executable specification exists.

### 4. Execute — implementation

```
Access: Full (read, write, test)
```

- Follow the plan sequentially
- Run required commands after each change (format, lint, test)
- Document decisions/deviations in code comments
- Update plan if scope changes mid-execution
- Verify each step against the plan's success criteria

**Done when**: all plan steps complete, success criteria met.

### 5. Review — verification and retrospective

```
Output: ~/dev/[task]/review.md
Access: Read-only after final commit
```

- Verify success criteria
- Run full test suite
- Check for regressions
- Document what was learned
- Note what to do differently next time

**Done when**: review document signed off.

## Phase transitions

Each transition is a deliberate decision, not a slide. Before moving from Research → Plan, you must have read enough to specify the change. Before Plan → Execute, you must have approval. Before Execute → Review, all steps must be complete.

Resist mixing phases:

- Don't start coding during Research ("just a small fix") — corrupts your model with assumptions
- Don't research mid-Execution ("oh I need to check one more thing") — produces incomplete plans
- Don't skip Review ("we shipped, it works") — loses the retrospective signal

## When to use RIPER

- Architecture changes
- Multi-file refactors
- New features touching multiple subsystems
- Migrations (DB schema, framework upgrade)
- Anything where mistakes compound (auth, payments, data integrity)

## When NOT to use RIPER

- Typo fixes
- Single-file bug fixes with obvious cause
- Documentation updates
- Prototype exploration where the discipline cost exceeds the discovery value

## Plan template

```markdown
# [Task] — Technical Plan

## Goal
[What we're building and why]

## Chosen Approach
[Selected from Innovation phase, with rationale]

## Success Criteria
- [ ] Measurable criterion 1
- [ ] Measurable criterion 2

## Implementation Steps
1. Step 1 — Est. 30 min — Verify: [check]
2. Step 2 — Est. 1 hour — Verify: [check]

## Tests Required
- Unit: [functions]
- Integration: [workflows]
- E2E: [user flows]

## Rollback Plan
[How to undo if needed]
```

## Persistent knowledge directory

Each RIPER task lives at `~/dev/[task]/`. Resumability is the point — if you walk away and return a week later, the research-notes + approaches + plan + review tell you exactly where you left off.

---

**License**: MIT.
