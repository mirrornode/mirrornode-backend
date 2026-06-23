# Copilot Instructions — mirrornode-backend

## System Context

This repo is part of the MIRRORNODE multi-agent execution lattice. Read `SYSTEM_CONTRACT.md`, `ARCHITECTURE.md`, and `AGENTS.md` before making changes.

## Hard Rules

- **Never generate references to non-real routes:** `/system/execute`, `/system/replay`, `/execute-task` do not exist.
- **All commands route through LUCIAN `POST /dispatch`.** Nodes do not self-route.
- **No silent failures.** Every state-changing action must call `emit_audit(repo, event_type, actor, verdict, evidence)`.
- **Documentation reflects real code paths only.** Do not describe aspirational or planned behavior as current.
- **Commerce logic stays in OSIRIS (port 7701).** Do not mix Stripe/payment logic into other agents.

## Architecture Quick Reference

```
Client → POST /dispatch → LUCIAN (7700) → target agent
```

Active agents: LUCIAN (7700), OSIRIS (7701)  
Registry-only: HERMES (7702), THOTH (7703), THEIA (7704), PTAH (7705), EVE (7706)

## Conventions

- Python: FastAPI, async handlers, `emit_audit()` on all mutations
- Canon audit records use: `emit_audit(repo, event_type, actor, verdict, evidence)`
- New routes must be registered in `canon/api/commands` before use
- Health endpoints required on all runtimes: `/health`, `/heartbeat`, `/identity`

## Before You Commit

- [ ] No references to non-real routes
- [ ] `SYSTEM_CONTRACT.md` still accurate
- [ ] `emit_audit()` called on all dispatch actions
- [ ] No agent is claiming a port without a confirmed runtime source
