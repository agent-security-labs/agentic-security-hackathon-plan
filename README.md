# Security for Agentic System and Tool Invocation

AI agents and MCP clients increasingly invoke external tools and APIs on a user's behalf. Doing this safely calls for a set of **security functions**: establishing who an agent is, what it is allowed to do, where a request came from, whether a sensitive action should proceed, and leaving an auditable trail.

This repository hosts an interactive overview page that maps this problem space — anchored to the **OWASP Top 10 for Agentic Applications 2026 (ASI01–ASI10)** — and shows how the building blocks we are working on fit into the larger picture.

> **📄 View the full interactive page: [Live version](https://agent-security-labs.github.io/agentic-security-hackathon-plan/agentic-security-hackathon-plan.html) · [Source](./agentic-security-hackathon-plan.html)**
> The three views in the page are linked — click any block, requirement, or card to trace one thread across all of them, and filter by maturity.

## The big picture

A single tool call from an agent passes through several security functions — verifying identity and credentials, checking authorization, validating intent and provenance, reaching a policy decision, then enforcing and recording it:

```
 WHAT THE AGENT / MCP CLIENT PRESENTS
 ┌─────────────────────┐ ┌──────────────────────┐ ┌─────────────────────────┐
 │ Identity &          │ │ Authorization tokens │ │ Intent & trigger-source │
 │ credentials         │ │ (OAuth)              │ │ provenance+confirmation │
 │ (DID / VC / VP)     │ │                      │ │                         │
 └──────────┬──────────┘ └──────────┬───────────┘ └────────────┬────────────┘
            ▼                       ▼                          ▼
 SECURITY FUNCTIONS · VERIFY → DECIDE → ENFORCE
 ┌─────────────────┐  ┌─────────────────┐  ┌──────────────────┐  ┌───────────────┐
 │ Verify identity │→ │ Check authoriz. │→ │ Validate intent  │→ │ Policy        │
 │ & credentials   │  │ & capability    │  │ & provenance     │  │ decision      │
 └─────────────────┘  └─────────────────┘  └──────────────────┘  └───────┬───────┘
                                                                   Allow │
                                                                         ▼
                                              ┌───────────────────────────────────┐
                                              │ Authorized tool / MCP invocation  │ ENFORCE
                                              └─────────────────┬─────────────────┘
                                                                ▼
                                              ┌───────────────────────────────────┐
                                              │ Audit & evidence chain            │ OBSERVE
                                              │ (replayable record)               │
                                              └───────────────────────────────────┘
```

Open areas around this pipeline where we welcome collaboration: memory / context-poisoning defense, runtime containment / kill-switch, third-party MCP attestation, goal / instruction integrity, and inter-agent / MCP channel trust.

## Requirements landscape

The same problem space, organised as twelve requirements across the request lifecycle and mapped to the OWASP ASI risks each one addresses:

| Stage | # | Requirement | Status | OWASP ASI |
|---|---|---|---|---|
| 1 · Identity & Trust | R1 | Agent / MCP identity | 🟢 Active | ASI03, ASI09 |
| | R2 | Credentials & lifecycle (DID / VC / VP, tokens, capability VC) | 🟢 Active | ASI03 |
| | R3 | Capability scoping (least-agency) | 🟡 Early | ASI03 |
| 2 · Request Provenance | R4 | Trigger-source & confirmation | 🟢 Active | ASI01, ASI09 |
| | R5 | Channel trust | 🟡 Early | ASI07 |
| | R6 | Goal / instruction integrity | ⚪ Open | ASI01 |
| 3 · Tool Access Safety | R7 | Tool authorization | 🟢 Active | ASI02, ASI03 |
| | R8 | Sensitive-data policy | 🟢 Active | ASI02, ASI06 |
| | R9 | Context-poisoning defense | ⚪ Open | ASI06 |
| 4 · Monitoring | R10 | Audit & evidence chain | 🟡 Early | ASI10 |
| | R11 | Runtime containment / kill-switch | ⚪ Open | ASI05, ASI08, ASI10 |
| | R12 | 3rd-party MCP attestation | ⚪ Open | ASI04 |

🟢 Active focus · 🟡 Early-stage · ⚪ Open, welcome collaboration

For the full descriptions, the cross-links between requirements, functions and work items, and the per-card details, **see the [interactive page](https://agent-security-labs.github.io/agentic-security-hackathon-plan/agentic-security-hackathon-plan.html)**.

## Collaborate with us

We are bringing several of these building blocks to an IETF hackathon to show how they relate within a common picture of agentic security. If you are working on agent identity, credentials and authorization, intent and provenance, tool-access policy, auditability — or on any of the open areas above — we would love to compare notes and build together.

The aim is not a single finished product but a shared, interoperable picture of how these security functions connect, so the community can contribute pieces that fit. Reach out via this repository's issues, or the relevant IETF working groups.

---

*Anchored to OWASP Top 10 for Agentic Applications 2026 (ASI01–ASI10, released Dec 2025).*
