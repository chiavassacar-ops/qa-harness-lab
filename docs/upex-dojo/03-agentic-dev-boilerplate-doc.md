# Agentic Dev Boilerplate — Documento canónico

> Notas de lectura del documento `docs/agentic-development-engineering.md`
> del repo `upex-galaxy/agentic-dev-boilerplate` (60 KB, 12 capítulos).
>
> Este es el material que está DETRÁS de la presentación de 18 slides.
> La presentación es la versión visual; este documento es la versión textual completa.
>
> Fecha de lectura: 21 de mayo de 2026

---

## Qué es el boilerplate, en una oración

Una **caja de herramientas lista para usar** para equipos que quieren que
una IA maneje todo el ciclo de desarrollo (de la definición del producto
al deploy) con **checkpoints humanos en cada etapa**.

No es "ponerle IA al editor". Es **la IA conduce el flujo completo y el
humano aprueba en cada paso**.

---

## Por qué existe

Porque los equipos arrancan siempre igual:

- Cero documentación estructurada.
- Cero skills compartidas entre devs.
- La IA olvida todo entre sesiones.
- Un solo chat hace de todo y se vuelve un quilombo.
- Los tickets de Jira tienen tres líneas.

Eso funciona hasta que el producto maneja plata, datos regulados o más
de 3 devs concurrentes. **Ahí explota.** Este boilerplate instala la
infraestructura para que no explote.

---

## Las tres patas de la estrategia

### 1. Spec-Driven

Primero specs, después código. La cadena completa es:

```
Constitution → PRD → SRS → Discovery → DESIGN.md → Épica → Historia → Plan → Código
```

**Conexión con 3impacto:** esto es exactamente lo que yo hago con el
QA Refinement por user story. La diferencia es que en el boilerplate
está formalizado en archivos versionados.

### 2. Skills-first, no prompts

En vez de tener prompts copy-paste, tenés `SKILL.md` versionados en el
repo. La IA carga el que corresponde según lo que le pidas.

**Conexión con Síntesis 5 (Clase 1):** esto es progressive loading puro,
implementado en archivos reales.

### 3. Agéntico

No un solo chat haciendo de todo, sino **un orquestador + subagentes**.
El orquestador decide y delega. Cada subagente hace una tarea chica y
reporta.

---

## Glosario mínimo (los términos que se repiten)

- **Skill** — capacidad reutilizable guardada en `.claude/skills/<nombre>/`.
  Se activa sola cuando lo que pedís coincide con su descripción.
- **Subagente** — trabajador especializado que el orquestador despacha
  para una tarea puntual (leer, escribir, verificar, deployar).
- **Engram** — la memoria persistente que sobrevive entre sesiones.
  Guarda decisiones, convenciones, bugs solucionados.
- **PBI** — la carpeta local por cada ticket donde se guarda todo lo
  relacionado (specs, plan, review, evidencia).

---

## Arquitectura en tres pisos

```
Arriba:      Desarrollador (decide, revisa, aprueba)
                         ↓
En el medio: Skills de IA (foundation, management, implementation)
             + Knowledge Layer (.context/)
                         ↓
Abajo:       Sistemas reales (Jira, Supabase, Vercel, GitHub)
```

---

## Context Engineering: la capa de conocimiento

**Esta es la idea fuerte del documento.** La información del proyecto
está organizada en **tres niveles**:

1. **Nivel proyecto** — PRD, SRS, modelo de negocio, mapa de features,
   tokens de diseño.
2. **Nivel módulo/épica** — contexto del módulo, roadmap de historias.
3. **Nivel historia/ticket** — criterios de aceptación, plan, review,
   matriz de cumplimiento.

Todo vive en una carpeta `.context/` versionada. **La IA lee lo que
necesita y solo eso.**

**Esto es Síntesis 5 hecha repositorio.**

---

## Cómo se trabaja en el día a día

El dev habla en castellano y la skill correcta se activa sola:

| Lo que tipeás | Skill que se activa |
|---------------|---------------------|
| "implementar UPEX-123" | `sprint-development` |
| "agregar feature al backlog: los users pueden exportar" | `product-management` |
| "creá rama para UPEX-789" | `git-flow-master` |
| "abrí un PR contra staging" | `git-flow-master` |
| "sprint report" | `product-management` (modo lectura) |

**No tenés que recordar comandos.** La IA matchea la intención con la
descripción de la skill.

---

## El modelo de orquestación: IA trabaja, humano decide

Este es el corazón del documento. Y va a sonar familiar porque es
**exactamente lo que pasa en 3impacto** entre Maxi 1, Maxi 2 y yo:

```
Orquestador → despacha → Subagente PLANIFICA → ● checkpoint humano
            → despacha → Subagente CODIFICA   → ● checkpoint humano
            → despacha → Subagente REVISA     → ● checkpoint humano
```

### Tres garantías del modelo

1. Cada subagente reporta. Nada queda en silencio.
2. El humano puede frenar, redirigir o modificar en cualquier checkpoint.
3. Todo queda en el transcript, auditable después.

### Por qué los checkpoints

La IA se equivoca. Cazar el error entre etapas evita que se propague.
Una mala decisión en Planificación que llega a Implementación es código
roto. Cazada en el gate de planificación es un cambio de 2 minutos.

**Conexión con Fowler/Böckeler:** esto es **feedforward inferencial
humano** dentro del loop. Es uno de los cuatro tipos de harness del
modelo 2×2.

---

## Los 5 gates de calidad (100% QA)

Toda historia que va a `staging` pasa por:

```
LINT → TYPES → TESTS → REVIEW → DEPLOY
```

Cada uno con su comando, su dueño, y qué pasa si falla.

**Lo más importante:** cuando algo falla, la IA NO auto-arregla. Para,
reporta el fallo con contexto, y ofrece tres opciones al humano:

- Reintentar
- Saltear
- Abortar

**Conexión con mi mapa harness de 3impacto:** esto es **feedback
computacional automatizado** — exactamente el cuadrante que en 3impacto
está vacío o implementado a mano.

---

## Anatomía de una historia (UPEX-XXX, paso a paso)

### 1. Arranque

Dev tipea "implementar UPEX-XXX". La IA:
- Busca contexto anterior en engram.
- Abre el ticket en Jira.
- Explora el código relacionado.

### 2. Stage 1 — Plan

Un subagente planifica, produce `implementation-plan.md`.
- El humano aprueba.
- Jira: `Ready For Dev` → `In Progress`.

### 3. Stage 2 — Implementación

Otro subagente escribe el código. En paralelo corren 3 verificadores:
- lint
- build
- tests

Si algo está rojo: fix loop, máximo 2 iteraciones.

### 4. Stage 3 — Code Review

PR abierto. Un subagente revisor camina la matriz AC-vs-código y
produce `review.md`.
- Jira: `In Progress` → `In Review`.

### 5. Stage 4 — Staging

Merge a staging. Vercel deploya, Supabase migra.
- Jira: `In Review` → `Ready For QA`.

### 6. Stage 5 — Producción

**SOLO si QA aprobó** (del repo gemelo `agentic-qa-boilerplate`) y el
humano confirma. **Nunca automático.**

---

## Cómo se extiende (para saber que se puede)

Tiene hooks documentados para agregar:

- Nuevas skills (con frontmatter estándar)
- Nuevos slash commands
- Nuevas variables de proyecto
- Nuevos custom fields de Jira
- Nuevos MCPs

Todo con scripts de validación:

- `bun run vars:check`
- `bun run jira:check`

**El harness se autoverifica.** Pieza más del rompecabezas.

---

## La promesa final del documento

> *"Una práctica de desarrollo que envía features más rápido, documenta
> cada decisión, recuerda todo entre sesiones, y nunca deploya a
> producción sin un gate humano. Construida sobre la premisa de que
> la IA hace el trabajo mecánico y el ingeniero toma las decisiones."*

---

## Tres conexiones para retener

### 1. Confirma teoría de Clase 1

Mi Síntesis 5 ("progressive loading") y mi Síntesis 4 ("jerarquía de
system prompts") están **implementadas como archivos reales** en este
repo. No son metáfora, son patrón concreto.

### 2. Es el modelo de Fowler hecho enterprise

El patrón "IA trabaja, humano decide con checkpoints" es **literalmente**
feedforward inferencial humano del modelo de Fowler/Böckeler. En 3impacto
está implícito; acá está formalizado y auditado.

### 3. Existe un repo gemelo de QA

`agentic-qa-boilerplate` usa la misma arquitectura `.agents/` pero del
lado QA. Cuando llegue a Clase 5–7 del Dojo, voy a estar viviendo en
ese repo gemelo. Entender este DEV es entender por adelantado la mitad
del puente.

---

## Referencias

- Repo: `https://github.com/upex-galaxy/agentic-dev-boilerplate`
- Documento canónico: `docs/agentic-development-engineering.md`
- Repo gemelo QA: `upex-galaxy/agentic-qa-boilerplate`
- Presentación visual: `https://www.upexgalaxy.com/presentation/agentic-dev-boilerplate`
