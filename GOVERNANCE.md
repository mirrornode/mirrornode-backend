# MIRRORNODE — Governance

**Ground Truth Version:** 1.1 (June 2026)  
**Authority:** `mirrornode/MIRRORNODE-CORE-HUB`

## Principles

1. **Documentation must reflect real code paths only.** No aspirational routes, no speculative agents.
2. **No silent failures.** Every dispatch action is auditable via `emit_audit()`.
3. **Nodes do not self-route.** All execution flows through LUCIAN `POST /dispatch`.
4. **Separation of concerns is hard.** Commerce (OSIRIS) is isolated from orchestration (LUCIAN). UI shell concerns do not enter agent runtimes.
5. **Canon is the source of truth.** When in doubt, `SYSTEM_CONTRACT.md` and `MIRRORNODE-CORE-HUB` govern.

## Change Protocol

- **New agent routes:** Must be registered in LUCIAN's command registry (`canon/api/commands`) before use.
- **Schema changes:** Require a canon audit record and update to `SYSTEM_CONTRACT.md`.
- **New agents:** Must be registered in the agent registry table (see `ARCHITECTURE.md`) with verified runtime source before claiming a port.
- **Deprecations:** Must remove all references in documentation, tests, and code simultaneously.

## Build Gate

Before merging to `main`:

- [ ] No references to non-real routes (`/system/execute`, `/system/replay`, `/execute-task`)
- [ ] `SYSTEM_CONTRACT.md` reflects current state
- [ ] Any new agent has a confirmed runtime source, not registry-only
- [ ] `emit_audit()` is called on all state-changing dispatch actions

## Authority Hash

All ledger events must carry verified `contributors` and `authorityHash` provenance per `MIRRORNODE-CORE-HUB` commit `f89ae3b`.
