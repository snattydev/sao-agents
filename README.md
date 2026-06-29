# SAO Agents 🏹⚔️🌸🎓

[English](README.md) / [Español](README_ES.md)

![Status](https://img.shields.io/badge/status-active-7ED3C1?style=flat-square)
![Hermes](https://img.shields.io/badge/platform-Hermes%20Profiles-31748f?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-ebbcba?style=flat-square)

> An ecosystem of **AI agents with personality**, inspired by _Sword Art Online_.  
> Each agent is a native [Hermes Agent](https://hermes-agent.nousresearch.com) profile with its own role, personality, and tools.

---

## 📋 Agents

| # | Agent | Role | Model (daily) | Heavy | Toolsets | Status |
|---|-------|------|:--------------:|:-----:|----------|--------|
| 🏹 | **Shinon** | Orchestrator (Host) | deepseek-v4-flash (GO) | — | web, browser, terminal, file, code_execution, vision, skills, memory, session_search, delegation, cronjob, todo | ⚡ Active |
| ⚔️ | **Kirito** | Engineering | deepseek-v4-flash (GO) | qwen3.7-plus | terminal, file, web, search, delegation | ⚡ Active |
| 🌸 | **Asuna** | Organization | deepseek-v4-flash (GO) | fallback ZEN | file, search, web, browser | ⚡ Active |
| 🎓 | **Eugeo** | Study | deepseek-v4-flash (GO) | fallback ZEN | file, search, web, browser, vision | ⚡ Active |
| 💪 | **Agil** | Fitness & Health | — | — | — | 💤 Repurposed |
| 🐉 | **Silica** | Finance & Data | — | — | — | 💤 Repurposed |
| ⚖️ | **Alice** | Social / Discord | deepseek-v4-flash | — | file, search, web, vision | 💤 Repurposed |
| 🐀 | **Argo** | Travel & Research | deepseek-v4-flash | — | file, search, web | 💤 Repurposed |
| 🌿 | **Leafa** | Content Assistant | deepseek-v4-flash | — | file, search, web, vision | 💤 Repurposed |
| 🔧 | **Lisbeth** | Tooling & DevOps | deepseek-v4-flash | — | terminal, file, search, web | 💤 Repurposed |
| 💻 | **Yui** | Review & Support | kimi-k2.6 | — | file(ro), search, web, vision | 💤 Repurposed |
| 🎤 | **Yuna** | Music | deepseek-v4-flash | — | file, search, web, tts, spotify, vision | 💤 Repurposed |

---

## 🚀 Installation

### Prerequisites

- [Hermes Agent](https://hermes-agent.nousresearch.com/docs/getting-started/installation) installed
- `opencode-go` provider configured

### Clone and configure an agent

```bash
# 1. Clone this repo
git clone https://github.com/your-user/sao-agents.git
cd sao-agents

# 2. Copy the SOUL.md of the agent you want
mkdir -p ~/.hermes/profiles/kirito
cp profiles/kirito/SOUL.md ~/.hermes/profiles/kirito/SOUL.md

# 3. Configure the profile with the corresponding model
hermes -p kirito config set model.default deepseek-v4-flash
hermes -p kirito config set model.provider opencode-go

# 4. Set an alias for direct use
hermes profile alias kirito

# 5. Use it
kirito chat -q "🏹 Shinon here: tell me who you are"
```

See [`SETUP.md`](./SETUP.md) for the complete per-agent guide.

---

## 🏗️ Stack

| Component | Technology |
|-----------|-----------|
| **Orchestrator** | [Hermes Agent](https://hermes-agent.nousresearch.com) (native profiles) |
| **Primary provider** | OpenCode Go ($10/mo) |
| **Secondary provider** | OpenCode ZEN (free) |
| **Default model** | deepseek-v4-flash (GO) / deepseek-v4-flash-free (ZEN fallback) |
| **Heavy models** | qwen3.7-plus, deepseek-v4-pro, minimax-m3 |
| **Communication** | `<agent> chat -q` (terminal) / `delegate_task` (ZEN subagents) |
| **Gateways** | Telegram, Discord, WhatsApp (per profile) |
| **Backups** | `hermes profile export` or copy `~/.hermes/profiles/<name>/` |

---

## 🔄 Agent communication

```bash
# Shinon delegates to Kirito
kirito chat -q "🏹 Shinon here: review this code, please"

# Shinon asks Asuna
asuna chat -q "🏹 Shinon here: organize these notes in the vault"
```

> ⚠️ Each `chat -q` starts a fresh session. Always include **self-ID**.

---

## 🗺️ Roadmap

See [`ROADMAP.md`](./ROADMAP.md) — Klein relay, VPS, desktop/laptop split.

---

> 🏹 _私が後ろにいる — 君は落ちない._
