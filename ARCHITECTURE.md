# MIRRORNODE — Architecture

**Ground Truth Version:** 1.1 (June 2026)  
**Canonical source:** `SYSTEM_CONTRACT.md` and `mirrornode/MIRRORNODE-CORE-HUB`

## Execution Model

MIRRORNODE is a governed multi-agent execution lattice. All commands enter through a single authority surface:

```
POST /dispatch  →  LUCIAN (port 7700)  →  target agent
```

Nodes do not self-route. LUCIAN is the only orchestration authority. No agent dispatches to another agent directly.

## Agent Registry

| Agent  | Port | Role                        | Runtime Status          |
|--------|------|-----------------------------|-------------------------|
| LUCIAN | 7700 | Orchestration & Manifest    | Active (`lucian/runtime.py`) |
| OSIRIS | 7701 | Payment & Commerce (Stripe) | Active (`osiris/runtime.py`) |
| HERMES | 7702 | Messaging & Protocol        | Registry only           |
| THOTH  | 7703 | Services & Health           | Registry only           |
| THEIA  | 7704 | Witness & Observation       | Registry only           |
| PTAH   | 7705 | Creation & Bridge           | Registry only           |
| EVE    | 7706 | Embodiment & Physical Manifest | Registry only        |

## Lattice Truth Surface

The following endpoints are verified real routes on LUCIAN:

- `GET /manifest` — current lattice state
- `GET /lattice/status` — reachable node health
- `GET /health` — service health
- `GET /heartbeat` — liveness
- `GET /identity` — node identity

## Explicit Non-Routes

These are NOT real routes and must not be referenced in documentation or tests:

- `/system/execute`
- `/system/replay`
- `/execute-task`

## Audit Mechanism

All dispatch actions emit a canon audit record:

```python
emit_audit(repo, event_type, actor, verdict, evidence)
```

## Canon Structure

```
canon/
  contracts/
  charters/
  api/
  dossiers/
```

This file reflects active runtime truth. Update it when runtimes change.
