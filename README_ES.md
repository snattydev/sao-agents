# SAO Agents 🏹⚔️🌸🎓

[English](README.md) / [Español](README_ES.md)

> 🚧 **Proyecto Personal de Aprendizaje** — Este repositorio es parte de una exploración continua sobre personalidad y orquestación de agentes de IA. Actualmente estamos desarrollando un proyecto integrador que será público cuando esté listo.
>
> ©️ **Copyright** — _Sword Art Online_ es propiedad de Reki Kawahara, A-1 Pictures y Aniplex. Este es un proyecto fan-made de aprendizaje sin fines comerciales. No está afiliado ni respaldado por los titulares de derechos.

![Status](https://img.shields.io/badge/status-active-7ED3C1?style=flat-square)
![Platform](https://img.shields.io/badge/platform-Hermes%20Profiles-31748f?style=flat-square)

> Un ecosistema de **agentes de IA con personalidad**, inspirado en _Sword Art Online_.  
> Cada agente está definido por un `SOUL.md` — un archivo de personalidad que establece su rol, voz, límites y dominio de expertise.

---

## 📋 Agentes

| # | Agente | Rol | Compute | Toolsets clave |
|---|--------|-----|:-------:|----------------|
| 🏹 | **Shinon** | Host y Orquestadora | Liviano | web, browser, terminal, file, code, vision, delegación, cron, memoria |
| ⚔️ | **Kirito** | Ingeniería | Pesado — código y arquitectura | terminal, file, web, delegación |
| 🌸 | **Asuna** | Organización y Vault | Liviano | file, web, browser, terminal |
| 🎓 | **Eugeo** | Estudio e Investigación | Liviano + Visión | file, web, browser, vision, terminal |
| 🌿 | **Leafa** | Contenido y Creatividad | Liviano | web, vision |
| ⚖️ | **Alice** | Social y Comunidad | Liviano | web, file, vision |
| 🔧 | **Lisbeth** | Tooling y DevOps | Liviano | terminal, file, web |
| 🐉 | **Silica** | Finanzas y Datos | Liviano | file, web |
| 🐀 | **Argo** | Viajes e Investigación | Liviano | web, file |
| 💻 | **Yui** | Review y QA | Pesado — análisis | file(ro), web, vision |
| 🎤 | **Yuna** | Música y Audio | Liviano | web, tts, spotify, vision |
| 💪 | **Agil** | Fitness y Salud | Liviano | web, file |

> Todos los agentes siguen el mismo patrón arquitectónico — un `SOUL.md` que define personalidad y dominio, junto con acceso a herramientas apropiadas. La columna "Compute" da una idea del tipo de modelo necesario, no un modelo específico.

> ⚠️ **Nota de seguridad:** Este es un setup mono-usuario — los agentes corren directamente en mi estación de trabajo con acceso amplio a herramientas porque soy el único que interactúa con ellos. En un entorno multi-usuario o de producción, convendría usar aislamiento por contenedores, credenciales acotadas y filesystems de solo lectura. La arquitectura con contenedores discutida en [`ARCHITECTURE.md`](./ARCHITECTURE.md) representa ese ideal de producción.

---

## 💡 Nota Personal

En mi setup personal uso **deepseek-v4-flash** para la charla diaria y orquestación — encuentra el punto justo entre velocidad, contexto y costo. Modelos más pesados aparecen para código complejo o investigación profunda. Pero este repo es sobre la **capa de personalidad y arquitectura**, no sobre el modelo subyacente. Cambiá el modelo por el que mejor se ajuste a tus necesidades y presupuesto.

---

## 🏗️ Stack

| Componente | Tecnología |
|------------|-----------|
| **Runtime** | [Hermes Agent](https://hermes-agent.nousresearch.com) (profiles nativos) |
| **Comunicación** | Terminal / Gateways (Telegram, etc.) |
| **Arquitectura** | Profiles — cada agente es un perfil independiente con su propia identidad |
| **Diseño** | `SOUL.md` — personalidad como configuración, inspirada en personajes de SAO |

Cada agente es un profile de Hermes independiente. Su `SOUL.md` actúa como system prompt — define quién es el agente, cómo habla, qué maneja y qué está fuera de sus límites.

---

## 🚀 Cómo empezar

1. **Elegí un agente** — leé su `SOUL.md` en `profiles/<agente>/`
2. **Cargalo en tu runtime** — la mayoría de los runtimes aceptan un system prompt o archivo de personalidad
3. **Configurá sus herramientas** — dale acceso a lo que necesita según su rol (archivos, web, terminal, etc.)
4. **Usalo** — iniciá una sesión y deja que la personalidad guíe la interacción

Los `SOUL.md` de este repo son autónomos. Agarrá el que se ajuste a tu caso, configuralo en tu plataforma de agentes, y listo.

Ver [`AGENTS.md`](./AGENTS.md) para los perfiles de personalidad completos.  
Ver [`ARCHITECTURE.md`](./ARCHITECTURE.md) para el razonamiento detrás del diseño.

---

## 🔄 Comunicación entre agentes

Los agentes pueden coordinarse entre sí mediante los mecanismos de delegación o mensajería de su runtime. Cada sesión es independiente — los agentes no comparten memoria a menos que estén explícitamente conectados.

Cuando un agente necesita a otro, se identifica y pasa contexto. El agente receptor actúa con su propia personalidad y herramientas.

---

## 🗺️ Roadmap

Ver [`ROADMAP.md`](./ROADMAP.md) — el proyecto evoluciona a medida que aprendo. La arquitectura ha cambiado múltiples veces y seguirá cambiando.

---

> 🏹 _私が後ろにいる — 君は落ちない._
