# Clase 2 — Shift-Left Testing (Bunkai)

> Descomposición técnica de la Clase 2 del Dojo UPEX Edición 3
> (Shift-Left Testing — Agentic Quality Engineer), dictada por
> Elyer Maldonado el martes 19 de mayo de 2026, 19:30–22h.
>
> "Bunkai" — descomponer la técnica en sus piezas, entender cada una,
> y conectarla con lo que ya sé. No es un resumen lineal de la clase
> (la clase saltó mucho); es una reordenación deliberada para que me
> sirva como referencia operativa.
>
> Fecha de procesamiento: 22 de mayo de 2026
> Clase dictada por: Elyer Maldonado (Sensei UPEX Dojo)

---

## 1. Marco mental de la clase

### Lo que prometía el programa (temario oficial)

- 40 min — Análisis estático sin MCPs
- 50 min — Risk-Based Testing + ACs como contrato + BDD
- 30 min — Refinamiento del ATP

### Lo que realmente fue la clase

La clase **se desbordó del temario**. Ely lo dijo al cierre:
> *"Esta clase va a ser enorme, eh, porque empieza lo bueno. (...)
> primero necesitamos saber cómo crear un tablero, cómo crear una
> gestión de incidencias profesionales para un proyecto."*

En vivo se vio:

1. Construcción de un proyecto agentic dev de cero (Bunkai TMS).
2. Setup de Jira (épicas, historias, custom fields, ACLI).
3. Creación de épicas e historias **con orquestación + subagentes**.
4. Aplicación de shift-left testing **en vivo, en un ticket real**.
5. Práctica grupal: cada alumno comenta refinamientos de AC en una historia.
6. Cierre: el rol del QA en este flujo, y cómo se conecta con TDD del dev.

**El temario oficial (análisis estático / risk-based / refinamiento ATP)
queda diferido a los videos asíncronos** que Ely está grabando para la
Dojoteca y el Devlog #1 (ver sección 7).

---

## 2. Los conceptos centrales

### 2.1. Qué es shift-left testing (definición operativa de Ely)

> *"Es básicamente entrar por un proceso de prevención de defectos
> a través de una serie de instrucciones específicas que tiene la
> skill. (...) La idea es que se haga ANTES del sprint planning.
> Una vez que ya nosotros definamos el chift-left, pasamos a modo
> estimación."*

**Tres piezas operativas del concepto:**

1. **Cuándo**: antes del sprint planning. Es el paso previo a la
   estimación.
2. **Quién**: el QA, con sombrero de "Quality Engineer".
3. **Qué hace**: prevenir defectos refinando criterios de aceptación
   **antes** de que el dev escriba la primera línea de código.

### 2.2. La frase que define el cambio de mentalidad

> *"Con la mentalidad de shift-left QA, no solo basta con añadir
> nuevos escenarios, sino BLINDAR los que ya están escritos para
> que el desarrollador no tenga margen de interpretación."*

**Lo que retengo:** shift-left no es "agregar tests al inicio".
Es **eliminar la interpretación del dev** a través de specs
que no dejan grietas.

### 2.3. El estado Jira "shift-left" en el flujo

La historia atraviesa estos estados:

```
backlog → refinement → SHIFT-LEFT → estimation → in progress → ...
```

**El paso shift-left es un estado dedicado** en Jira, no una
actividad implícita. Eso lo hace medible: una historia o pasó por
shift-left, o no pasó.

---

## 3. La técnica aplicada en vivo (el momento clave de la clase)

### 3.1. El contexto del experimento

Ely tomó la historia BK4 ("Create Workspace") y aplicó shift-left
**en vivo, frente a todos**, usando OpenCode + la skill ACLI.

### 3.2. El prompt exacto que usó Ely (para guardar como referencia)

> *"Necesito que pienses con la cabeza de un ingeniero de calidad
> de software qué errores podríamos prevenir de esta historia de
> usuario. Y solamente quiero que te concentres en el scope. (...)
> qué podemos prevenir de esta historia de ser implementada.
> Quiero que pienses como un QA, apliques esta típica ingeniería
> de calidad sin salirte del scope, y que puedas decirme si podemos
> refinar los criterios de aceptación. (...) Piensa desde la base
> de datos, piensa desde un punto de vista de API, o cuáles son
> los típicos problemas cuando se trata de este tipo de historia."*

**Estructura del prompt que voy a reusar:**

1. Rol explícito (*"pensa como QA"*).
2. Objetivo claro (*"prevenir defectos"*).
3. Restricción de scope (*"sin salirte del scope"*).
4. Ángulos de ataque sugeridos (*"DB, API, problemas típicos"*).
5. Pedido de output procesable (*"refinar AC, ver gaps, observaciones"*).

### 3.3. Lo que devolvió la IA (categorías de hallazgos)

La IA produjo análisis en estas categorías:

| Categoría | Ejemplo del caso BK4 |
|-----------|----------------------|
| **Colisión de slugs** | Race condition multi-tenant: dos owners crean nombres parecidos que derivan al mismo slug |
| **Slugs derivados extremos** | Si el name son caracteres especiales, el slug puede quedar de 1 carácter |
| **Abuso de endpoints** | El endpoint /workspaces no menciona rate limit; script malicioso podría crear 500 workspaces |
| **Seguridad / payload injection** | Usuario inyecta `role: "admin"` en el request body |
| **Collation en database** | "ACMÉ" vs "ACME" — index lower podría considerarlos distintos sin violar índice, pero el slug colisionaría |

**Lectura mía:** estas categorías son **un checklist replicable** para
cualquier historia. No son "ideas brillantes irrepetibles", son
**dimensiones de análisis** que aplican a casi cualquier US:

- Concurrencia (race conditions, multi-tenant)
- Casos límite de input (caracteres especiales, longitud mínima/máxima)
- Abuso / seguridad (rate limit, injection, payload manipulation)
- Capa de datos (collation, índices, constraints)

### 3.4. El refinamiento de ACs propuesto

La IA propuso **dos AC nuevos** + retoque de los existentes:

- AC nuevo 1: caso de slug duplicado → retorna 409.
- AC nuevo 2: caso de slug inválido por longitud < 3 caracteres → retorna 400.

Cuando Ely le preguntó *"¿qué pasa con los AC ya existentes?"*, la IA
los blindó también. **Esto es lo que el dev necesita: no margen de
interpretación.**

---

## 4. La práctica grupal: trabajo en equipo de QAs

### 4.1. La consigna

Cada alumno toma una historia del tablero y postea en los comentarios
de Jira sus propios criterios de aceptación refinados, **firmados con
su nombre**.

### 4.2. La modalidad de trabajo

> *"Yo agarro esos comentarios, los junto a todos y digo: bueno, me
> pareció bien estos criterios, vamos a usarlos. Así trabajamos todos
> en equipo."*

**Esto es importante**: el shift-left grupal no es "votación de
criterios". Es **convergencia mediada por el QA senior**. El QA
senior es quien decide qué propuestas entran al AC final.

### 4.3. Mi conexión con 3impacto

En 3impacto este rol lo hago YO (no Maxi 1, no Maxi 2). Es decir:

- **Yo soy el QA senior** que filtra propuestas.
- Pero **NO tengo un equipo de QAs aportando propuestas**.
- Solo tengo a mí mismo + IA.

**Implicación**: lo que en el Dojo es un loop colectivo (varios QAs
proponen, uno consolida), en 3impacto es un loop solitario (yo
propongo con IA, yo consolido). Eso me da **mayor velocidad pero
menor diversidad de mirada**. Vale tenerlo presente como sesgo.

---

## 5. La filosofía de fondo: Quality Engineering, no test automation

### 5.1. La advertencia de Ely (minuto 47)

> *"No salir de acá simplemente con 'a bueno, sea automatizar, armar
> unas pruebas'. Sino saber pensar a nivel estratégico de POR QUÉ
> se hace esto, o POR QUÉ deberíamos evitar esto."*

### 5.2. La pirámide implícita (el momento de Luis Flores)

Luis Flores reformuló y Ely lo validó:

```
50 TC que se nos ocurren (mental)
   ↓ filtrar
8-10 TC que documentamos (lo que puede introducir un bug en el futuro)
   ↓ filtrar
3-4 TC que automatizamos (los del flujo crítico)
```

**Lectura mía:** esta es una **pirámide de severidad inversa**. No
automatizo todo lo que documento; no documento todo lo que se me
ocurre. Cada filtro tiene un criterio:

- Mental → documentado: ¿este caso puede introducir un bug?
- Documentado → automatizado: ¿este caso es flujo crítico?

### 5.3. La conexión con BDD del hilo de Slack

Esta semana en el Slack del Dojo, en respuesta a mi pregunta sobre
Gherkin, Ely planteó:

> *"BDD es la práctica completa, Gherkin es solo el lenguaje, y
> Cucumber es el patrón de pruebas automatizadas. Hacer BDD sin
> Cucumber es la mejor opción: usar Gherkin a nivel Historia de
> Usuario nada más."*

**Esto encaja perfecto con el shift-left de la clase**: el lenguaje
Given/When/Then es el formato del **refinamiento de AC**, no del
script de automatización. El script (Playwright, Vitest) viene
después y no necesita parsear Gherkin.

---

## 6. Lo que también pasó en la clase (contexto técnico denso)

### 6.1. El proyecto Bunkai TMS

Ely mostró el repo `bunkai-tms`, creado a partir del
`agentic-dev-boilerplate` (el mismo que procesé en los archivos
03 y 04 de este repo). Stack: **Next.js + Supabase + Vercel**.

**Mi conexión:** este es **el mismo stack de 3impacto**. Lo que Ely
está construyendo en vivo es estructuralmente equivalente a lo que
los Maxis construyen en 3impacto, pero con dos diferencias críticas:

1. Ely usa **Claude Code + skills**, los Maxis usan **Lovable**.
2. Ely tiene **CLAUDE.md + CONTEXT.md + DESIGN.md** versionados,
   los Maxis tienen un **Knowledge file plano**.

Ver `05-palancas-3impacto.md` para el detalle de las palancas.

### 6.2. La frase sobre Lovable (minuto 7:30)

> *"Una de las cosas que se cae la mata: aplicaciones como Lovable
> (no sé si la han visto), hay otras como Vercel v0, Bolt y entre
> otras. Son aplicaciones para crear webs, pero esto es como la
> punta del iceberg. O sea, es muy ineficiente en cierto sentido
> si quieres construir una aplicación más robusta. Y como nosotros
> estamos creando una aplicación seria, ahí es cuando entra en
> juego nada más y nada menos que Claude Code u Open Code."*

**Mi lectura del impacto en 3impacto:**

- 3impacto está construido sobre **Lovable** (la "punta del iceberg").
- La aplicación es **seria** (B2B SaaS ESG, datos sensibles, RLS
  obligatorio según el Engineering Mandate).
- Esto es exactamente el caso que Ely describe como **mal alineado**.

**No es mi pelea acá**: yo soy QA, no Architect. Pero **es un dato
para mi mapa harness**: el techo técnico de Lovable es una limitación
del sistema, no una elección de los Maxis. Mi rol es cerrar el
feedback computacional **dentro de esa restricción**.

### 6.3. La técnica de "modo orquestación"

Ely mostró cómo Claude Code puede despachar **subagentes en
background** que trabajan en paralelo sin chocar entre sí:

> *"Agents are dispatched on background. La IA puede seguir hablando
> o puede seguir haciendo cosas mientras estos agentes siguen
> trabajando. (...) El punto de que la ventana de contexto sea tan
> baja te permite poder hablar con la IA en esta misma sesión sin
> tener que abrir sesiones nuevas."*

**Conexión con Síntesis 6 (Clase 1):** esto es la metáfora de la
cocina hecha terminal. Cada subagente es un cocinero especializado.
El orquestador es el chef que delega.

### 6.4. El rol del CLI vs MCP

> *"El CLI es 10 veces más efectivo que los MCPs. El MCP de por sí
> consume muchos tokens, tiene que hacer llamadas de ida y vuelta,
> tiene protocolos. (...) Un CLI es una API compactada, fácil de
> usar."*

**Para retener:** cuando hay opción entre CLI o MCP para la misma
tarea, **preferir CLI**. Menos tokens, más determinístico. El MCP
queda para cuando no hay CLI disponible.

---

## 7. La tarea de la semana (que mandó Ely por Slack)

### 7.1. Misión primaria

- **Preparación**: ver TODOS los videos de Clase 1 y Clase 2 en la
  Dojoteca (todavía no están subidos, paciencia).
- **Acción**: crear mi proyecto de `qa-engineering` según las
  instrucciones del video, y usar la skill `/shift-left-testing`
  para validar las Historias de Usuario de Bunkai.

### 7.2. Misión secundaria

- **Preparación**: ver TODOS los videos del Devlog #1.
- **Acción**: intentar crear mi propio proyecto de Software,
  instalando el Boilerplate de Dev, para usar las skills según
  fases: `/project-foundation` + `/project-bootstrap` +
  `/product-management`.

### 7.3. Contenido del Devlog #1 (10 partes anunciadas)

| Parte | Tema |
|-------|------|
| 1 | Idealización del proyecto + Jira Setup |
| 2 | Diseño Sketch (Claude Design) |
| 3 | Auto-instalador (magic command) para setup local |
| 4 | Onboarding teórico del Agentic Dev Boilerplate ← **ya procesé esto** |
| 5 | Skill `/project-foundation` (Constitución, PRD, SRS) |
| 6 | Skill `/project-bootstrap` (Frontend Next.js) |
| 7 | Skill `/project-bootstrap` (Backend + DB Supabase + Vercel) |
| 7.2 | Errores de deployment en Vercel (tips) |
| 8 | Skill `/product-management` para Backlog y Sprint |
| 9 | Repaso de Épicas e Historias de Usuario |
| 10 | (en grabación) Creando Épicas e Historias con la skill |

**Notas mías sobre la tarea:**

- La misión **primaria** está mejor alineada con mi rol QA.
- La misión **secundaria** la conviene hacer aunque no sea
  mi rol, porque "entender el lado dev me hace mejor QA"
  (textual de Ely).
- Esperar a que los videos estén disponibles en la Dojoteca antes
  de avanzar (Ely insiste en paciencia).

---

## 8. Lo que me llevo: 5 acciones concretas

### 8.1. Para el Dojo

1. **Esperar los videos** de Dojoteca antes de hacer la tarea (no
   intentar hacerlo de memoria a partir de la clase desordenada).
2. **Cuando vea los videos**, comparar con esta nota y corregir lo
   que esté mal interpretado.

### 8.2. Para 3impacto

3. **Reusar el prompt de Ely** (sección 3.2) para hacer shift-left
   en una historia real de 3impacto. Probar con el REQ-03 (Perfiles
   públicos) que ya tengo como archivo de contexto.
4. **Aplicar la pirámide de Luis Flores** (sección 5.2) a una
   historia de 3impacto: ¿qué 50 TC se me ocurren? ¿Cuáles
   documento? ¿Cuáles automatizaría si pudiera?

### 8.3. Para el repo

5. **Cuando me toque escribir la nota de Clase 5** (Playwright),
   volver a esta sección 3.3 y ver si las **categorías de hallazgo**
   (concurrencia, casos límite, abuso, capa de datos) se reflejan
   como tests automatizados o no.

---

## 9. Tres preguntas que me quedan abiertas

1. **La skill `/shift-left-testing` que mencionó Ely** vive en el
   repo de QA (`agentic-qa-boilerplate`). Cuando descargue ese repo
   (¿después de Clase 4 o 5?), ¿qué prompt usa exactamente esa
   skill? ¿Es el mismo que usó Ely en vivo o es más sofisticado?

2. **¿El estado Jira "shift-left" se configura a mano** o lo
   instala el boilerplate? Si lo instala el boilerplate, podríamos
   replicarlo en 3impacto.

3. **¿Cómo se mide si shift-left funcionó?** Ely no dio métrica.
   Una hipótesis mía: comparar bugs encontrados post-sprint en
   historias que pasaron por shift-left vs historias que no. Si
   hay diferencia, shift-left tiene ROI medible.

---

## Referencias

- Transcripción completa: archivo del proyecto
  `UPEX_Dojo__Modulo__2__Shift-Left_Testing__Agentic_Quality_Engineer___E3_`
- Programa del Dojo: `00-programa.md`
- Mapeo Dojo ↔ mi plan: `01-mapeo-con-mi-plan.md`
- Síntesis Clase 1: `02-clase-01-context-engineering.md`
- Boilerplate Dev (doc): `03-agentic-dev-boilerplate-doc.md`
- Boilerplate Dev (slides): `04-agentic-dev-boilerplate-slides.md`
- Palancas para 3impacto: `05-palancas-3impacto.md`
- Engineering Mandate de 3impacto:
  `docs/3impacto-context/GLOBAL_SPEC___ENGINEERING_MANDATES`
- Ejemplo REQ-03 (QA Refinement):
  `docs/3impacto-context/REQ-03___Perfiles_públicos`
