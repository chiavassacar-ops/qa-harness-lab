# Clase 1 — Context Engineering

> Síntesis de los 6 conceptos centrales de la Clase 1 del Dojo UPEX
> Edición 3, escritas con mis palabras siguiendo el método pedagógico
> trabajado con Claude.
>
> **Estas síntesis son MIS palabras**, no son la versión canónica de
> Claude ni del Dojo. Son mi anclaje mental — si dentro de seis meses
> me preguntan qué es uno de estos conceptos, esta es la versión que
> tengo que poder recitar.
>
> Fecha de asimilación: 14 al 18 de mayo de 2026
> Clase dictada por: Elyer Maldonado (Sensei UPEX Dojo)

---

## Síntesis 1 — Agente IA

> Un agente IA es una inteligencia artificial que no solo responde
> preguntas, sino que puede hacer tareas siguiendo un objetivo.

**El contraste central:** chatbot **responde**, agente **hace**.
Y "siguiendo un objetivo" le da dirección, no es ejecución ciega.

---

## Síntesis 2 — Context Engineering

> Context Engineering significa preparar bien toda la información que
> le das a la IA para que trabaje mejor. No es solo "hacer un buen
> prompt". Es darle a la IA el contexto correcto, en el orden correcto
> y con las reglas correctas.

**Conexión con Hashimoto:** esto es el loop de refinamiento aplicado
al contexto que recibe la IA.

---

## Síntesis 3 — Ventana de contexto

> La ventana de contexto es la cantidad de información que la IA puede
> "tener presente" mientras responde. Es como la memoria de trabajo de
> la IA dentro de una conversación.

**Anclaje de Ely:** la metáfora del "globo de agua" — la ventana es
finita, y cuando se llena, lo que entra hace salir otra cosa. El
ejemplo numérico: 200K tokens nominales, alucinación empieza a aparecer
hacia los 475K acumulados.

---

## Síntesis 4 — System Prompt

> System prompt es un conjunto de instrucciones que la IA utiliza para
> llevar a cabo un objetivo. Esas instrucciones tienen 3 niveles: el
> propio del fabricante, el inicial del usuario (que da un marco de
> acción), y un tercero propio del proyecto que estamos desarrollando.
> Claude y otras IA le dan jerarquía a esas capas o archivos.
> Lovable no lo hace.

**Para retener:** la jerarquía implica que **el más específico pisa al
más general** — cuando hay conflicto entre el nivel usuario y el nivel
proyecto, gana el del proyecto. Esto es lo que hace útil la jerarquía,
y es exactamente lo que Lovable no tiene.

---

## Síntesis 5 — Progressive Loading

> Progressive Loading en IA es darle a la inteligencia artificial
> solamente el contexto que necesita para la tarea actual, cargando
> más información únicamente cuando el flujo lo requiere. La idea no
> es "meter toda la documentación del proyecto", sino construir un
> sistema donde la IA accede progresivamente a reglas, specs, skills,
> mandatos o módulos específicos según el problema que está
> resolviendo.

**Tres mecanismos concretos que lo implementan:**
1. **Skills** — cada skill solo carga su metadata (200-500 tokens) al
   inicio; el contenido completo se carga solo cuando la IA la invoca.
2. **Subagentes** — la IA principal delega tareas a subagentes con su
   propia ventana de contexto; el subagente trabaja en silencio y solo
   devuelve el resultado final.
3. **Variables agénticas + project.yaml** — en vez de pegar valores en
   `CLAUDE.md`, se definen variables que la IA busca cuando las
   necesita.

---

## Síntesis 6 — Las tres metáforas de Ely (mapeadas a Just-in-Time de Toyota)

> Los japoneses aprendieron y usaron Just-in-Time para armar sus autos.
> Aplicaron **progressive loading** porque coordinaron con los
> proveedores que les llevaran los insumos en el momento que los
> necesitaba, y no tenían todo el stock en sus galpones.
> Aplicaron **orquestación** porque pudieron armar autos ensamblando
> partes que venían de distintos lugares, pero existía una línea de
> ensamblaje principal.
> Y aplicaron la **especialización de armado** de partes con el menor
> rechazo de pieza posible, porque cada proveedor se dedicaba
> exclusivamente a fabricar UNA pieza, lo que le permitía perfeccionar
> el proceso, reducir defectos al mínimo, y entregar componentes
> listos para integrar.

### Mapeo metáforas Ely ↔ JIT Toyota

| Metáfora de Ely | Mi analogía JIT | Qué representa |
|-----------------|-----------------|----------------|
| **Biblioteca** (catálogo, no libros memorizados) | **JIT de insumos** (los proveedores entregan cuando se necesita, sin stock en galpón) | Progressive loading |
| **Cocina** (chef delega, no fríe) | **Línea de ensamblaje** (orquesta partes de distintos proveedores) | Orquestación / subagentes |
| **Orquesta** (cada músico sabe su parte) | **Especialización de proveedores** (cada uno hace UNA pieza muy bien, bajo rechazo) | Skills / composición de capacidades |

### Por qué este mapeo me sirve

Las tres metáforas de Ely y mi analogía JIT son **el mismo concepto
desde dos vocabularios distintos**. El de Ely viene del software /
agentes IA; el mío de la industria manufacturera. Ambos describen un
**sistema modular orquestado donde el conocimiento vive distribuido en
piezas especializadas y se compone en runtime**.

Para 3impacto, mi vocabulario JIT puede ser más entendible para los
Maxis que las metáforas de Ely, porque los PMs vienen de negocio, no
de IA.

### Cita textual de Ely (cierre del bloque)

> *"Para que sepan que esa es la moda o el meta del uso de la
> inteligencia artificial en el estado del arte es la orquestación."*

---

## Lo que une las 6 síntesis

Las 6 forman una secuencia lógica:

1. **Qué es la IA con agencia** (Síntesis 1).
2. **Qué disciplina la usa bien** (Síntesis 2).
3. **Cuál es su límite físico** (Síntesis 3).
4. **Cómo se le habla al inicio** (Síntesis 4).
5. **Cómo se le va dando contexto a lo largo del trabajo** (Síntesis 5).
6. **Cómo se organiza todo eso a nivel sistema** (Síntesis 6).

La mentalidad opuesta — el **mega-prompt** que carga todo de una y
pretende que una sola IA lo haga todo sola — es lo que el Dojo me
está enseñando a desarmar.

---

## Conexiones con material posterior

- **Síntesis 5 (progressive loading)** está **implementada como
  archivos reales** en el Agentic Dev Boilerplate (ver `03-agentic-dev-boilerplate-doc.md`).
- **Síntesis 4 (jerarquía system prompt)** se materializa en el trío
  `CLAUDE.md` + `CONTEXT.md` + `DESIGN.md` del boilerplate, y es la
  base de mi hipótesis de `AGENTS.md` para Lovable
  (ver `05-palancas-3impacto.md`).
- **Síntesis 6 (orquestación)** es la columna vertebral del modelo
  agentic — el "IA trabaja, humano decide con checkpoints" del
  boilerplate.

---

## Referencias

- Programa del Dojo: `00-programa.md`
- Mapeo Dojo ↔ mi plan: `01-mapeo-con-mi-plan.md`
- Material aplicado (boilerplate dev): `03-agentic-dev-boilerplate-doc.md`
- Slides del boilerplate: `04-agentic-dev-boilerplate-slides.md`
- Palancas para 3impacto: `05-palancas-3impacto.md`
