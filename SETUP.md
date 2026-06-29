# SAO Agents — Setup Guide

## Requisitos

- [Hermes CLI](https://hermes-agent.nousresearch.com) instalado
- API keys en `~/.hermes/.env`:
  - `OPENCODE_GO_API_KEY` — proveedor principal (pago: ~$10/mes según uso)
  - `OPENCODE_ZEN_API_KEY` — proveedor secundario (gratis, rate limited)
- Tokens de bot de Telegram para cada agente (opcional)
- Obsidian vault (opcional, para agents con vault access)

## Proveedores

El ecosistema usa **2 providers nativos de Hermes** más un proxy opcional:

| Provider | Costo | Modelo | Contexto | Estabilidad |
|:---------|:-----:|:-------|:--------:|:-----------:|
| **OpenCode Go** | $10/mes aprox | deepseek-v4-flash | 1M | Alta |
| **OpenCode ZEN** | Gratis 🆓 | deepseek-v4-flash-free | Limitado | Media (broken pipes) |
| **FreeLLMAPI** 🔄 | Gratis 🆓 | Gemini 3.5 Flash, GPT-4.1, DS V4 Pro y +50 modelos | Variable | Según provider |

FreeLLMAPI (https://freellmapi.co) es un proxy auto-hosteable que une los tiers gratis de 17 providers. Opcional — ver `personal/tecnologia/freellmapi.md` en la vault.

## Instalación Rápida

```bash
# 1. Clonar el repo
git clone <repo-url> ~/.hermes/sao-agents
cd ~/.hermes/sao-agents

# 2. Crear profiles para los agentes activos
for agent in kirito asuna eugeo; do
  hermes profile create "$agent" --clone
done

# 3. Copiar SOUL.md de cada agente
for agent in kirito asuna eugeo; do
  cp "profiles/$agent/SOUL.md" ~/.hermes/profiles/$agent/SOUL.md
done

# 4. Configurar modelos según arquitectura multi-model
# Kirito → opencode-go / deepseek-v4-flash + qwen3.7-plus heavy
hermes -p kirito config set model.default deepseek-v4-flash
hermes -p kirito config set model.provider opencode-go
hermes -p kirito config set model.base_url https://opencode.ai/zen/go/v1

# Asuna → opencode-go / deepseek-v4-flash
hermes -p asuna config set model.default deepseek-v4-flash
hermes -p asuna config set model.provider opencode-go
hermes -p asuna config set model.base_url https://opencode.ai/zen/go/v1

# Eugeo → opencode-zen / deepseek-v4-flash-free (gratis, para chat cotidiano)
hermes -p eugeo config set model.default deepseek-v4-flash-free
hermes -p eugeo config set model.provider opencode-zen
hermes -p eugeo config set model.base_url https://opencode.ai/zen/v1

# 5. Verificar
hermes profile list
```

## Configuración por Agente

### Shinon (default)
```bash
# Shinon usa el profile default de Hermes
hermes config set model.default deepseek-v4-flash
hermes config set model.provider opencode-go
hermes config set model.base_url https://opencode.ai/zen/go/v1
hermes config set fallback_providers '["opencode-zen"]'

# Delegación → ZEN free para subagentes (ahorra GO)
hermes config set delegation.provider opencode-zen
hermes config set delegation.model deepseek-v4-flash-free
```

### Kirito (Engineering)
```bash
kirito config set model.default deepseek-v4-flash
kirito config set model.provider opencode-go
kirito config set model.base_url https://opencode.ai/zen/go/v1

# Habilita delegation para subagentes con modelo según tarea
kirito config set agent.max_turns 90
```
Requiere skill `subagent-model-routing` para elegir modelo según complejidad:
- `delegate_task` → deepseek-v4-flash (simple)
- `terminal(hermes chat -q --model qwen3.7-plus)` → código pesado

### Asuna (Organization)
```bash
asuna config set model.default deepseek-v4-flash
asuna config set model.provider opencode-go
asuna config set model.base_url https://opencode.ai/zen/go/v1

# Sin delegation ni terminal — solo organización
asuna config set toolsets.enabled '[file, search, web, browser]'
```

### Eugeo (Study)
```bash
eugeo config set model.default deepseek-v4-flash
eugeo config set model.provider opencode-go
eugeo config set model.base_url https://opencode.ai/zen/go/v1

# Fallback a ZEN free
eugeo config set fallback_providers '["opencode-zen"]'

# Gateway de Telegram
eugeo gateway install
```

### Agentes Reposicionados

Silica (finanzas) y Agil (fitness) están **reposicionados** desde 28/Jun/2026 — perfiles preservados, esperando reassign. Para reactivar:

```bash
hermes profile use silica
hermes profile use agil
```

### Agentes Reposicionados

Alice, Argo, Leafa, Lisbeth, Yui, Yuna tienen sus SOUL.md en `profiles/<agente>/` del repo. Para restaurar:

```bash
hermes profile create alice --clone
cp profiles/alice/SOUL.md ~/.hermes/profiles/alice/SOUL.md
```

## Skills importantes

| Skill | Dónde está | Para qué |
|:------|:-----------|:---------|
| `subagent-model-routing` | `~/.hermes/skills/` | Elegir modelo según tipo de tarea (6 modelos) |
| `sao-roster-delegation` | `~/.hermes/skills/` | Cómo delegar a cada agente del roster |

## Gateways de Telegram

```bash
# Por agente
eugeo gateway install   # persistente via systemd

# Ver estado
hermes -p eugeo gateway status
```

Cada agente necesita un bot token único en su `.env`:
```bash
echo "TELEGRAM_BOT_TOKEN=tu_token_aqui" >> ~/.hermes/profiles/eugeo/.env
```

## Vault de Obsidian

```bash
# Asuna (RW)
mkdir -p ~/.hermes/profiles/asuna/vault
ln -s /ruta/a/tu/vault ~/.hermes/profiles/asuna/vault
```

## Verificación

```bash
# Listar todos los perfiles
hermes profile list

# Probar un agente
kirito chat -q "Decime quién soy"

# Ver health del gateway
hermes -p eugeo gateway status
```
