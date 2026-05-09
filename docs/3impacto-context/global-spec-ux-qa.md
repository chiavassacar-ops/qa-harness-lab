GLOBAL SPEC — UX & CONTENT CONSISTENCY RULES (MANDATOS GENERALES QA)


Descripción

MANDATOS GENERALES QA

Estándares Funcionales de Plataforma

3impacto · v1.0 · Marzo 2026

Toda US Recargada hereda estos mandatos automáticamente.

Solo se documenta en la US lo que se desvía de este estándar.

 

 

1. Inputs de Texto
Reglas que aplican a todo campo de texto de la plataforma, sin excepción.

 

1.1 Maxlength
[TXT-01] Campos de texto corto (nombres, títulos, labels): maxlength = 80 caracteres.

[TXT-02] Campos de texto medio (descripciones breves, motivos, razones): maxlength = 300 caracteres.

[TXT-03] Campos de texto largo (narrativas, descripciones extendidas, manifiestos): maxlength = 600 caracteres.

[TXT-04] Campos de párrafo o texto enriquecido (publicaciones, contenido editorial): maxlength = 2000 caracteres.

[TXT-05] Todo campo con maxlength debe mostrar contador de caracteres restantes visible en tiempo real (ej: '42/80').

[TXT-06] El contador cambia a color rojo cuando quedan menos del 10% de caracteres disponibles.

[TXT-07] El campo no permite escribir más allá del maxlength. No se trunca — se bloquea la entrada.

1.2 Placeholder y Labels
[TXT-08] Todo input tiene label visible permanente (no solo placeholder). El label no desaparece al tipear.

[TXT-09] Todo input tiene placeholder descriptivo que indica qué se espera (ej: 'Nombre legal de la organización').

[TXT-10] Los placeholders no repiten el label. Son complementarios (label: 'Email corporativo', placeholder: 'nombre@empresa.com').

1.3 Trim y Sanitización
[TXT-11] Todo campo de texto aplica trim() automático al perder el foco (elimina espacios al inicio y final).

[TXT-12] Campos de texto corto no permiten saltos de línea.

[TXT-13] Se reemplazan automáticamente múltiples espacios consecutivos por uno solo.

 

2. Validaciones de Formato por Tipo de Dato
Cada tipo de dato tiene reglas de validación específicas que se aplican globalmente.

 

2.1 Email
[FMT-01] Validación de formato RFC 5322 simplificado (regex estándar).

[FMT-02] Se valida en tiempo real al perder foco (onBlur), no solo al submit.

[FMT-03] Mensaje de error: 'Ingresá un email válido (ej: nombre@empresa.com)'.

[FMT-04] Se convierte automáticamente a minúsculas.

[FMT-05] Maxlength de campo email: 120 caracteres.

2.2 Teléfono
[FMT-06] Solo permite dígitos numéricos (0-9). No acepta letras ni caracteres especiales.

[FMT-07] Permite el prefijo '+' solo como primer carácter (código de país).

[FMT-08] Maxlength: 20 caracteres (cubre todos los formatos internacionales).

[FMT-09] Teclado numérico en mobile (inputmode='tel').

[FMT-10] Mensaje de error: 'Solo se permiten números. Incluí el código de país con +'.

2.3 URLs / Sitio Web
[FMT-11] Validación de formato URL (protocolo + dominio mínimo).

[FMT-12] Si el usuario no incluye protocolo, se agrega 'https://' automáticamente.

[FMT-13] Maxlength: 200 caracteres.

[FMT-14] Mensaje de error: 'Ingresá una URL válida (ej: https://www.ejemplo.com)'.

2.4 Números e Importes
[FMT-15] Campos numéricos solo aceptan dígitos. Teclado numérico en mobile (inputmode='numeric').

[FMT-16] Campos de importe aceptan un separador decimal (punto). Máximo 2 decimales.

[FMT-17] Campos de importe muestran el símbolo de moneda como prefijo no editable.

[FMT-18] No se permiten valores negativos salvo excepción explícita en la US.

2.5 Identificación Fiscal / Documentos
[FMT-19] Campo alfanumérico. Permite letras, números, guiones y puntos.

[FMT-20] Maxlength: 30 caracteres.

[FMT-21] Se convierte automáticamente a mayúsculas.

 

 

3. Tooltips y Textos de Ayuda
Toda la plataforma debe ser autoexplicativa. Ningún campo queda sin contexto.

 

[TIP-01] Todo campo de formulario tiene tooltip explicativo. Sin excepción.

[TIP-02] El tooltip se activa con ícono de ayuda (?) al lado del label. En mobile, se activa con tap.

[TIP-03] El tooltip muestra texto breve (máximo 120 caracteres) que explica qué se espera y por qué.

[TIP-04] Los tooltips no repiten el label ni el placeholder. Agregan contexto que no está en ningún otro lugar.

[TIP-05] Tooltips en campos obligatorios deben indicar si el campo es obligatorio y por qué.

[TIP-06] Tooltips en campos opcionales deben indicar qué beneficio tiene completarlos.

[TIP-07] El tooltip se cierra al hacer click fuera, al presionar Escape, o después de 5 segundos sin interacción.

[TIP-08] Los tooltips nunca tapan el campo que están explicando.

 

4. Campos Obligatorios y Opcionales
 

[REQ-01] Los campos obligatorios se marcan con asterisco rojo (*) al lado del label.

[REQ-02] Los campos opcionales se marcan con texto '(opcional)' en color atenuado al lado del label.

[REQ-03] Al intentar enviar con campos obligatorios vacíos: scroll automático al primer campo con error.

[REQ-04] Mensaje de error en campo obligatorio vacío: 'Este campo es obligatorio'.

[REQ-05] El error se muestra debajo del campo, en rojo, con ícono de alerta.

[REQ-06] El borde del campo cambia a rojo cuando tiene error.

[REQ-07] El error desaparece en tiempo real cuando el usuario corrige el valor.

 

5. Buscadores y Campos de Búsqueda
 

[SRC-01] Maxlength en buscadores: 120 caracteres.

[SRC-02] Búsqueda por debounce de 300ms (no se dispara en cada keystroke).

[SRC-03] Mostrar indicador de loading mientras se busca.

[SRC-04] Si no hay resultados: mensaje 'No se encontraron resultados para [término]'. No se muestra vacío.

[SRC-05] Botón o ícono de limpiar búsqueda (X) visible cuando hay texto ingresado.

[SRC-06] Al limpiar búsqueda, se restauran los resultados por defecto.

[SRC-07] El buscador mantiene el foco después de limpiar.

[SRC-08] Placeholder del buscador: 'Buscar por [contexto]...' (ej: 'Buscar por nombre o país...').

 

 

6. Estados de Componentes UI
Todo componente interactivo debe tener estados claramente definidos y diferenciables.

 

6.1 Botones
[BTN-01] Estado default: color sólido con contraste legible.

[BTN-02] Estado hover: cambio de luminosidad (+10%) y cursor pointer.

[BTN-03] Estado active/pressed: escala 0.98 (efecto de presión sutil).

[BTN-04] Estado disabled: opacidad 50%, cursor not-allowed. No dispara acción.

[BTN-05] Estado loading: texto reemplazado por spinner + texto 'Procesando...' El botón queda disabled durante el loading.

[BTN-06] Botones de acción irreversible (eliminar, rechazar) son rojos y piden confirmación.

[BTN-07] Doble click en botones de submit está bloqueado. Se deshabilita al primer click hasta recibir respuesta.

6.2 Inputs
[INP-01] Estado default: borde sutil, fondo diferenciado del background.

[INP-02] Estado focus: borde de color primario (highlight), outline visible para accesibilidad.

[INP-03] Estado error: borde rojo, mensaje de error debajo, ícono de alerta.

[INP-04] Estado disabled: opacidad 60%, fondo gris, no editable, cursor not-allowed.

[INP-05] Estado readonly: visualmente diferente de disabled (sin opacidad reducida, pero no editable).

6.3 Cards
[CRD-01] Estado default: sombra sutil o borde definido.

[CRD-02] Estado hover: elevación aumentada (sombra mayor) + cursor pointer si es clickeable.

[CRD-03] Estado seleccionado: borde de color primario + indicador visual (check o highlight).

[CRD-04] Estado loading: skeleton loader que replica la estructura de la card.

6.4 Estados de Carga Globales
[LOD-01] Toda carga de datos muestra skeleton loaders, nunca pantalla en blanco.

[LOD-02] Los skeletons replican la estructura real del contenido (no un spinner genérico centrado).

[LOD-03] Si la carga tarda más de 5 segundos, mostrar mensaje: 'Esto está tardando más de lo esperado...'.

[LOD-04] Si la carga falla, mostrar mensaje de error con botón de reintentar.

[LOD-05] Las transiciones entre loading y contenido cargado son suaves (fade-in, no flash).

6.5 Estados Vacíos
[EMP-01] Toda lista o grilla sin datos muestra un empty state con ícono, título y descripción.

[EMP-02] El empty state incluye un CTA cuando corresponde (ej: 'Aún no tenés espacios. Explorá Descubrir').

[EMP-03] Nunca se muestra una tabla con headers pero sin filas, ni una grilla vacía sin explicación.

 

 

7. Responsive y Breakpoints
La plataforma es full responsive. No existen vistas 'solo desktop'.

 

[RES-01] Breakpoints estándar: mobile < 640px, tablet 640-1024px, desktop > 1024px.

[RES-02] Toda vista debe testearse en: 375px (iPhone SE), 390px (iPhone 14), 768px (iPad), 1024px (iPad landscape), 1280px (laptop), 1440px (desktop).

[RES-03] Grillas: 1 columna en mobile, 2 en tablet, 3+ en desktop (salvo excepciones en la US).

[RES-04] Tablas en mobile: se transforman en cards apiladas o en scroll horizontal con indicador visual.

[RES-05] Formularios en mobile: una columna, inputs al 100% del ancho, botones al 100% del ancho.

[RES-06] Navegación en mobile: colapsa a menú hamburguesa o bottom navigation.

[RES-07] Modales en mobile: ocupan pantalla completa (full-screen modal), no modal flotante.

[RES-08] Texto nunca se corta ni se oculta sin ellipsis (...) con tooltip del texto completo.

[RES-09] Imágenes son responsive (max-width: 100%, height: auto). Nunca se deforman.

[RES-10] Touch targets en mobile: mínimo 44x44px (estándar Apple/Google).

[RES-11] No hay hover-only interactions en mobile. Todo lo que funciona con hover tiene alternativa de tap.

 

8. Cursor, Foco y Navegación
 

[FOC-01] Al abrir un formulario o modal, el cursor se posiciona automáticamente en el primer campo interactivo.

[FOC-02] Tab navega los campos en orden lógico (de arriba a abajo, de izquierda a derecha).

[FOC-03] Shift+Tab navega en orden inverso.

[FOC-04] Enter en el último campo de un formulario ejecuta el submit (salvo textareas).

[FOC-05] Escape cierra modales, dropdowns y tooltips.

[FOC-06] No hay saltos erráticos de cursor al interactuar con campos.

[FOC-07] El indicador de foco es visible en todo momento (outline o borde). No se elimina el focus ring.

[FOC-08] Elementos clickeables tienen cursor: pointer. No clickeables tienen cursor: default. Disabled tiene cursor: not-allowed.

 

 

9. Mensajes de Error, Éxito y Confirmación
Reglas para todos los mensajes del sistema, en todos los contextos.

 

9.1 Mensajes de Error
[ERR-01] Todo error muestra un mensaje específico. Nunca 'Error desconocido' ni 'Algo salió mal' genérico.

[ERR-02] Los errores de campo se muestran inline, debajo del campo, en rojo.

[ERR-03] Los errores de sistema (red, servidor) se muestran como toast o banner superior.

[ERR-04] Todo error de sistema incluye sugerencia de acción: 'Intentá de nuevo' o 'Contactá soporte'.

[ERR-05] Errores de validación se muestran al perder foco (onBlur), no solo al submit.

[ERR-06] Los mensajes de error están en español rioplatense (tuteo con vos, ej: 'Ingresá', 'Completá').

9.2 Mensajes de Éxito
[SUC-01] Toda acción exitosa muestra confirmación visual (toast verde o redirect con mensaje).

[SUC-02] Los toasts de éxito desaparecen solos después de 4 segundos.

[SUC-03] Los toasts son descartables con click o swipe.

9.3 Confirmaciones
[CNF-01] Acciones destructivas (eliminar, rechazar, cancelar) siempre piden confirmación con modal.

[CNF-02] El modal de confirmación tiene título claro, descripción de consecuencias, y dos botones: cancelar (neutro) y confirmar (rojo para destructivas).

[CNF-03] El botón de confirmar destructivo dice la acción concreta ('Eliminar', 'Rechazar'), no 'Aceptar'.

[CNF-04] Acciones con impacto financiero (compras, transferencias) muestran resumen antes de confirmar.

 

10. Filtros, Orden y Paginación
 

10.1 Filtros
[FIL-01] Los filtros se aplican sin recarga de página (client-side o fetch asíncrono).

[FIL-02] Al aplicar filtros, se muestra contador de resultados actualizado ('12 resultados').

[FIL-03] Siempre visible un botón o link 'Limpiar filtros' que restaura el estado por defecto.

[FIL-04] Los filtros activos se muestran como chips/tags visibles con X para remover individualmente.

[FIL-05] En mobile, los filtros se ocultan en un drawer/modal con botón 'Filtrar' visible.

[FIL-06] Si los filtros no devuelven resultados, se muestra empty state con sugerencia: 'Probá con menos filtros'.

10.2 Orden
[ORD-01] Orden por defecto: se define en cada US. Si no se especifica, es por fecha descendente (más reciente primero).

[ORD-02] El selector de orden es visible y muestra la opción activa.

[ORD-03] Al cambiar orden, los resultados se actualizan sin recarga.

10.3 Paginación
[PAG-01] Paginación por defecto: 12 items por página en grillas, 20 en tablas/listas.

[PAG-02] Se muestra: 'Mostrando X–Y de Z resultados'.

[PAG-03] Navegación con botones Anterior/Siguiente + números de página.

[PAG-04] En mobile, paginación simplificada: solo Anterior/Siguiente + indicador de página actual.

[PAG-05] Al cambiar de página, se hace scroll al inicio de la lista/grilla.

[PAG-06] Si se prefiere infinite scroll en una US, se indica explícitamente. El default es paginación numérica.

 

 

11. Archivos y Uploads
Reglas para toda carga de archivos en la plataforma.

 

[UPL-01] Todo uploader muestra los formatos aceptados antes de seleccionar archivo (ej: 'JPG, PNG o PDF. Máx 5MB').

[UPL-02] Tamaño máximo por defecto: imágenes 5MB, documentos 10MB, videos 50MB (salvo excepción en US).

[UPL-03] Si el archivo excede el tamaño, mensaje: 'El archivo excede el tamaño máximo de X MB'.

[UPL-04] Si el formato no es válido, mensaje: 'Formato no permitido. Usá [formatos válidos]'.

[UPL-05] Barra de progreso visible durante la subida.

[UPL-06] Preview del archivo subido: thumbnail para imágenes, nombre+tamaño para documentos.

[UPL-07] Opción de eliminar archivo subido antes de confirmar (ícono X o papelera).

[UPL-08] Drag & drop habilitado en desktop. Zona de drop con feedback visual.

[UPL-09] En mobile, el selector abre cámara + galería como opciones.
[UPL-10] Excepción HERO Premium

Para Portada Premium de Espacios de Impacto:

máximo 3MB

ratio 1.6–2.5

mínimo 1920x1080

formatos JPG/PNG/WebP


 Se actualiza mandato QA del módulo HERO para alinear validaciones con definición vigente implementada. Nuevos valores oficiales: 3MB, ratio 1.6–2.5, mín. 1920x1080. Evita futuros desvíos por criterios obsoletos.

12. Selects, Multiselects y Componentes Compuestos
 

[SEL-01] Todo select tiene opción por defecto: 'Seleccioná una opción' (no seleccionable como valor válido).

[SEL-02] Selects con más de 8 opciones incluyen buscador interno.

[SEL-03] Multiselects muestran los items seleccionados como chips/tags con X para remover.

[SEL-04] Si un multiselect tiene más de 3 seleccionados, muestra '3 seleccionados +X más' colapsado.

[SEL-05] Selects de país muestran banderas al lado del nombre.

[SEL-06] Los 17 ODS se muestran siempre como círculos seleccionables con su color oficial.

[SEL-07] Sliders muestran el valor numérico actual en tiempo real.

[SEL-08] Toggles (sí/no) muestran label de estado activo ('Activo' / 'Inactivo').

[SEL-09] Date pickers usan formato DD/MM/AAAA. No se acepta formato americano.

 

13. Tablas de Datos
 

[TBL-01] Headers fijos (sticky) al hacer scroll vertical.

[TBL-02] Columnas con ancho proporcional al contenido. Nunca columnas vacías excesivamente anchas.

[TBL-03] Textos largos en celdas se truncan con ellipsis y tooltip con texto completo.

[TBL-04] Filas alternadas con diferencia sutil de fondo (zebra striping) para legibilidad.

[TBL-05] Columnas ordenables tienen indicador visual (flecha arriba/abajo).

[TBL-06] En mobile: las tablas se transforman en cards apiladas o permiten scroll horizontal con indicador.

[TBL-07] Si una tabla tiene acciones por fila (editar, eliminar, ver), se agrupan en una columna 'Acciones' al final.

 

 

14. Accesibilidad Mínima
Estándares mínimos de accesibilidad que aplican a toda la plataforma.

 

[A11-01] Contraste mínimo de texto: ratio 4.5:1 (WCAG AA).

[A11-02] Todo elemento interactivo es alcanzable y operable con teclado.

[A11-03] Imágenes con contenido informativo tienen alt text descriptivo.

[A11-04] Imágenes decorativas tienen alt='' (vacío).

[A11-05] Los formularios usan labels asociados con for/id. No solo placeholders.

[A11-06] Los mensajes de error están vinculados al campo con aria-describedby.

[A11-07] Los modales atrapan el foco (focus trap) y devuelven el foco al elemento que los abrió al cerrarse.

 

15. Idioma, Tono y Copy
 

[LNG-01] Todo el copy de la plataforma está en español rioplatense (vos/tuteo, ej: 'Ingresá', 'Seleccioná', 'Completá').

[LNG-02] Toda string es internacionalizable (usa t('key')), pero el idioma por defecto y de lanzamiento es español.

[LNG-03] Los mensajes son directos, claros y empáticos. No usan jerga técnica.

[LNG-04] Naming oficial: 'organizaciones' (no 'empresas'), 'Espacios de Impacto' (no 'proyectos'), 'miembros' (no 'suscriptores'), 'Escudo Digital' (no 'membresía' a secas).

[LNG-05] Números se formatean con punto como separador de miles y coma como decimal (ej: 1.234,56). Estándar LATAM.

[LNG-06] Fechas se muestran en formato: '12 de marzo de 2026' (texto) o '12/03/2026' (compacto). Nunca MM/DD/YYYY.

[LNG-07] Moneda por defecto: USD. Se muestra como 'US$ 1.234,56'.

 

16. Semáforos y Estados de Proceso
Aplica a todo sistema que use estados progresivos o de validación.

 

[SEM-01] Los semáforos usan colores consistentes en toda la plataforma: rojo (incompleto/error), amarillo (pendiente/en revisión), verde (aprobado/habilitado), gris (rechazado/inactivo).

[SEM-02] El color del semáforo siempre va acompañado de texto descriptivo del estado. No se comunica solo con color.

[SEM-03] El usuario siempre puede ver por qué está en un estado determinado (detalle de campos faltantes, motivo de rechazo, etc.).

[SEM-04] Las transiciones de estado son visibles y comprensibles (ej: 'Tu perfil pasó de En revisión a Aprobado').

 

17. Notificaciones y Feedback Visual
 

[NOT-01] Los toasts aparecen en la esquina superior derecha en desktop, parte superior en mobile.

[NOT-02] Máximo 3 toasts visibles simultáneamente. Si hay más, se apilan.

[NOT-03] Colores de toast: verde (éxito), rojo (error), amarillo (warning), azul (info).

[NOT-04] La campana de notificaciones muestra badge con conteo de no leídas.

[NOT-05] El badge desaparece al abrir el panel de notificaciones.

[NOT-06] Cada notificación tiene: ícono de tipo, texto, fecha relativa ('hace 2 horas'), y link a la acción.

 

18. Performance Percibida
 

[PRF-01] Tiempo de respuesta de filtros y búsquedas: < 300ms percibido.

[PRF-02] Lazy loading en imágenes de grillas y listas.

[PRF-03] Las acciones del usuario dan feedback inmediato (optimistic UI donde aplique).

[PRF-04] Las animaciones y transiciones no exceden 300ms.

[PRF-05] No hay flickering de contenido (evitar layout shifts al cargar).

 

19. Cross-Browser
 

[BRW-01] Browsers soportados: Chrome (últimas 2 versiones), Safari (últimas 2), Firefox (última), Edge (última).

[BRW-02] Mobile: Safari iOS (últimas 2), Chrome Android (últimas 2).

[BRW-03] No se garantiza soporte para Internet Explorer.

 

 

20. Cómo Aplicar Este Documento
 

Este documento es normativo. Toda US Recargada hereda estos mandatos automáticamente.

 

[USO-01] En la US no se repiten los mandatos de este documento. Solo se referencia: 'Aplican mandatos generales'.

[USO-02] Si un requerimiento necesita desviarse de un mandato, la US lo documenta explícitamente con el código del mandato y la excepción (ej: 'Excepción a TXT-01: el campo de manifiesto usa maxlength 1000').

[USO-03] Dev construye respetando estos mandatos. Si no hay excepción en la US, aplica el estándar.

[USO-04] QA testea contra estos mandatos. Si algo no se cumple y no hay excepción, es un defecto.

[USO-05] El documento se versiona. Cambios requieren aprobación de QA y Dev.

 

21. Navegación y CTAs
[NAV-01] Todo CTA debe llevar al destino funcional prometido por el texto del botón.

 

[NAV-02] Los enlaces provenientes de emails deben redirigir al módulo correspondiente dentro de la plataforma.

 

[NAV-03] Si un módulo aún no está disponible, el CTA debe estar deshabilitado o mostrar un mensaje claro indicando que la funcionalidad estará disponible próximamente.

 

[NAV-04] Nunca se redirige a páginas placeholder sin contexto para el usuario.

 

[NAV-05] Los deep links deben incluir el identificador del recurso correspondiente (ej: /spaces/{id}).

 

 

22. Consistencia de Componentes
[DS-01] Un mismo tipo de acción debe usar el mismo componente UI en toda la plataforma.

 

[DS-02] Elementos críticos del sistema (checkbox de términos, selects de país, confirmaciones) deben utilizar componentes del Design System oficial.

 

[DS-03] No se permite duplicar componentes con comportamiento diferente para la misma función.

 

[DS-04] QA debe reportar cualquier divergencia de componente como defecto de consistencia UI.

 

 

23. Consistencia Semántica
[SEM-05] Los términos oficiales definidos en el glosario del producto deben usarse de forma consistente en toda la plataforma.

 

[SEM-06] No se permiten variaciones de naming para el mismo concepto (ej: Organización / Perfil Organización).

 

[SEM-07] Los nombres de módulos, roles y entidades deben coincidir entre UI, emails y documentación.

 

 

24. Confirmación de Acciones
[ACT-01] El sistema solo puede mostrar mensajes de éxito cuando la operación haya sido confirmada por el backend.

 

[ACT-02] No se deben mostrar mensajes de éxito optimistas en acciones críticas (envío de emails, transacciones, invitaciones).

 

[ACT-03] Si la operación falla, se debe mostrar error claro con posibilidad de reintentar.

 

 

25. Promesas de UI
[PRM-01] Ningún texto de interfaz puede prometer funcionalidades inexistentes.

 

[PRM-02] Si la interfaz indica que una acción puede realizarse desde un módulo (ej: perfil), dicha acción debe existir en ese módulo.

 

[PRM-03] QA debe validar coherencia entre promesas de interfaz y funcionalidad disponible.
