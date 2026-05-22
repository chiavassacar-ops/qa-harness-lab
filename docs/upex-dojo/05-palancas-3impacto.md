# Palancas del Agentic Dev Boilerplate aplicadas a 3impacto

> Mi síntesis personal: qué de todo este material puedo bajar
> efectivamente a mi rol de QA en 3impacto, dadas las restricciones
> de la plataforma (Lovable, Knowledge file cerrado, sin control de
> system prompt ni skills).
>
> Este archivo NO resume el boilerplate (eso está en 03 y 04). Acá
> guardo solo lo accionable.
>
> Fecha: 21 de mayo de 2026

---

## La restricción base

**No puedo trasplantar el boilerplate a 3impacto.**

- El boilerplate corre en Claude Code + Next.js + Supabase + Bun.
- 3impacto corre en Lovable, una plataforma cerrada donde el contexto
  se carga vía un Knowledge file.
- No tengo control del system prompt ni puedo agregar skills.

Pero **el stack subyacente es el mismo: Next.js + Supabase + TypeScript**
(ver Engineering Mandate de Maxi 1, layer 4). La aplicación es
técnicamente compatible 1:1 con el boilerplate. Lo que cambia es
**quién maneja el agente** y **cómo se carga el contexto**.

---

## Las 3 palancas que puedo bajar

### Palanca 1 — La jerarquía de capas (de Foundation)

#### El patrón del boilerplate

3 archivos raíz que definen "qué sabe la IA":

| Archivo | Función |
|---------|---------|
| `CLAUDE.md` | Reglas operativas (qué hace, qué no hace) |
| `CONTEXT.md` | Mapa de conocimiento (qué archivos hay y para qué) |
| `DESIGN.md` | Identidad visual (tokens, paleta, tipografía) |

#### El estado actual en 3impacto

| Archivo del boilerplate | Equivalente en 3impacto | Estado |
|---|---|---|
| `CLAUDE.md` | Engineering Mandate (de Maxi 1) | ✅ Existe |
| `DESIGN.md` | UX/Content Rules | ✅ Existe |
| `CONTEXT.md` | (nada) | ❌ Hueco |

#### El hueco accionable

**No hay `CONTEXT.md`** en 3impacto. No hay un mapa que le diga a la
IA "este es el inventario de specs, dónde vive cada cosa y para qué
sirve".

#### Mi hipótesis de AGENTS.md para Lovable

Como Lovable no me deja tener archivos separados, mi `AGENTS.md` debería
**colapsar los 3 archivos en uno**, con un orden claro:

```
1. CONTEXT  — mapa de qué hay y dónde (resuelve el hueco actual)
2. RULES    — reglas operativas (equivalente a CLAUDE.md)
3. DESIGN   — tokens visuales (equivalente a DESIGN.md)
```

**Por qué este orden:** el mapa primero, porque sin saber qué existe,
las reglas son aire. Las reglas después, porque modulan cómo usar el
mapa. Los tokens al final, porque son detalle aplicable solo cuando
ya hay decisión técnica tomada.

#### Próximo paso

Drafteo del `AGENTS.md` v1 con este patrón en una sesión próxima.

---

### Palanca 2 — La máquina de estado Jira (de Daily Dev)

#### El patrón del boilerplate (slide 9)

```
Ready For Dev → In Progress → In Review → Ready For QA
                  [Plan OK]   [PR abierto]  [staging verde]
```

Cada transición es **automática** y disparada por un evento
verificable (plan aprobado, PR abierto, staging deploy verde).

#### El estado actual en 3impacto

**No lo sé.** Y este es exactamente el tipo de pregunta operacional
que conviene preguntar.

Preguntas para mapear el estado real:

1. ¿Qué transiciones de Jira están automatizadas hoy en 3impacto?
2. ¿Cuáles las dispara una persona a mano (Maxi 1 o Maxi 2)?
3. ¿Hay eventos verificables atados a las transiciones, o son
   manuales sin gate técnico?

#### Por qué importa

Cada transición manual sin gate verificable es **harness computacional
automatizado que falta**. Es decir: es la columna del cuadrante
"feedback computacional" de mi mapa Fowler/Böckeler que está vacía
o implementada con discreción humana.

#### Próximo paso

Mapear las transiciones reales antes de proponer automatización. **No
proponer harness sin diagnóstico.**

---

### Palanca 3 — El PM Voice por defecto (de Personalidad)

#### El patrón del boilerplate (slide 5)

La IA del boilerplate habla por defecto en **PM Voice**: traduce código
a valor de negocio. Para hablar técnico hay que pedirlo explícitamente
("modo técnico" o "hablá técnico").

#### Por qué importa en 3impacto

3impacto es un equipo de 3 personas con voces muy distintas:

| Persona | Rol | Voz que necesita |
|---------|-----|------------------|
| Maxi 1 | CEO/PO/PM | Valor de negocio, sin jerga técnica |
| Maxi 2 | PM/DEV | Técnica detallada |
| Carlos (yo) | QA shift-left | Mixta, según contexto (refinamiento vs validación) |

**Pregunta para el `AGENTS.md`:** ¿la IA de Lovable habla igual con los
tres? Si sí, ahí hay un problema que el Knowledge file puede arreglar
con instrucciones de voz por interlocutor.

#### Idea concreta para el AGENTS.md

Sección de "tono según interlocutor":

```markdown
## Cuándo hablar PM Voice
- Cuando el prompt viene de Maxi 1 o pregunta por valor/impacto.

## Cuándo hablar técnico
- Cuando el prompt viene de Maxi 2 o pregunta por implementación.

## Cuándo hablar QA-mixto
- Cuando el prompt habla de criterios de aceptación, refinamiento o validación.
```

#### Próximo paso

Validar con Maxi 1 si está OK que la IA de Lovable tenga este
comportamiento diferenciado. Es una decisión de producto, no técnica.

---

## Tres preguntas que me quedan abiertas

No las contesto solo. Son las que valdría escribir en el cuaderno antes
de avanzar:

### 1. Sobre AGENTS.md para Lovable

Si el Knowledge file colapsa `CLAUDE.md` + `CONTEXT.md` + `DESIGN.md`
en uno solo, ¿el orden propuesto (CONTEXT → RULES → DESIGN) es
correcto? ¿O conviene RULES primero porque son las que más
"interrumpen" si fallan?

### 2. Sobre la máquina de estado Jira en 3impacto

¿Qué transiciones están automáticas y cuáles las dispara alguien a
mano? (Esto no lo sé sin preguntar — y es legítimo preguntar.)

### 3. Sobre la voz de la IA en Lovable

¿Maxi 1 y Maxi 2 perciben hoy que la IA les habla igual o distinto?
Si es igual, ¿les sirve? Si lo perciben distinto, ¿cómo describirían
la diferencia?

---

## Lo que NO voy a hacer ahora

Por disciplina, dejo afuera de esta tanda:

- ❌ Pedir acceso GitHub a Maxi 2 (todavía no es el momento, la
  pregunta sigue abierta).
- ❌ Proponer el AGENTS.md a Maxi 1 (primero lo drafteo, después
  lo presento con artefacto en mano).
- ❌ Replicar el boilerplate completo (no aplica al stack Lovable).
- ❌ Re-abrir la conversación de Lovable en el Slack del Dojo (ver
  memoria: Ely valora la concisión, dejar decantar).

---

## Referencias

- Documento canónico del boilerplate: `03-agentic-dev-boilerplate-doc.md`
- Presentación 18 slides: `04-agentic-dev-boilerplate-slides.md`
- Mapa harness 3impacto: `docs/3impacto-harness-map.md`
- Engineering Mandate: `docs/3impacto-context/GLOBAL_SPEC...`
- UX/Content Rules: `docs/3impacto-context/GLOBAL_SPEC___UX...`
