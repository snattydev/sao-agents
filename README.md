# SAO Agents 🏹⚔️🌸🎓

[English](README.md) / [Español](README_ES.md)

> 🚧 **Personal Learning Project** — This repository is part of an ongoing exploration into AI agent personality and orchestration. An integrated project is currently under development and will be made public once ready.
>
> ©️ **Copyright Notice** — _Sword Art Online_ is the property of Reki Kawahara, A-1 Pictures, and Aniplex. This is a fan-made, non-commercial learning exercise. Not affiliated with or endorsed by the copyright holders.

![Status](https://img.shields.io/badge/status-active-7ED3C1?style=flat-square)
![Platform](https://img.shields.io/badge/platform-Hermes%20Profiles-31748f?style=flat-square)

> An ecosystem of **AI agents with personality**, inspired by _Sword Art Online_.  
> Each agent is shaped by a `SOUL.md` — a personality file that defines its role, voice, boundaries, and domain expertise.

---

## 📋 Agents

| # | Agent | Role | Compute | Key Toolsets |
|---|-------|------|:-------:|--------------|
| 🏹 | **Shinon** | Host & Orchestrator | Lightweight | web, browser, terminal, file, code, vision, delegation, cron, memory |
| ⚔️ | **Kirito** | Engineering | Heavy — code & architecture | terminal, file, web, delegation |
| 🌸 | **Asuna** | Organization & Vault | Lightweight | file, web, browser, terminal |
| 🎓 | **Eugeo** | Study & Research | Lightweight + Vision | file, web, browser, vision, terminal |
| 🌿 | **Leafa** | Content & Creativity | Lightweight | web, vision |
| ⚖️ | **Alice** | Social & Community | Lightweight | web, file, vision |
| 🔧 | **Lisbeth** | Tooling & DevOps | Lightweight | terminal, file, web |
| 🐉 | **Silica** | Finance & Data | Lightweight | file, web |
| 🐀 | **Argo** | Travel & Research | Lightweight | web, file |
| 💻 | **Yui** | Review & QA | Heavy — analysis | file(ro), web, vision |
| 🎤 | **Yuna** | Music & Audio | Lightweight | web, tts, spotify, vision |
| 💪 | **Agil** | Fitness & Health | Lightweight | web, file |

> All agents follow the same architectural pattern — a `SOUL.md` that defines personality and domain, paired with appropriate tool access. The "Compute" column gives a rough idea of model capability needed, not a specific model.

> ⚠️ **Security note:** This is a single-user setup — agents run directly on my workstation with broad tool access because I'm the only one interacting with them. In a multi-user or production environment, you'd want container isolation, scoped credentials, and read-only filesystems. The container architecture discussed in [`ARCHITECTURE.md`](./ARCHITECTURE.md) represents that production ideal.

---

## 💡 Personal Note

In my personal setup, I use **deepseek-v4-flash** for daily conversation and orchestration — it hits the sweet spot of speed, context window, and cost. Heavier models come in for complex code or deep research. But this repo is about the **personality and architecture layer**, not the model underneath. Swap in whatever model fits your needs and budget.

---

## 🏗️ Stack

| Component | Technology |
|-----------|-----------|
| **Runtime** | [Hermes Agent](https://hermes-agent.nousresearch.com) (native profiles) |
| **Communication** | Terminal / Gateways (Telegram, etc.) |
| **Architecture** | Profiles — each agent is an independent profile with its own identity |
| **Design** | `SOUL.md` — personality-as-config, inspired by SAO characters |

Each agent is a standalone Hermes profile. Its `SOUL.md` acts as the system prompt — defining who the agent is, how it speaks, what it handles, and what's off-limits.

---

## 🚀 Getting Started

1. **Pick an agent** — read its `SOUL.md` in `profiles/<agent>/`
2. **Drop it into your agent runtime** — most runtimes accept a system prompt or personality file
3. **Configure tools** — give the agent access to what its role needs (files, web, terminal, etc.)
4. **Use it** — start a session and let the personality drive the interaction

The `SOUL.md` files in this repo are self-contained. Grab the one that fits your use case, configure it in your agent platform of choice, and you're off.

See [`AGENTS.md`](./AGENTS.md) for full personality profiles.  
See [`ARCHITECTURE.md`](./ARCHITECTURE.md) for the thinking behind the design.

---

## 🔄 Agent Communication

Agents can coordinate with each other via their runtime's delegation or messaging mechanisms. Each session is independent — agents don't share memory unless explicitly connected.

When one agent needs another, it identifies itself and passes context. The receiving agent acts on it with its own personality and tools.

---

## 🗺️ Roadmap

See [`ROADMAP.md`](./ROADMAP.md) — the project evolves as I learn. Architecture has shifted multiple times and will keep shifting.

---

> 🏹 _私が後ろにいる — 君は落ちない._
