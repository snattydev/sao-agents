# SAO Agents — Architecture

> The architecture has evolved as I've learned. What follows is the current design thinking, with ~~strikethrough~~ marking concepts that have shifted along the way. This repo documents the journey, not a fixed destination.

---

## Design Philosophy

Each agent is a **profile** — an independent identity with its own personality (`SOUL.md`), tool access, and memory. Profiles are the unit of deployment: create one per agent, configure its tools, and let its personality drive the interaction.

The design evolves on three axes:
- **Isolation** — from full native access (single-user) to containerized (production)
- **Model assignment** — from multi-model routing per agent to a simpler unified provider
- **Roster size** — from 12 agents to a smaller active set and back as needs change

---

## Current Architecture

```
┌─────────────────────────────────────────────┐
│                 User                         │
│        (Terminal / Telegram)                 │
└──────────────────┬──────────────────────────┘
                   │
            ┌──────▼──────┐
            │   Shinon    │
            │ (Orchestr.) │
            └──────┬──────┘
                   │
          ┌────────┼────────┐
          │        │        │
    ┌─────▼──┐ ┌──▼───┐ ┌──▼────┐
    │ Asuna  │ │Eugeo │ │Kirito │
    │(Organ.)│ │(Study)│ │(Eng.) │
    └────────┘ └──────┘ └───────┘
```

### Profiles

Each agent is a standalone profile. Shinon (the default profile) serves as the host and orchestrator — the entry point for the user and the coordinator of the ecosystem. Other agents are independent profiles that can be interacted with directly or through delegation.

### Gateways

Agents can be reached through messaging gateways. Each gateway-connected agent has its own bot identity and can hold independent conversations. Currently Telegram is the active gateway; other platforms follow the same pattern.

### Storage

Each profile has its own isolated storage for sessions, memories, and configuration. ~~Some agents were designed to run in containers with mounted vaults~~ — the container pattern represents the production ideal but isn't currently in use for daily operation.

---

## Architecture Evolution

The architecture has gone through several phases as I've learned what works:

| Phase | Model Strategy | Roster | Isolation |
|:------|:--------------|:-------|:----------|
| **Initial** | ~~Multi-model routing per agent (GO + ZEN + FreeLLMAPI)~~ | Full 12-agent roster | ~~Containerized~~ |
| **Consolidation** | ~~Unified ZEN-only provider~~ | Reduced to 3-4 active | Native profiles |
| **Current** | Unified provider, lightweight primary model with heavier fallbacks for complex tasks | Flexible — core + conceptual | Native (single-user), container architecture documented as ideal |

Key shifts:
- ~~Complex per-agent model routing was replaced by a simpler unified provider strategy~~ — reduced cognitive overhead and maintenance
- ~~The roster was slimmed down as I learned which agents actually added value vs. which were overkill~~
- Containerization remains the aspirational deployment model for production use, but native profiles work well for a single-user setup

---

## Container Vision (Production Ideal)

For a production or multi-user deployment, each agent would run in its own container:

```
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│  Agent A     │  │  Agent B     │  │  Agent C     │
│ ┌──────────┐ │  │ ┌──────────┐ │  │ ┌──────────┐ │
│ │ SOUL.md  │ │  │ │ SOUL.md  │ │  │ │ SOUL.md  │ │
│ │ Config   │ │  │ │ Config   │ │  │ │ Config   │ │
│ │ Sessions │ │  │ │ Sessions │ │  │ │ Sessions │ │
│ │ Tools    │ │  │ │ Tools    │ │  │ │ Tools    │ │
│ └──────────┘ │  │ └──────────┘ │  │ └──────────┘ │
└──────────────┘  └──────────────┘  └──────────────┘
```

Each container has:
- Its own filesystem (scoped to what the agent needs)
- Limited network access (based on role — web agents browse, finance agents don't)
- Dedicated credentials (bot tokens, API keys)
- Independent session and memory storage

This pattern keeps agents isolated: if one is compromised or malfunctions, the others aren't affected. In my current single-user setup, this level of isolation isn't necessary — agents run directly on my workstation.

---

## SOUL.md Engine

The `SOUL.md` file is the heart of each agent. It defines:

1. **Canon personality** — character traits from the SAO Fandom wiki
2. **Communication style** — tone, dialect, catchphrases, speaking patterns
3. **Role boundaries** — what the agent does and doesn't handle
4. **Relationship dynamics** — how it interacts with other agents
5. **Domain** — the area it specializes in

The runtime reads `SOUL.md` at session start and uses it as the system prompt. This makes personality both portable (copy the file, get the same agent) and iterable (edit the file, change the behavior).

---

## Principles

1. **Canon personality** — drawn from the SAO Fandom wiki, not Wikipedia
2. **Tool restriction narrativa** — toolsets reflect the fictional role
3. **Consistent voice** — all agents in this roster use Argentine voseo
4. **SOUL.md as source of truth** — personality, instructions, relationships all live in one file
5. **Evolution over rigidity** — the architecture has changed multiple times and will keep changing. That's by design.
