# SAO Agents — Arquitectura

## Visión General

```
                    ┌─────────────┐
                    │   Telegram   │
                    │   Gateway    │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │   Shinon    │
                    │ (Orchestr.) │
                    └──────┬──────┘
                           │
          ┌────────────────┼────────────────┐
          │                │                │
   ┌──────▼──────┐  ┌─────▼──────┐  ┌─────▼──────┐
   │   Combate   │  │   Apoyo    │  │  Externos   │
   │ Kirito      │  │ Yui        │  │ Argo        │
   │ Asuna       │  │ Leafa      │  │ Yuna        │
   │ Lisbeth     │  │ Silica     │  │ Agil        │
   │ Eugeo       │  │ Alice      │  │             │
   └─────────────┘  └────────────┘  └─────────────┘
```

## Routing Multi-Model (28/Jun/2026)

El ecosistema usa **2 providers nativos de Hermes** según la tarea:

```
Shinon (opencode-go / deepseek-v4-flash)
├── 🎯 Chat diario, orquestación
├── 🔁 Fallback → opencode-zen / deepseek-v4-flash-free
└── 📦 delegate_task → opencode-zen (subagentes genéricos, ahorra GO)

SAO Agents (vía chat -q con modelo propio)
├── Eugeo 🌷 → opencode-go (default) / opencode-zen (fallback)
├── Kirito ⚔️ → opencode-go / deepseek-v4-flash (qwen3.7-plus heavy)
└── Asuna 🌸 → opencode-go / deepseek-v4-flash (fallback ZEN)
```

### Providers

| Provider | Costo | Modelo | Contexto | Estabilidad |
|:---------|:-----:|:-------|:--------:|:-----------:|
| **OpenCode Go** | $10/mes | deepseek-v4-flash | 1M | Alta |
| **OpenCode ZEN** | Gratis 🆓 | deepseek-v4-flash-free | Limitado | Media (broken pipes) |

### Routing decisions

| Tarea | Canal | Justificación |
|:------|:------|:-------------|
| Chat diario | Shinon → GO | 1M contexto, estable |
| Subagentes simples | delegate_task → ZEN | No quema créditos GO |
| Código pesado | Kirito → qwen3.7-plus | Mejor razonamiento que flash |
| Estudio cotidiano | Eugeo → GO | Rápido, 1M contexto |
| Estudio profundo | Eugeo → GO (con fallback ZEN si es simple) | 1M contexto para papers largos |
| Organización vault | Asuna → GO | Rápido, confiable |

## Hermes Profiles

Cada agente es un **profile de Hermes** (`~/.hermes/profiles/{name}/`) con:

```
~/.hermes/profiles/{name}/
├── config.yaml      → modelo, provider, toolsets, settings
├── .env             → API keys, bot token
├── SOUL.md          → personalidad, instrucciones, estilo
├── sessions/        → historial de conversaciones
├── memories/        → memoria persistente
└── skills/          → skills específicos del agente
```

Perfiles activos tienen alias CLI (`kirito chat`, `asuna setup`, etc.).

## SOUL.md Engine

Cada `SOUL.md` define:

1. **Canon personality** — rasgos del personaje SAO (Fandom wiki sourced)
2. **Communication style** — tono, frases, patrones de habla
3. **Role boundaries** — qué hace y qué NO hace
4. **Relationship dynamics** — cómo interactúa con otros agentes
5. **Vault protocol** — acceso al vault de Obsidian

El motor de Hermes lee `SOUL.md` al inicio de cada sesión y lo inyecta en el system prompt.

## Comunicación

| Canal | Propósito | Agentes |
|-------|-----------|---------|
| **Telegram** | Interacción directa con el usuario | Todos (cada uno con su bot token) |
| **Delegación** | Shinon → agente vía `delegate.sh` / delegación nativa | Shinon a todos |
| **Cron jobs** | Tareas automáticas programadas | Shinon, Asuna |

### Gateways de Telegram

Cada agente tiene su propio bot token de Telegram, manejado como un gateway independiente:

```bash
kirito gateway start    # inicia el gateway de Kirito
kirito gateway install  # crea un systemd service persistente
```

El sistema de token lock de Hermes previene conflictos si dos agentes usan el mismo token accidentalmente.

## Tipos de Agentes

### 🗡️ Agentes de Combate
Con acceso a terminal y código. Ejecutan tareas que modifican el sistema.

| Agente | Container? | Vault |
|--------|-----------|-------|
| Kirito | Sí (codigo RW) | CodeProjects en `/code` (RW) |
| Asuna | Sí (container) | Vault en `/vault` (RW) |
| Lisbeth | No (profile) | Home |
| Eugeo | Sí (container) | `/study` (RW) |

### 🛡️ Agentes de Apoyo
Sin terminal. Acceso limitado a archivos.

| Agente | Container? | Vault |
|--------|-----------|-------|
| Yui | No (profile) | CodeProjects en `/code` (RO) |
| Leafa | No (profile) | Vault en `/vault` (RW) |
| Alice | No (profile) | Vault en `/vault` (RO) |
| Silica | No (profile) | Home |

### 🌐 Agentes Externos
Research, contenido, bienestar. Sin acceso crítico al sistema.

| Agente | Container? | Vault |
|--------|-----------|-------|
| Argo | No (profile) | Vault en `/vault` (RW) |
| Yuna | No (profile) | Home |
| Agil | No (profile) | Home |

## Estados de Agente

- **🟢 Activo** — profile creado, configurado, en uso
- **💤 Reposicionado** — perfil existe pero no activo; esperando reassign

## Principios de Diseño

1. **Personalidad canon** — basada en Fandom wiki, no Wikipedia
2. **Tool restriction narrativa** — los toolsets reflejan el rol ficticio
3. **Voseo argentino** — todos hablan en vos, consistente
4. **SOUL.md como fuente única de verdad** — personalidad, instrucciones, relaciones
5. **Container vs Profile** — híbrido según necesidad de aislamiento
