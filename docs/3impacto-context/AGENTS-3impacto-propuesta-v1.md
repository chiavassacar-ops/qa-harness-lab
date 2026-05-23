# AGENTS.md — Propuesta de Knowledge File para Lovable (3impacto)

> **Estado**: Propuesta v1 para discusión con el equipo.
> **Autor**: Carlos Chiavassa (QA Shift-Left, 3impacto).
> **Inspiración**: patrón `CLAUDE.md` + `CONTEXT.md` + `DESIGN.md`
> del Agentic Dev Boilerplate (UPEX Galaxy).
> **Objetivo**: extender el Engineering Mandate actual con una capa de
> CONTEXTO que hoy no existe, para reducir la interpretación de la IA
> y mejorar la consistencia entre sesiones de Lovable.

---

## Por qué este archivo, en una oración

El Engineering Mandate actual le dice a Lovable **qué reglas seguir**
(seguridad, stack, UI, data). Lo que NO le dice es **qué existe ya en
el proyecto, dónde vive, y para qué sirve cada parte**. Este archivo
agrega esa capa de mapa para que la IA no tenga que reinferir el
estado del repo cada vez.

---

## Sección 1 — CONTEXT (el mapa del proyecto)

> Esta sección le dice a la IA QUÉ EXISTE y DÓNDE VIVE.
> Sin este mapa, las reglas del Mandate son aire: la IA puede saber
> "usar AppButton" pero no sabe que AppButton ya existe en
> `src/components/ui/AppButton.tsx`.

### 1.1. Identidad del proyecto

- **Nombre**: 3impacto.
- **Tipo**: B2B SaaS de medición de impacto / ESG.
- **Estado**: en desarrollo activo, pre-launch.
- **Modelo de negocio**: organizaciones cargan datos de impacto,
  generan reportes, publican perfil público.

### 1.2. Stack técnico (referencia rápida — fuente de verdad: Engineering Mandate Part 2)

- Frontend: React 18 + Vite + TypeScript (strict).
- Styling: Tailwind + clsx + tailwind-merge.
- UI Kit: shadcn/ui (solo átomos base).
- State: TanStack Query (server) + Zustand/Context (cliente).
- Backend: Supabase (Auth + Postgres + Storage + Edge Functions).
- i18n: react-i18next (NO hardcoded strings).

### 1.3. Mapa de carpetas (qué hay y dónde)

```
src/components/ui/         → Átomos base. AppButton vive acá.
src/components/[Feature]/  → Componentes por feature.
src/hooks/                 → Hooks de lógica de negocio.
src/lib/                   → Utilities + Zod schemas + constants.
src/integrations/          → Clientes de servicios externos.
```

### 1.4. Entidades del dominio (qué tablas existen)

> TODO: completar con la lista real de tablas de Supabase.
> Esta sección es **crítica** porque sin ella la IA inventa entidades.

Convenciones:
- Nombres: `snake_case`, plural.
- Campos obligatorios en TODA tabla: `id`, `created_at`, `updated_at`.
- RLS: política obligatoria por tabla.
- Soft delete: campo `status` (ENUM), no boolean.

### 1.5. Roles del sistema (RBAC actual)

> TODO: completar con la lista real de roles.
> Incluir: nombre del rol, qué puede ver, qué puede hacer.

Ejemplo de estructura:
```
- super_admin: acceso total (staff 3impacto).
- org_admin: gestión de su organización.
- org_member: lectura + carga de datos en su organización.
- public_viewer: solo lectura de perfiles públicos.
```

### 1.6. Endpoints públicos vs privados

> TODO: listar endpoints públicos (no requieren auth) explícitamente.
> Por defecto, todo es privado.

### 1.7. Estados y máquinas de estado del dominio

Cuando una entidad tiene ciclo de vida (ej: workspace, report,
publication), documentar acá la máquina de estados completa.

Ejemplo:
```
Reporte: draft → in_review → approved → published → archived
```

### 1.8. Integraciones externas

> TODO: listar integraciones (email, analytics, etc.).
> Cada una con: qué hace, qué Edge Function la maneja, qué pasa si
> falla.

---

## Sección 2 — RULES (reglas operativas)

> Esta sección es un **resumen ejecutivo** del Engineering Mandate
> existente, NO un reemplazo. Lo que está acá es lo que la IA tiene
> que tener presente en CADA prompt. El Mandate completo es la
> referencia detallada.

### 2.1. Seguridad (NON-NEGOTIABLE — ver Mandate Part 1)

- **RBAC obligatorio en DOS niveles**: Supabase RLS + validación
  server-side.
- **Nunca confiar en checks de frontend**. Frontend solo presenta;
  la decisión es siempre del backend.
- **Secrets**: NUNCA en código, NUNCA en commit. Solo en secret
  manager.
- **PII**: separada cuando se pueda, acceso logueado siempre.
- **Storage**: buckets privados por defecto, pre-signed URLs vía
  Edge Functions.
- **Inputs**: validados con Zod schemas, queries parametrizadas.
  Raw SQL prohibido.

### 2.2. Reglas de componentes UI

- **Toda acción usa `<AppButton />`**. Prohibido `PrimaryButton`,
  `SecondaryButton`, `OutlineButton`.
- **shadcn/ui solo átomos base**: no usar componentes compuestos
  prebuild si existe un átomo equivalente.
- **Mobile-first**: altura interactiva mínima 40px (`h-10`).
- **i18n**: NO hardcoded strings. Todo via `t('key')`.

### 2.3. Reglas de data

- **Tablas**: snake_case plural + id/created_at/updated_at + RLS.
- **Forms**: Zod fuera del componente, `z.infer` para typing.
- **Queries**: TanStack Query con keys `['entity', 'id', 'action']`.
- **Lógica sensible**: Edge Function, no en el cliente.

### 2.4. Reglas de calidad

- **Rule of Two**: solo abstraer cuando hay 2+ casos reales.
- **Máximo 200 líneas por archivo**.
- **Errores**: catch backend → map a i18n key → toast.
- **Tests**: Vitest, focus en `src/lib`.

### 2.5. Prioridades estrictas de implementación (orden)

1. Seguridad y RLS.
2. Correctitud del modelo de datos.
3. Completitud del backoffice.
4. Correctitud del frontend.
5. Pulido visual.

> **Lectura**: ante conflicto entre dos prioridades, gana la de número
> menor. Si pulir visual rompe RLS, no se pulle.

### 2.6. Prohibiciones absolutas

- NO crear entidades no definidas explícitamente.
- NO inferir lógica de negocio.
- NO agregar demo o seed data.
- NO exponer Supabase keys.
- NO bypass RLS.
- NO auto-crear roles o permisos.
- NO agregar features fuera de scope.

---

## Sección 3 — DESIGN (sistema visual)

> Esta sección es un **resumen ejecutivo** del UX/Content Rules
> existente. Tokens y convenciones para que la IA no invente
> variantes.

### 3.1. Tokens de color

- **Primary Blue**: `#0F3553`.
- **Coral**: usado para CTAs (solid o gradient).
- **Otros**: referenciar al archivo `UX/Content Rules` completo.

### 3.2. AppButton (especificación completa)

Ubicación: `src/components/ui/AppButton.tsx`.

**Geometría INMUTABLE:**
- Border: 1px only.
- Radius: `rounded-full`.
- Transition: `transition-all duration-300 ease-out`.

**Tamaños:**
- `sm` → 24px height, `px-3`.
- `default` → 32px height, `px-5`.

**Variantes válidas:**
- `coral`, `coral-outlined`.
- `primary`, `primary-outlined`.
- `muted-outlined`.

**Hover:**
- Solid: elevation + shadow.
- Outlined: subtle tinted background.

### 3.3. Accesibilidad

- `aria-labels` en íconos.
- Focus rings visibles (`ring-2`).
- Altura interactiva mínima 40px (excepto AppButton sm).

---

## Sección 4 — VOZ DE LA IA (cómo hablar con cada interlocutor)

> Esta sección es **adicional** al Mandate actual. Resuelve un hueco
> identificado: hoy la IA de Lovable habla igual con todos, lo cual
> es útil para uno y ruidoso para otros.

### 4.1. Por defecto: PM Voice

Cuando no hay señal contraria, la IA traduce código a valor de
negocio. Output:
- Qué cambió desde la perspectiva del usuario final.
- Qué impacto tiene en la organización (no en el archivo).
- Riesgos visibles, sin jerga técnica innecesaria.

### 4.2. Modo técnico (on-demand)

Se activa cuando el prompt incluye una de estas señales:
- Palabras técnicas: "schema", "RLS", "Edge Function", "Zod",
  "TanStack", "TypeScript error".
- Pedido explícito: "modo técnico", "hablá técnico".
- Pregunta sobre archivo específico (`src/...`).

En modo técnico:
- Mostrar el código.
- Explicar las decisiones de arquitectura.
- Citar archivos relevantes (path completo).

### 4.3. Modo QA-mixto (para refinement)

Se activa cuando el prompt habla de:
- Criterios de aceptación.
- Refinamiento de historia.
- Validación / testing.
- Análisis de riesgo.

En modo QA-mixto:
- Output en formato Given/When/Then cuando aplique.
- Identificar gaps de spec antes de proponer implementación.
- Considerar concurrencia, casos límite, abuso, capa de datos.

---

## Sección 5 — CHECKLIST DE PRE-FLIGHT

> Antes de generar código, la IA verifica mentalmente:

- [ ] ¿La entidad/tabla que voy a tocar existe en sección 1.4?
  Si no, ALTO y consultar.
- [ ] ¿La acción tiene RLS resuelto en backend, no solo en frontend?
- [ ] ¿Los strings van por `t('key')`?
- [ ] ¿Los inputs están validados con Zod?
- [ ] ¿Usé `<AppButton />` para todas las acciones?
- [ ] ¿El archivo va a quedar bajo 200 líneas?

Si alguno falla, NO generar código. Pedir clarificación.

---

## Sección 6 — CÓMO MANTENER ESTE ARCHIVO

> El archivo es vivo. Cuando algo cambia en el proyecto, el archivo
> debe reflejarlo, o se vuelve mentira y la IA confía en mentiras.

### Triggers para actualizar este archivo

- Nueva tabla en Supabase → actualizar sección 1.4.
- Nuevo rol → actualizar sección 1.5.
- Nuevo endpoint público → actualizar sección 1.6.
- Nueva integración externa → actualizar sección 1.8.
- Nuevo patrón de error detectado en QA → agregar a sección 2.

### Responsabilidades sugeridas

- **Maxi 1 (PO)**: secciones 1.1, 1.4 (validación de entidades),
  1.5 (roles).
- **Maxi 2 (Dev)**: secciones 1.2, 1.3, 1.6, 1.7, 1.8, 2.
- **Carlos (QA)**: secciones 4 (voz), 5 (checklist), 6 (mantenimiento).

---

## Apéndice — Relación con el Engineering Mandate actual

Este archivo NO reemplaza el Mandate. **Lo extiende.**

| Pieza | Mandate actual | Este archivo |
|-------|---------------|--------------|
| Reglas de seguridad detalladas | ✅ Part 1 (autoridad) | Sección 2.1 (resumen) |
| Stack técnico detallado | ✅ Part 2 (autoridad) | Sección 1.2 (resumen) |
| Reglas de UI detalladas | ✅ Part 2 + UX Rules | Sección 2.2 + 3 (resumen) |
| Mapa de entidades del dominio | ❌ no existe | ✅ Sección 1.4 (nuevo) |
| Mapa de roles RBAC | ❌ no existe | ✅ Sección 1.5 (nuevo) |
| Voz de la IA por interlocutor | ❌ no existe | ✅ Sección 4 (nuevo) |
| Checklist de pre-flight | ❌ no existe | ✅ Sección 5 (nuevo) |
| Proceso de mantenimiento | ❌ no existe | ✅ Sección 6 (nuevo) |

**Regla de oro ante conflicto**: si una afirmación de este archivo
contradice el Mandate, gana el Mandate. Este archivo no es autoridad,
es mapa.

---

## Referencias

- Engineering Mandate actual (autoridad): GLOBAL SPEC — ENGINEERING
  MANDATES (CONTEXTO LOVABLE), Part 1-3.
- UX/Content Rules actual (autoridad): GLOBAL SPEC — UX / CONTENT
  CONSISTENCY RULES.
- Patrón inspirador (UPEX Galaxy): Agentic Dev Boilerplate, archivos
  `CLAUDE.md` + `CONTEXT.md` + `DESIGN.md`.
- Análisis de palancas: `qa-harness-lab/docs/upex-dojo/05-palancas-3impacto.md`.
