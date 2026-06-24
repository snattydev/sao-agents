# SAO Agents — Setup Guide

## Requisitos

- [Hermes CLI](https://hermes-agent.nousresearch.com) instalado
- API keys para los modelos que uses (opencode-go, kimi-k2.6, etc.)
- Tokens de bot de Telegram para cada agente (opcional)
- Obsidian vault (opcional, para agents con vault access)

## Instalación Rápida

```bash
# 1. Clonar el repo
git clone <repo-url> ~/.hermes/sao-agents
cd ~/.hermes/sao-agents

# 2. Crear profiles para los agentes activos
for agent in kirito asuna eugeo silica agil; do
  hermes profile create "$agent" --clone
done

# 3. Copiar configs y SOUL.md
for agent in kirito asuna eugeo silica agil; do
  cp "profiles/$agent.md" ~/.hermes/profiles/$agent/SOUL.md
  # Ajustar config.yaml según necesites
  hermes -p "$agent" config set model.default <modelo-correspondiente>
done

# 4. Verificar
hermes profile list
```

## Configuración por Agente

### Shinon (default)
```bash
# Shinon usa el profile default de Hermes
hermes config set model.default deepseek-v4-flash
hermes config set terminal.cwd ~
```

### Kirito (Engineering)
```bash
kirito config set model.default deepseek-v4-pro
kirito config set terminal.cwd ~/Projects
```

### Asuna (Organization)
```bash
asuna config set model.default deepseek-v4-flash
asuna config set terminal.cwd ~/Documents
```

### Eugeo (Study)
```bash
eugeo config set model.default qwen3.6-plus
eugeo gateway install  # para tenerlo siempre disponible
```

### Silica (Finance)
```bash
silica config set model.default minimax-m2.5
```

### Agil (Fitness)
```bash
agil config set model.default deepseek-v4-flash
```

## Gateways de Telegram

```bash
# Por agente
kirito gateway start
kirito gateway install   # persistente via systemd

# Ver estado
kirito gateway status
```

Cada agente necesita un bot token único en su `.env`:

```bash
echo "TELEGRAM_BOT_TOKEN=tu_token_aqui" >> ~/.hermes/profiles/kirito/.env
```

## Liberar Agentes Reposicionados

Los agentes en estado 💤 tienen sus `SOUL.md` en `profiles/liberated/`. Para reactivar:

```bash
hermes profile create alice --clone
cp profiles/liberated/alice/SOUL.md ~/.hermes/profiles/alice/
alice config set model.default glm-5.1
```

## Vault de Obsidian

Para agentes con acceso al vault:

```bash
# Asuna (RW)
mkdir -p ~/.hermes/profiles/asuna/vault
ln -s /ruta/a/tu/vault ~/.hermes/profiles/asuna/vault

# Alice (RO)
ln -s /ruta/a/tu/vault ~/.hermes/profiles/alice/vault
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
