REQ-03 · Perfiles públicos para usuarios y organizaciones


Descripción

US Recargada Funcional · REQ-03
Objetivo funcional
Dar presencia pública a usuarios individuales y organizaciones dentro de la plataforma mediante perfiles accesibles sin autenticación, con información básica, feed de actividad y espacios de impacto vinculados.

Alcance
Incluye
Perfil público para usuarios individuales y organizaciones

Foto de portada y foto de perfil o logo

Datos básicos visibles

Feed de publicaciones

Etiquetas clickeables de Espacios de Impacto

Slide/carousel de espacios donde contribuye

URL pública amigable y compartible

Acceso sin autenticación

Fuera de alcance
Sistema de follow

Mensajería directa

Reacciones sociales públicas

API, SQL, arquitectura, seguridad profunda, logs y performance técnica

Actores
Actor principal: Usuario u organización dueña del perfil

Actor secundario: Visitante no autenticado

Precondiciones visibles
El usuario u organización tiene cuenta creada.

Para organizaciones, existe onboarding previo.

Los perfiles públicos están habilitados sin autenticación.

Flujo principal esperado
El usuario u organización accede a la edición de su perfil público desde su panel.

Carga o edita portada, foto de perfil o logo, nombre, tipo, país y descripción breve.

Publica una actualización en el feed con texto libre y etiquetas de Espacios de Impacto.

El slide de espacios se actualiza automáticamente cuando el actor se vincula a nuevos espacios.

Un visitante accede a la URL pública y visualiza el perfil completo sin necesidad de registrarse.

Variantes funcionales
Variante A · Perfil sin publicaciones
El feed muestra empty state.

El slide de espacios puede estar vacío.

Variante B · Organización en verificación
El perfil público existe, pero puede mostrar indicador visible de verificación en proceso.

Reglas funcionales específicas
RF-01: Las URLs públicas son amigables y permanentes con formato por slug.

RF-02: Las etiquetas de Espacios de Impacto en publicaciones son clickeables y llevan al espacio correspondiente.

RF-03: El slide de espacios se actualiza automáticamente y no es editable manualmente.

RF-04: Las publicaciones muestran texto, fecha y etiquetas. No hay editor enriquecido.

RF-05: El perfil público muestra la misma información independientemente de si el visitante está autenticado o no.

RF-06: El comportamiento exacto del botón de contacto queda sujeto a definición funcional final.

RF-07: El feed debe mostrar contenido en orden cronológico descendente.

Mandatos generales QA aplicables a esta US
Esta historia hereda automáticamente los mandatos generales QA definidos en el documento base vigente. Para evitar redundancia, no se duplican aquí de forma completa.

Aterrizaje específico para REQ-03
La URL pública debe ser accesible sin autenticación y mantener coherencia con el slug definido.

El perfil debe mostrar empty states claros cuando no existan publicaciones o espacios vinculados.

Las etiquetas de Espacios de Impacto deben ser visualmente reconocibles como enlaces y llevar al destino prometido.

El feed debe respetar orden cronológico descendente y mantener consistencia visual en desktop y mobile.

Las imágenes de portada, perfil o logo deben respetar responsive, no deformarse y mostrar feedback correcto durante upload.

Si el perfil muestra indicador de verificación en proceso, este debe ser visible, comprensible y consistente con los estados del sistema.

Cualquier desvío respecto del documento de mandatos generales QA debe declararse explícitamente en esta historia.

Acceptance Criteria
AC-01: Un usuario u organización puede editar su perfil público con portada, logo o foto, datos y descripción.

AC-02: Puede publicar una actualización con texto y etiquetas de Espacios de Impacto.

AC-03: Las etiquetas son clickeables y llevan al espacio correspondiente.

AC-04: El slide de espacios muestra automáticamente los espacios donde el actor contribuye.

AC-05: La URL pública es accesible sin autenticación y muestra el perfil completo.

AC-06: Un perfil sin publicaciones ni espacios muestra empty states coherentes.

AC-07: Las fotos de portada y perfil se pueden cargar y se muestran correctamente.

AC-08: Los mandatos generales QA del documento base aplican a esta historia y se validan junto con las particularidades definidas en REQ-03.

Riesgos / pendientes
DP-01: Definir si el slug lo elige el usuario o se genera automáticamente.

DP-02: Definir tamaño y proporción final de portada y perfil.

DP-03: Definir comportamiento exacto del botón de contacto.

DP-04: Definir forma visible del indicador de verificación en proceso.

Criterio de preparación para QA
Historia apta para backlog y testing funcional con pendientes menores no bloqueantes.

Test cases funcionales derivados
TC-01 · Edición de perfil
Ingresar a edición de perfil.

Cargar portada, logo y completar datos.

Guardar.

Verificar visualización en URL pública.

TC-02 · Publicación con etiquetas
Crear publicación.

Etiquetar espacios.

Guardar.

Verificar etiquetas clickeables.

TC-03 · URL pública sin login
Abrir la URL sin sesión.

Verificar acceso y contenido completo.

TC-04 · Empty states
Ingresar a un perfil sin publicaciones ni espacios.

Verificar mensajes vacíos coherentes.

TC-05 · Validaciones heredadas
Validar herencia de mandatos generales QA del documento base.

Validar uploads de imagen, truncado, responsive y loaders.

Validar links, empty states y consistencia de navegación.

QA REFINEMENT
REQ-03 · Perfil público de usuarios y organizaciones

Este análisis complementa la especificación funcional del PO con definiciones necesarias para reducir ambigüedad, facilitar implementación y prevenir errores funcionales.

Esta historia debe cumplir con:

GLOBAL SPEC — ENGINEERING MANDATES

GLOBAL SPEC — UX & CONTENT CONSISTENCY RULES

1. Clarificación del comportamiento funcional
El perfil público permite que usuarios individuales y organizaciones tengan una página visible públicamente dentro de la plataforma.

El perfil cumple tres funciones principales:

Identidad pública del actor.

Historial visible de actividad.

Vinculación con Espacios de Impacto.

El perfil debe poder ser visualizado por cualquier visitante sin autenticación.

No incluye funcionalidades sociales avanzadas como follow, reacciones o mensajería.

2. Estados funcionales del perfil
Aunque no están definidos explícitamente, funcionalmente existen los siguientes estados:

Estado

Significado

Perfil incompleto

perfil sin publicaciones ni espacios

Perfil activo

perfil con información básica y actividad

Perfil organización en verificación

perfil visible con indicador de verificación pendiente

Reglas:

todos los estados deben poder visualizarse públicamente

el visitante no autenticado ve el mismo contenido que un usuario autenticado

3. Reglas de negocio identificadas
RN-01: Todo usuario o organización puede tener un perfil público accesible mediante URL.

RN-02: El perfil puede incluir foto de portada y foto de perfil o logo.

RN-03: El perfil muestra información básica del actor (nombre, tipo, país y descripción).

RN-04: El perfil puede mostrar publicaciones en un feed cronológico descendente.

RN-05: Las publicaciones pueden incluir etiquetas de Espacios de Impacto.

RN-06: Las etiquetas de Espacios de Impacto son clickeables.

RN-07: El perfil puede mostrar un slide/carousel con los espacios donde el actor contribuye.

RN-08: El contenido del slide se genera automáticamente a partir de vínculos existentes.

RN-09: El perfil público debe poder visualizarse sin autenticación.

RN-10: El feed debe ordenarse en orden cronológico descendente.

4. Criterios de aceptación (Gherkin)
AC-01 Edición de perfil público
Given un usuario u organización accede a la edición de su perfil  
When actualiza portada, foto de perfil o logo, datos básicos y descripción  
Then el sistema guarda los cambios  
And la información se refleja en la URL pública del perfil

AC-02 Publicación en el feed
Given un usuario u organización accede a su perfil  
When publica una actualización con texto y etiquetas de Espacios de Impacto  
Then la publicación aparece en el feed del perfil  
And se muestra con fecha y etiquetas asociadas

AC-03 Etiquetas clickeables
Given una publicación contiene etiquetas de Espacios de Impacto  
When un visitante hace click en una etiqueta  
Then el sistema redirige al Espacio de Impacto correspondiente

AC-04 Visualización del slide de espacios
Given un usuario u organización contribuye a uno o más Espacios de Impacto  
When un visitante accede al perfil público  
Then el slide muestra automáticamente esos espacios

AC-05 Acceso público sin autenticación
Given un visitante accede a la URL pública del perfil  
When no tiene sesión iniciada  
Then puede visualizar el perfil completo sin restricciones

AC-06 Perfil sin actividad
Given un perfil no tiene publicaciones ni espacios asociados  
When un visitante accede al perfil  
Then el sistema muestra empty states claros para feed y espacios

5. Consideraciones UX funcionales
El perfil público debe ser fácilmente interpretable por visitantes externos.

Requisitos UX clave:

el encabezado debe identificar claramente al actor (nombre, tipo y país)

la foto de perfil/logo y la portada deben visualizarse correctamente en desktop y mobile

el feed debe mostrar contenido de forma clara y cronológica

las etiquetas de Espacios de Impacto deben ser claramente identificables como enlaces

los empty states deben indicar que aún no existe actividad

6. Riesgos detectados por QA
R-01: No está definida la estructura final del slug de URL pública.

R-02: No está definido si el slug puede editarse posteriormente.

R-03: No está definido el límite máximo de publicaciones visibles en el feed.

R-04: No está definido el comportamiento exacto del botón de contacto.

R-05: No está definida la proporción final de las imágenes de portada y perfil.

R-06: No está definido si el feed soportará paginación o scroll infinito.

7. Ambigüedades / decisiones pendientes
DP-01: Confirmar si el slug se genera automáticamente o puede ser personalizado por el usuario.

DP-02: Confirmar dimensiones finales de imágenes de portada y perfil.

DP-03: Definir comportamiento funcional del botón de contacto.

DP-04: Definir cómo se mostrará visualmente el estado de verificación en proceso.
