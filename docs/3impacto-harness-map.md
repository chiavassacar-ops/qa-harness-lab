# Mapa harness × 3 carriles × 3impacto

**Autor:** Charly (QA shift-left)
**Fecha:** 9 de mayo de 2026
**Estado:** Borrador — primera versión

> Documento que conecta el modelo de harness engineering (Hashimoto, Fowler/Böckeler)
> con el modelo de 3 carriles de Javier Garzas, aplicado al proyecto 3impacto.
> Sirve como base para conversación con Maxi 1 (CEO-PO-PM) y Maxi 2 (PM-DEV).

---

## 1. Cómo encajan los 3 carriles con el modelo de Fowler

### Carril 1 — Inner Loop (exploración rápida)

- **Quién lo opera:** Maxi 1 y Maxi 2 prototipando en Lovable.
- **Velocidad:** minutos a horas.
- **Qué harness aplica acá:** [PENDIENTE — sección 1.1]
- **Por qué:** los prototipos pueden y deben fallar. Si los frenamos con harness pesado, perdemos velocidad de exploración.

### Carril 2 — Middle Loop (supervisión y control)

- **Quién lo opera:** yo (Charly), QA shift-left.
- **Velocidad:** horas a un día.
- **Qué harness aplica acá:** TODO. Acá vive el harness.
- **Sensors computacionales que necesitamos:** [PENDIENTE — sección 1.2]
- **Sensors inferenciales que podríamos usar:** [PENDIENTE — sección 1.3]

### Carril 3 — Outer Loop (validación con usuarios reales)

- **Quién lo opera:** todo el equipo + usuarios finales (empresas, ONGs).
- **Velocidad:** días a semanas.
- **Qué harness aplica acá:** [PENDIENTE — sección 1.4]

---

## 2. Mapa de riesgos en 3impacto

¿Qué cosas en 3impacto NO pueden fallar nunca? Estos son los candidatos #1 para harness duro (gates obligatorios).

1. [PENDIENTE]
2. [PENDIENTE]
3. [PENDIENTE]
4. [PENDIENTE]

---

## 3. Tres controles concretos que podríamos tener este mes

NO los voy a implementar ahora. Solo los identifico, los priorizo y los presento para conversar con el equipo.

### Control 1: [PENDIENTE]
- **Tipo en cuadro 2×2:** [Computational + Feedback / etc.]
- **Esfuerzo estimado:** [bajo / medio / alto]
- **Qué problema previene:** [PENDIENTE]

### Control 2: [PENDIENTE]
- **Tipo:** [...]
- **Esfuerzo:** [...]
- **Qué previene:** [...]

### Control 3: [PENDIENTE]
- **Tipo:** [...]
- **Esfuerzo:** [...]
- **Qué previene:** [...]

---

## 4. Una pregunta abierta para conversar con el equipo

[PENDIENTE]

---

## Notas de cierre

- Este documento es vivo. Va a evolucionar a medida que aprenda más y conversemos como equipo.
- Las fuentes intelectuales detrás están en `/docs/notas-harness/`.
