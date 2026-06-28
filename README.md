# Network-Automation — Agentic Network Engineering Platform

This repository is the **home base** for an on-prem team of specialized AI agents
that run network operations end-to-end: design, configuration, automation,
compliance, audit, change management, and risk.

You (the human operator) sit at the top as the **NOC Lead** — you set intent and
approve high-impact actions. A team of specialist agents does the work underneath,
each owning one discipline, all sharing a single source of truth and a single
audit trail.

> **Status:** Architecture / design phase. The first deliverable is the *target
> architecture map* — see [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md). No agents
> are wired to production yet.

## The foundation we build on

This platform is not greenfield. Two existing repos become components of it:

| Existing asset | Role in the target architecture |
|---|---|
| [`netbox-nornir-graphql-webinar`](https://github.com/packetcoders/netbox-nornir-graphql-webinar) | The **config-generation engine** — NetBox (source of truth) → GraphQL → Nornir → Jinja2. Becomes the Config & Automation agents' execution tooling. |
| `Firewall-Analyser` | The **security analysis surface** — becomes the Firewall/Security agent's UI and ruleset-analysis backend. |

## Where to start

1. **[`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md)** — the full target architecture: layers, data flows, deployment on the Dell servers.
2. **[`docs/AGENTS.md`](docs/AGENTS.md)** — the agent roster: one agent per discipline, with responsibilities, tools, and autonomy levels.
3. **[`docs/GOVERNANCE.md`](docs/GOVERNANCE.md)** — guardrails, RBAC, autonomy tiers, approval gates, and the audit trail. *Read this before giving any agent write access.*
4. **[`docs/ROADMAP.md`](docs/ROADMAP.md)** — the phased build plan from read-only lab to governed production.

## Design principles

- **Source of truth is NetBox.** Intended state lives in NetBox + Git, never in an agent's head.
- **Everything is config-as-code.** Templates, policies, agent definitions, and runbooks are versioned and peer/agent-reviewed via PRs.
- **Read-only by default; writes are earned.** An agent starts read-only and is promoted per the autonomy tiers in `GOVERNANCE.md`.
- **Every action is auditable.** Intent, prompt, tool calls, diffs, and approvals are logged immutably — this *is* the compliance evidence.
- **Human-in-the-loop on production.** Agents propose; the operator approves anything that touches prod.
