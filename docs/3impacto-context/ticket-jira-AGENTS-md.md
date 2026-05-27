# Ticket Jira — Sugerencia: AGENTS.md para Lovable

> Texto listo para pegar como descripción del ticket en el epic
> "Mejoras de Knowledge/IA" del proyecto 3impacto.

---

## TÍTULO SUGERIDO

```
Sugerencia: extender Engineering Mandate con capa de CONTEXTO (AGENTS.md)
```

---

## TIPO

Task / Spike (o lo que use el equipo para sugerencias de proceso).

---

## DESCRIPCIÓN

### Contexto

Durante el Dojo UPEX de Agentic Quality Engineering, procesé el
patrón de Knowledge Files usado en el Agentic Dev Boilerplate
(stack idéntico al nuestro: React + Vite + Supabase + TypeScript).
Ese patrón divide el contexto de la IA en TRES archivos:

- `CLAUDE.md` → reglas operativas.
- `CONTEXT.md` → mapa de qué existe en el proyecto.
- `DESIGN.md` → sistema visual.

### Diagnóstico aplicado a 3impacto

Hicimos el mapeo contra nuestros archivos actuales:

| Pieza del patrón | Equivalente en 3impacto | Estado |
|------------------|-------------------------|--------|
| `CLAUDE.md` (reglas) | Engineering Mandate | ✅ Existe (y muy completo) |
| `DESIGN.md` (visual) | UX/Content Rules | ✅ Existe |
| `CONTEXT.md` (mapa) | — | ❌ **Hueco** |

**No tenemos un mapa del proyecto** que le diga a Lovable:
- Qué tablas existen.
- Qué roles RBAC hay configurados.
- Qué endpoints son públicos y cuáles privados.
- Qué integraciones externas están en uso.
- Qué máquinas de estado tienen las entidades del dominio.

Cada sesión de Lovable arranca sin ese mapa y tiene que reinferirlo
desde código, lo cual genera inconsistencias entre sesiones.

### Propuesta

Crear un archivo `AGENTS.md` que **extienda** (no reemplace) el
Engineering Mandate, con tres capas:

1. **CONTEXT**: mapa de entidades, roles, endpoints, integraciones.
2. **RULES**: resumen ejecutivo de las reglas del Mandate (la
   autoridad sigue siendo el Mandate completo).
3. **DESIGN**: resumen de tokens y AppButton (autoridad sigue siendo
   UX/Content Rules).

Más dos secciones nuevas:

4. **Voz de la IA por interlocutor** (PM Voice / técnico / QA-mixto).
5. **Checklist de pre-flight** antes de generar código.
6. **Proceso de mantenimiento** del archivo.

### Beneficio esperado

- Reducir la cantidad de "interpretaciones libres" que hace Lovable
  cuando le falta contexto.
- Reducir el tiempo que se pierde corrigiendo código que asume
  entidades inexistentes o roles mal mapeados.
- Acelerar el onboarding cuando entre alguien nuevo al proyecto
  (el archivo es también documentación humana).

### Lo que NO propone esta sugerencia

- NO reemplazar el Engineering Mandate (sigue siendo la autoridad).
- NO modificar el UX/Content Rules (sigue siendo la autoridad).
- NO cambiar el flujo de trabajo actual entre Maxi 1, Maxi 2 y yo.

### Estado del drafteo

- v1 del archivo ya está drafteado (adjunto / link al archivo).
- Las secciones de RULES y DESIGN están rellenadas con el contenido
  del Mandate y UX Rules actuales.
- Las secciones de CONTEXT (entidades, roles, endpoints) tienen
  marcadores TODO porque requieren validación del equipo:
  - Lista de tablas y entidades del dominio.
  - Lista de roles RBAC actualmente configurados.
  - Lista de endpoints públicos.
  - Lista de integraciones externas activas.

### Próximos pasos sugeridos

1. Revisión del draft v1 por Maxi 1 (validación de entidades,
   negocio).
2. Revisión del draft v1 por Maxi 2 (validación técnica del mapa
   de carpetas e integraciones).
3. Iteración a v2 con los TODOs completados.
4. Decisión del equipo: ¿se sube al Knowledge file de Lovable o se
   mantiene como documento interno?

### Referencias

- Drafteo v1 del AGENTS.md (archivo adjunto).
- Análisis original de palancas:
  `qa-harness-lab/docs/upex-dojo/05-palancas-3impacto.md`.
- Material de fondo del patrón:
  `qa-harness-lab/docs/upex-dojo/03-agentic-dev-boilerplate-doc.md`.

---

## CRITERIOS DE ACEPTACIÓN

(Para que el ticket pueda cerrarse)

- [ ] Maxi 1 revisó el draft v1 y dio feedback en comentarios.
- [ ] Maxi 2 revisó el draft v1 y dio feedback en comentarios.
- [ ] El equipo decidió en conjunto: implementar / iterar / archivar.
- [ ] Si se implementa: existe versión v2 con TODOs completados.
- [ ] Si se implementa: existe acuerdo escrito sobre quién mantiene
      qué sección del archivo.

---

## ASIGNADO A

Carlos Chiavassa (autor de la sugerencia).

---

## ETIQUETAS SUGERIDAS

- `knowledge-engineering`
- `IA-improvement`
- `process`
- `documentation`
