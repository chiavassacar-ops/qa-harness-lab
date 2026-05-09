# Notas de Birgitta Böckeler — "Harness engineering for coding agent users"

**Fuente:** https://martinfowler.com/articles/harness-engineering.html
**Fecha de lectura:** 9 de mayo de 2026
**Secciones leídas:** "Feedforward and Feedback" + "Computational vs Inferential"

## El cuadro 2×2

|                            | Computational (determinístico) | Inferential (semántico, IA) |
|----------------------------|--------------------------------|------------------------------|
| **Feedforward** (antes)    | feature test plan             |  shift left testing          |
| **Feedback** (después)     | regresion                      |  creacion de nuevas reglas de negocios|

## Feedforward vs Feedback

Feedforward: anticiparse a la acción del agente dándole contexto y reglas 
Feedback: despúes de la acción del agente y evalúa el resultadao
si tengo solo feedforwar no tengo aseguramiento de la calidad
Si tengo solo feedback freno la salida a producción porqu eme lleno de errores

## Computational vs Inferential

lo computacional es objetivo y problablemente se facil que una ia te reemplace
Inferecnial es interpretación, criterios, analisis de ngocio

## Cómo conecta esto con mi trabajo en 3impacto

muchos ia para chequear un prompt para subir a Lovable, pero no armamos el arnes para ese prompt se distorcione dentro de Lovable. Creemo sque con el contexto dque le dimos al inicio esta todo solucionado

## Pregunta abierta

Me queda claro cque lo computacional no es suficiente y es facil reemplazar
Lo inferencial es criterio y es negocios por lo tanto es humano
El feedforward es fundamental para que todo el equipo se concentre en este punto. 
En feedback fixear errores y contarlos para ganar un campeonato, no sirve. El Qa debe aprender a ser ingeniero en arnes para que no vuelvan a ocurrir
