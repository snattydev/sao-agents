# SAO Agents 🏹⚔️🌸🎓

![Status](https://img.shields.io/badge/status-active-7ED3C1?style=flat-square)
![Hermes](https://img.shields.io/badge/platform-Hermes%20Profiles-31748f?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-ebbcba?style=flat-square)

> Un ecosistema de **agentes de IA con personalidad**, inspirado en _Sword Art Online_.  
> Cada agente es un perfil nativo de [Hermes Agent](https://hermes-agent.nousresearch.com) con su propio rol, personalidad y herramientas.
>
> ⚠️ **Nota:** Esta es una configuración personal. El roster refleja mis necesidades particulares. Usalo como inspiración para armar el tuyo.

---

## 📋 Agentes

| # | Agente | Rol | Modelo (daily) | Heavy | Toolsets | Estado |
|---|--------|-----|:--------------:|:-----:|----------|--------|
| 🏹 | **Shinon** | Orchestrator (Host) | deepseek-v4-flash (GO) | — | web, browser, terminal, file, code_execution, vision, skills, memory, session_search, delegation, cronjob, todo | ⚡ Activo |
| ⚔️ | **Kirito** | Engineering | deepseek-v4-flash (GO) | qwen3.7-plus | terminal, file, web, search, delegation | ⚡ Activo |
| 🌸 | **Asuna** | Organization | deepseek-v4-flash (GO) | fallback ZEN | file, search, web, browser | ⚡ Activo |
| 🎓 | **Eugeo** | Study (MEXT) | deepseek-v4-flash-free (ZEN) | ds-v4-flash (GO) | file, search, web, browser, vision | ⚡ Activo |
| 💪 | **Agil** | Fitness & Health | — | — | — | ⚪ Apagado |
| 🐉 | **Silica** | Finance & Data | — | — | — | ⚪ Apagado |
| ⚖️ | **Alice** | Social / Discord | deepseek-v4-flash | — | file, search, web, vision | 💤 Reposicionado |
| 🐀 | **Argo** | Travel & Research | deepseek-v4-flash | — | file, search, web | 💤 Reposicionado |
| 🌿 | **Leafa** | Content Assistant | deepseek-v4-flash | — | file, search, web, vision | 💤 Reposicionado |
| 🔧 | **Lisbeth** | Tooling & DevOps | deepseek-v4-flash | — | terminal, file, search, web | 💤 Reposicionado |
| 💻 | **Yui** | Review & Support | kimi-k2.6 | — | file(ro), search, web, vision | 💤 Reposicionado |
| 🎤 | **Yuna** | Music | deepseek-v4-flash | — | file, search, web, tts, spotify, vision | 💤 Reposicionado |

---

## 🚀 Instalación

### Prerequisitos

- [Hermes Agent](https://hermes-agent.nousresearch.com/docs/getting-started/installation) instalado
- Proveedor `opencode-go` configurado

### Clonar y configurar un agente

```bash
# 1. Clonar este repo
git clone https://github.com/tu-usuario/sao-agents.git
cd sao-agents

# 2. Copiar el SOUL.md del agente que quieras
mkdir -p ~/.hermes/profiles/kirito
cp profiles/kirito/SOUL.md ~/.hermes/profiles/kirito/SOUL.md

# 3. Configurar el perfil con el modelo correspondiente
hermes -p kirito config set model.default deepseek-v4-flash
hermes -p kirito config set model.provider opencode-go

# 4. Asignar alias para usarlo directo
hermes profile alias kirito

# 5. Usarlo
kirito chat -q "🏹 Shinon acá: decime quién sos"
```

Ver [`SETUP.md`](./SETUP.md) para la guía completa por agente.

---

## 🏗️ Stack

| Componente | Tecnología |
|------------|-----------|
| **Orquestador** | [Hermes Agent](https://hermes-agent.nousresearch.com) (profiles nativos) |
| **Provider principal** | OpenCode Go ($10/mes) |
| **Provider secundario** | OpenCode ZEN (gratis) |
| **Modelo default** | deepseek-v4-flash (GO) / deepseek-v4-flash-free (ZEN fallback) |
| **Modelos heavy** | qwen3.7-plus, deepseek-v4-pro, minimax-m3 |
| **Comunicación** | `<agente> chat -q` (terminal) / `delegate_task` (subagentes ZEN) |
| **Gateways** | Telegram, Discord, WhatsApp (según perfil) |
| **Backups** | `hermes profile export` o copiar `~/.hermes/profiles/<name>/` |

---

## 🔄 Comunicación entre agentes

```bash
# Shinon delega a Kirito
kirito chat -q "🏹 Shinon acá: revisá este código, porfa"

# Shinon consulta a Asuna
asuna chat -q "🏹 Shinon acá: organizame estas notas en el vault"
```

> ⚠️ Cada `chat -q` arranca sesión desde cero. Incluir **self-ID** siempre.

---

## 🗺️ Roadmap

Ver [`ROADMAP.md`](./ROADMAP.md) — Klein relay, VPS, división desktop/laptop.

---

> 🏹 _私が後ろにいる — 君は落ちない._
