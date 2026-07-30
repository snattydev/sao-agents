# SAO Agents — Roadmap

> This is a living document. ~~Strikethrough~~ marks things that changed direction as I learned. What's here isn't a promise — it's a record of where I thought things were going and where they actually went.

---

## Fase 1: Fundación ✅

- [x] ~~Arquitectura definida (containerized agents + profiles)~~ → Architecture settled on native profiles with containers as production ideal
- [x] SOUL.md para todos los agentes del roster
- [x] ~~Gateways de Telegram operativos~~ → Gateways operativos para el perfil principal y los activos
- [x] ~~Hermes profiles reference documentado~~ → SOUL.md y setup guide documentados

## Fase 2: Perfiles Activos

- [x] Shinon (default) configurado como orquestador
- [x] ~~Kirito operativo con deepseek-v4-flash~~ → Engineering profile creado, evaluado, y su approach incorporado en la arquitectura
- [x] ~~Asuna operativa con organización de vault~~ → Profile de organización funcionando con vault access
- [x] ~~Eugeo operativo con gateway de Telegram~~ → Study profile con gateway activo
- [x] ~~Sistema de delegación multi-agente funcionando estable~~ → Mecanismo de coordinación entre agentes implementado y en evolución
- [ ] Documentación del ecosistema → iteración continua

Lo que aprendí: ~~tener 12 agentes activos era overkill~~. La arquitectura se consolidó alrededor de un núcleo más chico, con el roster completo documentado como diseño conceptual. Los perfiles existen cuando tienen un propósito claro, no por completitud.

## Fase 3: Klein — Relay Agent 🤝

- [ ] ~~Diseñar SOUL.md para Klein (SAO canon)~~ → Klein sigue en diseño conceptual
- [ ] ~~Crear profile de Hermes~~ → Pendiente de definir si el rol agrega valor al ecosistema actual
- [ ] ~~Configurar gateway~~ → Requiere hardware/VM secundario

Klein fue pensado como el primer agente externo al equipo original. El concepto sigue siendo interesante — un agente relay liviano que opere desde otro dispositivo — pero la prioridad cambió a consolidar el núcleo existente primero.

## Fase 4: VPS — Despliegue Remoto 🌐

- [ ] ~~Adquirir VPS~~ → Evaluado, postergado. El setup actual cumple para single-user
- [ ] ~~Migrar profiles activos al VPS~~ → Pendiente de decidir si la arquitectura multi-host agrega valor hoy
- [ ] ~~Gateways 24/7~~ → Los gateways activos ya corren 24/7 en local

La lección: no necesitaba un VPS para tener disponibilidad. Los servicios core ya están corriendo localmente.

## Fase 5: Expansión 🚀

- [ ] ~~Reactivar agentes reposicionados~~ → Varios agentes fueron evaluados y sus skills/dominios reabsorbidos en otros perfiles o en automatizaciones directas
- [ ] ~~Dashboard de monitoreo~~ → Reemplazado por health checks automáticos
- [x] Automatización de mantenimiento (health checks, reindex de vault, briefings diarios)
- [ ] Canal de Discord — sigue en evaluación

---

## Lo que sigue (sin fecha)

- Seguir iterando la arquitectura a medida que aprendo
- Explorar patrones de delegación más limpios entre agentes
- El proyecto integrador que unifica todo esto — cuando esté listo, será público
