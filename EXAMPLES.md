# Examples

A worked RIPER task end-to-end. Hypothetical scenario: replace a hand-rolled session token system with proper JWT.

---

## Task: Replace session tokens with JWT in our API

### Phase 1 — Research

Output: `~/dev/jwt-migration/research-notes.md`

```markdown
# JWT migration — research

## Current state

- `auth/sessions.ts`: 312 LOC. Hand-rolled token generation using random bytes + SHA256.
- `auth/middleware.ts`: 89 LOC. Validates token by DB lookup on every request.
- DB: `sessions` table, 4.2M rows, indexed on `token_hash`.
- Token shape: 64 random bytes, base64-encoded. No expiry encoded; expiry stored in DB.
- Token refresh: separate endpoint, rotates token in DB.

## Findings

- 4.2M sessions means token validation = DB read per request. Latency p95: 12ms.
- Token revocation is fast (delete row) but token validation is slow.
- No token rotation enforced; old tokens valid until DB delete.
- Mobile clients have hard-coded tokens with 90-day TTL.

## Constraints

- 50+ services depend on the current auth endpoint shape.
- Mobile app v3.x in production won't be updated for ~6 weeks.
- Can't break the existing token format without coordinated rollout.

## Open questions

- Do we want JWT signing keys per-service or central?
- Does refresh-token model match our security review board's requirements?
- What's the migration window?
```

### Phase 2 — Innovate

Output: `~/dev/jwt-migration/approaches.md`

```markdown
# JWT migration — approaches

## Approach A: Full JWT replacement, big-bang cutover

- Replace token format entirely.
- Deploy backend + clients in lockstep.
- Pros: clean, single auth model going forward.
- Cons: requires mobile app update; 6-week timeline.
- Risk: any client we don't update breaks at cutover.

## Approach B: Dual-format support during migration window

- Backend accepts both old random-token and new JWT.
- Old tokens validated via DB; new tokens validated via signature.
- Mobile app updates over 90 days; backend retires old format after.
- Pros: no forced client coordination.
- Cons: complexity in middleware; longer migration tail.

## Approach C: JWT-with-DB-lookup hybrid

- Issue JWT (signed, with metadata) but still validate via DB.
- Keep DB-as-source-of-truth; signature is just optimization.
- Pros: instant revocation; no migration of clients.
- Cons: defeats the perf benefit of JWT; mostly cosmetic upgrade.

## Recommendation: Approach B

Approach B trades complexity (dual-format) for client flexibility (no forced update). Mobile migration is the binding constraint; B respects it. C is rejected because it doesn't solve the actual problem (DB latency).
```

### Phase 3 — Plan

Output: `~/dev/jwt-migration/jwt-migration-plan.md`

```markdown
# JWT migration — technical plan

## Goal
Move auth from DB-lookup random tokens to JWT-signature validation, reducing
p95 latency 12ms → <1ms while maintaining mobile client compatibility for 90
days.

## Chosen approach
Approach B (dual-format support during migration window).

## Success criteria
- [ ] All new sessions issued as JWT
- [ ] Existing random tokens continue to work
- [ ] p95 latency for JWT validation < 1ms (measured at gateway)
- [ ] Existing test suite passes
- [ ] Mobile v3.x continues to authenticate

## Implementation steps

1. Add JWT signing infrastructure (key generation, rotation) — Est. 4h
   - Verify: keys generated, rotation script tested in staging
2. Add JWT issuance to /login + /refresh endpoints — Est. 6h
   - Verify: new sessions return JWT alongside random token
3. Update middleware to accept both formats — Est. 3h
   - Verify: requests with random token still work; requests with JWT work
4. Migrate session refresh to issue JWT only — Est. 2h
   - Verify: existing client behaviors continue
5. Add telemetry on token format mix — Est. 2h
   - Verify: dashboard shows random→JWT ratio
6. After 90 days: deprecate random token format — separate plan

## Tests required
- Unit: JWT signing/validation, dual-format middleware
- Integration: /login + /refresh return JWT, gateway accepts both
- E2E: mobile v3 client logs in successfully, mobile v4 client logs in with JWT

## Rollback plan
- Feature flag `JWT_ENABLED=false` on middleware → fall back to random tokens only
- All JWT-issued sessions remain valid via signature (no DB row needed to invalidate)
```

### Phase 4 — Execute

Working code. The plan's 6 steps are completed sequentially. At each step, the verify check is run before moving to the next. Mid-execution discoveries get added to the plan's "deviations" section, not silently changed.

### Phase 5 — Review

Output: `~/dev/jwt-migration/review.md`

```markdown
# JWT migration — review

## Success criteria check
- [x] All new sessions issued as JWT — verified in telemetry
- [x] Existing random tokens continue to work — soak-tested for 7 days
- [x] p95 latency for JWT validation < 1ms — measured 0.4ms at gateway
- [x] Existing test suite passes — green
- [x] Mobile v3.x continues to authenticate — telemetry confirms

## What went well
- Dual-format middleware was cleaner than expected
- Signing-key rotation script paid off when we rotated mid-migration
- Telemetry made the migration progress visible to stakeholders

## What we'd do differently
- Step 5 (telemetry) should have been step 1 — we were flying blind for the first half
- The 90-day window is conservative; mobile v3.x uptake dropped to <5% within 60 days
- Key-management runbook should be merged into ops docs (TODO: separate PR)

## Open items
- Deprecation plan for random token format (separate task)
- Service-by-service audit of token usage outside the main /login flow (separate task)
```

---

## Why this works

Each phase produced an artifact that the next phase consumed. No phase mixed concerns. The plan was specific enough to execute mechanically. The review verified against the plan's success criteria, not against vague feelings.

The cost: ~half a day of overhead before the first line of code was written.

The benefit: a migration that didn't break anything, with traceable decisions and resumability.

For tasks smaller than this, the overhead exceeds the benefit. Use judgment.
