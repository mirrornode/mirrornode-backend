# MIRRORNODE — Agent Registry

**Ground Truth Version:** 1.1 (June 2026)  
**Source of truth:** `SYSTEM_CONTRACT.md` · `AGENTS_TODO.md`

## Active Runtimes

### LUCIAN — Port 7700
**Role:** Orchestration & Manifest  
**Source:** `lucian/runtime.py`  
**Entry point:** `POST /dispatch`  
**Responsibilities:**
- Canonical command entry for the entire lattice
- Maintains `/manifest` with real lattice state
- Keeps `/lattice/status` aligned with reachable node health
- All dispatch actions emit canon audit records
- Command registry visibility via `canon.api.commands`

### OSIRIS — Port 7701
**Role:** Payment & Commerce (Stripe)  
**Source:** `osiris/runtime.py`  
**Responsibilities:**
- Stripe routes isolated to commerce concerns only
- Maintains `/health`, `/heartbeat`, `/identity`, `/stripe/status`
- Audits checkout, invoice, refund, subscription, and webhook flows
- UI shell concerns do not enter this runtime

## Registry-Only (Not Yet Runtime)

The following agents are registered in LUCIAN's manifest but do not have confirmed independent runtimes. Do not document them as active services.

| Agent | Port | Role                        |
|-------|------|-----------------------------|
| HERMES | 7702 | Messaging & Protocol       |
| THOTH  | 7703 | Services & Health          |
| THEIA  | 7704 | Witness & Observation      |
| PTAH   | 7705 | Creation & Bridge          |
| EVE    | 7706 | Embodiment & Physical Manifest |

Each registry-only agent needs a health endpoint and confirmed runtime source before being promoted to Active.

## Shared Agent Contract

All agents must:
- Route command execution through LUCIAN `POST /dispatch`
- Expose health surfaces honestly
- Audit runtime actions with `emit_audit()`
- Avoid documenting non-existent endpoints
- Keep repo roles aligned with real runtime boundaries
