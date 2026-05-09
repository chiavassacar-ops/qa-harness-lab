# Mapa harness × 3 carriles × 3impacto

**Autor:** Charly (QA shift-left)
**Fecha:** 9 de mayo de 2026
**Estado:** Borrador inicial — pendiente validación en repo del proyecto

---

## Hallazgo del 9 de mayo

Al estudiar harness engineering para proponerlo al equipo, descubrí
que 3impacto YA TIENE harness engineering implementado en buena medida,
solo que no se llama así.

## Lo que ya tenemos (confirmado)

### Feedforward inferencial: MUY FUERTE ✅

- **Global Spec — Engineering Mandates** (escrito por Maxi 1, cargado en Lovable):
  feedforward inferencial enterprise-grade. Cubre seguridad, arquitectura,
  performance, design system, i18n, side effects, anchoring, IPFS.
- **Global Spec — UX & Content Consistency Rules**: complemento orientado
  a UX/QA con 200+ reglas verificables sobre inputs, validaciones,
  estados, responsive, accesibilidad, tono.
- **QA Refinement por US** (mi rol actual): conversión de US ambiguas
  en specs con reglas de negocio, criterios Gherkin, riesgos y decisiones
  pendientes documentadas.

### Feedforward computacional: DECLARADO ⚠️

El Engineering Mandate declara:
- ESLint rules con `no-restricted-imports` (lucide-react, pdfjs-dist,
  recharts, framer-motion).
- Cross-domain import guard (Public/Auth no puede importar Backoffice).
- Bundle budgets (Public/Auth ≤300KB gzip, App ≤500KB gzip).
- TypeScript strict mode obligatorio.
- ZOD schemas para todas las validaciones.
- `ci:performance` declarado: typecheck, lint, build, bundle report.

**Pendiente validar**: ¿estas reglas están realmente cableadas en
GitHub Actions y bloquean PRs? Hasta no entrar al repo, no lo sé.

### Feedback computacional: DESCONOCIDO ❓

No tengo visibilidad todavía sobre:
- Si existe `.github/workflows/` con jobs activos.
- Si hay branch protection rules en `main`.
- Si los status checks bloquean merges.
- Si hay tests automatizados corriendo.

**Próximo paso**: pedir acceso de lectura al repo del proyecto.

### Feedback inferencial: HUMANO E INFORMAL ⚠️

- Maxi 1 revisa output de Lovable a ojo y pide correcciones.
- Yo testeo manual contra criterios de aceptación.
- No hay AI code review, LLM-as-judge ni revisor automático
  post-Lovable.

## Mapeo a los 3 carriles de Garzas

### Carril 1 — Inner Loop (exploración rápida)

- **Quién opera**: Maxi 1 y Maxi 2 prototipando en Lovable.
- **Harness implícito existente**:
  1. Trabajo serializado en Lovable (no trabajan los dos a la vez).
  2. Pre-flight de Maxi 1: ChatGPT (escribe requisitos) → Claude (valida) → Lovable.
  3. Pre-flight de Maxi 2 con Gemini.
  4. Engineering Mandate cargado como contexto permanente.

### Carril 2 — Middle Loop (supervisión y control)

- **Quién opera**: yo (Charly).
- **Harness existente**: QA refinement por US + testeo manual contra
  mandatos generales.
- **Hueco identificado**: no hay sensors automáticos que verifiquen
  cumplimiento del Engineering Mandate antes del merge. La supervisión
  depende de mi tiempo humano.

### Carril 3 — Outer Loop (validación con usuarios reales)

- **Estado**: pendiente de mapeo. Lo armamos cuando entendamos
  mejor el flujo de release.

## Huecos detectados (preliminar)

1. **No sé si los lint/budget checks corren en CI**. Si solo están
   declarados en el spec pero no enforzados, el documento es intención,
   no harness.

2. **No hay feedback inferencial automatizado**. Después de que Lovable
   genera código, no hay revisor automático que evalúe si cumple el spec
   antes de llegar a mí.

3. **El AGENTS.md de Lovable no se actualiza con lecciones aprendidas
   sistemáticamente**. Cuando se detecta un patrón nuevo, no veo proceso
   para incorporarlo al spec global.

## Propuesta inicial (a validar y refinar)

1. **Auditar el repo**: validar qué del Engineering Mandate está
   realmente corriendo en GitHub Actions y qué solo está declarado.

2. **Cerrar el loop de feedback computacional**: si los gates no están
   activos, cablearlos. Branch protection + status checks que bloqueen
   merge si fallan.

3. **Establecer un proceso de actualización del Knowledge file**: cada
   patrón de error que detecto en QA refinement o en testing se convierte
   en una nueva regla del spec. Esto es engineering del harness puro,
   tal como lo describe Hashimoto.

## Pregunta abierta para conversar con el equipo

¿Cuál es la fricción más grande que sienten Maxi 1 y Maxi 2 hoy con
Lovable? Si lo sabemos, podemos priorizar qué hueco cerrar primero.

---

## Documentos de contexto

- `docs/3impacto-context/global-spec-engineering.md`
- `docs/3impacto-context/global-spec-ux-qa.md`
- `docs/3impacto-context/req-03-ejemplo-qa-refinement.md`
