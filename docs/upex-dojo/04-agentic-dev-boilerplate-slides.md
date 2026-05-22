# Agentic Dev Boilerplate — Presentación 18 slides

> Notas de la presentación visual en
> `https://www.upexgalaxy.com/presentation/agentic-dev-boilerplate`
>
> La presentación está dividida en **4 actos**. Cada acto contesta una
> pregunta distinta. Estas notas no resumen slide por slide — eso ya
> está en el doc canónico (archivo 03). Acá guardo solo lo que la
> presentación agrega o muestra mejor que el texto.
>
> Fecha de lectura: 20 de mayo de 2026

---

## Los 4 actos

| Acto | Slides | Pregunta que contesta |
|------|--------|----------------------|
| 1 — Fundamentos | 3–5 | ¿Qué es esto y con quién hablo? |
| 2 — Anatomía | 6–10 | ¿Qué piezas tiene adentro? |
| 3 — En acción | 11–14 | ¿Cómo lo uso día a día? |
| 4 — Cierre | 15–18 | ¿Qué NO toco y dónde sigo? |

---

## Las 5 ideas que valen más que las otras 13

### Idea 1 — Skills, Commands y Scripts (slide 6)

Son **tres tipos de piezas** del repo, con tres dueños distintos:

| Pieza | Quién decide | Ejemplo |
|-------|--------------|---------|
| **Skill** | La IA (auto-trigger por match) | `sprint-development` |
| **Command** | Yo (lo invoco con `/nombre`) | `/sync-ai-memory` |
| **Script** | Yo (lo tipeo en terminal) | `bun run setup` |

**Regla mnemotécnica:**
> Skill = la IA decide. Command = yo decido. Script = yo tipeo.

---

### Idea 2 — Personalidad de la IA: el "PM Voice" por defecto (slide 5)

La IA del boilerplate **no me habla como dev senior por defecto**:
me habla como **Project Manager**. Traduce código a valor de negocio.

Si quiero que me hable técnico tengo que pedirlo:
> "modo técnico" o "hablá técnico"

### Otras seis estrategias de comunicación

- **Caveman mode** — recorta ~75% de palabras. Útil para ahorrar tokens.
- **Butler Pattern** — respuesta corta primero, después menú de temas.
- **Background-narrator** — en segundo plano avisa con `result:`,
  `needs input:`, `failed:`.
- **Language mirror** — me responde en mi idioma; archivos (código,
  PRs, Jira) quedan en inglés.
- **Visual Mapping Bias** — si se puede mapear, prefiere tabla/diagrama
  antes que prosa.

**Por qué importa:** son palancas de control conocidas. No voy a pelear
con la IA, voy a saber qué palabras disparan qué modo.

---

### Idea 3 — Las 5 fases del ciclo de vida (slide 7)

Esta es **la columna vertebral** del repo:

```
0. Bootstrap     →  una vez por clon         (instalar)
1. Foundation    →  una vez por producto     (definir producto)
2. Scaffold      →  una vez post-Foundation  (cablear Next.js+Supabase)
3. Daily Dev     →  por ticket / continuo    ← donde vivo el 80%
4. Maintenance   →  al detectar drift        (cuando docs ≠ realidad)
```

**Lo más importante:** la fase 3 (Daily Dev) se dispara con
`/sprint-development`. Eso significa: el flujo
"ticket Jira → plan → código → review → deploy a staging → hand-off a QA"
**es un solo comando.**

---

### Idea 4 — La máquina de estado de Jira (slide 9)

Cuatro estados, cuatro transiciones automáticas:

```
Ready For Dev → In Progress → In Review → Ready For QA
                  [Plan OK]   [PR abierto]  [staging verde]
```

**Nota muy importante (la slide lo marca en rojo):** el repo **nunca
llega a "Done"**. Done es responsabilidad del repo gemelo
`agentic-qa-boilerplate`.

**Mi conexión:** cuando llegue a Clases 5–7 del Dojo, voy a vivir
**del otro lado de esta máquina de estados**, validando los tickets
que el dev tira a `Ready For QA`.

---

### Idea 5 — Modelo mental TL;DR (slide 17)

Si tengo que retener UNA sola cosa de toda la presentación, es esta:

```
Skills        = scripts teatrales para la IA (multi-acto, con personajes)
Commands      = utilidades de un solo acto que yo llamo
Scripts       = yo los corro en la terminal
.context/     = lo que la IA SABE del proyecto (memoria)
Application   = el producto real (lo que se construye)
```

Y el orden de uso en proyecto nuevo:

```
1) project.yaml  →  2) /project-foundation  →  3) /project-bootstrap  →  4) /sprint-development
```

---

## Lo que hay que saber pero no memorizar

Las slides 10, 11, 14, 15, 16 son **de referencia**. Útiles cuando ya
esté operando el repo. No para entender ahora.

### Slide 10 — Tres circuitos

Cómo conectan variables, orquestador y comandos shell entre sí.

- Variables `{{VAR}}` se resuelven desde `.agents/project.yaml`.
- 4 sintaxis de variables:
  - `{{VAR_NAME}}` — config estática a nivel proyecto.
  - `{{environments.x}}` — referencia cross-env.
  - `<<VAR_NAME>>` — computada en runtime, no persiste.
  - `{{jira.<slug>}}` — referencia a custom fields de Jira.
- El resto es plomería.

### Slide 11 — Sprint vs SDD

- **Path A** (`/sprint-development` solo): ticket estándar (<400 líneas,
  sin nueva arquitectura).
- **Path B** (`/sprint-development + SDD bundle`): ticket complejo
  (>400 líneas, refactor multi-archivo, nueva arquitectura).
- **Standalone** (`/sdd-*` solo): trabajo exploratorio sin ticket
  todavía.

**Vale saber:** SDD = "Spec-Driven Development". Para tickets normales,
sprint-development solo basta.

### Slide 14 — Commands & Scripts

Catálogo. Útil de tener cerca cuando empiece a tocar.

### Slide 15 — Piezas que NUNCA invoco directamente

4 categorías de cosas que la IA carga sola y yo no llamo directo:

- Tool / community skills (cargadas por workflow skills).
- `agentic-dev-core/references/*` (doctrina compartida).
- SDD orchestrator + SDD skills (instaladas por gentle-ai a nivel
  usuario, no en este repo).
- **Engram (MCP persistent memory)** — la memoria que reemplaza tener
  que reexplicarle todo a Claude cada vez.

### Slide 16 — MCPs disponibles

5 herramientas externas:

| MCP | Para qué |
|-----|----------|
| **Context7** | Docs oficiales de librerías y frameworks |
| **Tavily** | Búsqueda web, soluciones de comunidad |
| **Supabase** | Queries de DB, schema, estado del proyecto |
| **n8n** | Automatización de workflows |
| **Atlassian** | Jira + Confluence (tickets, transitions, custom fields) |

**Las que conozco del Dojo:** Context7 y Atlassian. Las otras tres son
contexto, no tarea para hoy.

---

## Detalle adicional de la slide 8: Foundation host vs Project scaffolding

Esta slide importa porque distingue dos cosas que suenan parecidas:

| | `agentic-dev-core` | `/project-bootstrap` |
|---|---|---|
| **Rol** | Host pasivo de doctrina | Skill de workflow que andamia mi codebase |
| **Cuándo se invoca** | Nunca directamente | Una vez por proyecto, DESPUÉS de `/project-foundation` |
| **Quién lo usa** | Otros skills lo citan automáticamente | Yo lo invoco a mano |

**Regla:** la doctrina es pasiva, el scaffolding es activo. **No son
intercambiables.**

---

## Cómo me ayuda esto en 3impacto

No puedo trasplantar el boilerplate a 3impacto (3impacto corre en
Lovable, no en Claude Code + Next.js + Supabase). Pero hay **tres
palancas que sí puedo bajar** — ver archivo 05.

---

## Cómo me ayuda esto en el Dojo

### Para Clase 1 (asimilación pendiente)

La presentación me confirma tres conceptos con material visual:

1. **Context engineering progresivo** (Síntesis 5) → slide 10.
2. **Jerarquía de instrucciones** (Síntesis 4) → trío `CLAUDE.md` +
   `CONTEXT.md` + `DESIGN.md`.
3. **System prompt** (concepto 4, todavía no escrito) → slide 5
   completa. Esta slide me va a ahorrar trabajo cuando escriba la
   síntesis de ese concepto.

### Para Clase 2 (donde estoy ahora)

La presentación muestra lo que Ely no alcanzó a mostrar en vivo: el
flujo completo de shift-left desde el lado dev. Cuando arme la nota
`02-clase-02-shift-left-bunkai.md` para el repo, puedo citar
especialmente la **slide 9 (máquina de estado Jira)**.

### Para Clases 5–11

El repo gemelo `agentic-qa-boilerplate` tiene la misma estructura pero
del lado QA. Cuando llegue a Clase 5 (Playwright E2E), voy a estar
viviendo en ese repo. Esta presentación es el espejo invertido: lo que
yo valido como QA es lo que esta presentación describe del lado dev.

---

## Referencias

- Presentación: `https://www.upexgalaxy.com/presentation/agentic-dev-boilerplate`
- Documento canónico: archivo `03-agentic-dev-boilerplate-doc.md`
- Síntesis aplicada a 3impacto: archivo `05-palancas-3impacto.md`
