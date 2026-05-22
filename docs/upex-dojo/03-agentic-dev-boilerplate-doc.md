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
