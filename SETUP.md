# SAO Agents — Setup Guide

A general guide to running a SAO-style agent. The specifics depend on your runtime and infrastructure.

## What You Need

- An **agent runtime** that supports personality/system prompt files (like [Hermes Agent](https://hermes-agent.nousresearch.com))
- An **LLM provider** with API access
- (Optional) A **messaging gateway** (Telegram, Discord, etc.) if you want your agent available from chat platforms

---

## Quick Start

1. **Pick a personality** — choose a `SOUL.md` from `profiles/<agent>/` in this repo
2. **Create a profile** — most runtimes let you create named profiles, each with its own config
3. **Inject the SOUL.md** — use the file as the system prompt or personality definition
4. **Set up a model** — lighter agents work fine on smaller models; heavier ones benefit from stronger reasoning
5. **Add tools** — give the agent access to what its role needs: files, web search, terminal, etc.
6. **Test it** — start a session and see if the personality sticks

---

## Architecture Patterns

### Single-user (like my setup)

Agents run directly on your workstation with the same access level you have. Fine when you're the only user, but risky in shared environments.

### Containerized (recommended for production)

Each agent runs in its own container with scoped filesystem access, limited network, and dedicated credentials. This is the cleaner, more secure approach — especially if agents have different trust levels (e.g., one handles finance, another browses the web).

### Hybrid

Some agents run natively (lightweight, no isolation needed), others in containers (when they need heavy tool access or isolation). Choose based on each agent's role.

---

## SOUL.md — The Core

Every agent in this ecosystem is defined by its `SOUL.md`. This file contains:

| Section | What it defines |
|---------|----------------|
| **Identity** | Who the agent is — name, avatar, role, profile reference |
| **Personality** | Canon traits drawn from the SAO character — how they think and react |
| **Communication style** | Tone, dialect, catchphrases, metaphors |
| **Domain** | What the agent handles — its area of expertise |
| **Relationships** | How they relate to other agents in the roster |

The SOUL.md acts as the system prompt. Drop it in, and the agent becomes that character.

---

## Tools & Tool Restrictions

Each agent's toolset should reflect its role narratively:

- A **study agent** needs web search, document reading, maybe vision
- An **engineering agent** needs terminal access and file read/write
- A **social agent** might only need messaging and web search
- A **music agent** needs search plus any audio-related tools

The principle: **tool restriction narrativa** — toolsets reflect the fictional role.

---

## Communication Between Agents

Agents can coordinate in several ways:

- **Direct delegation** — one agent sends a task to another, passing context
- **Shared files** — agents write to a shared location and read from it
- **Message relay** — through a gateway, agents can message each other

Each approach has trade-offs. The simplest is direct delegation with self-identification (the sending agent states who it is).

---

## Security Considerations

- **API keys and tokens** go in environment files, never in the personality files or repo
- **Gateways** should use dedicated bot tokens per agent
- **Container isolation** is ideal when agents have different trust levels
- **Vault access** (if using a knowledge base) should be read-only for agents that only need to query, read-write for those that organize

---

## Tips

- Start with fewer agents. One well-tuned agent is worth more than ten half-baked ones.
- The personality is the differentiator. Two agents with the same model but different SOULs behave completely differently.
- Iterate on the SOUL.md as you use the agent — you'll discover what works and what doesn't.
- The architecture will change as you learn. That's fine. Document the evolution.
