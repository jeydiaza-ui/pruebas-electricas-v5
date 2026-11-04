# Cambios

## v5.0.3 — 2026-11-04

- **Quitar o cambiar fotos en el modo automático.** En cada paso aparece **Quitar foto** y una tira de **“Fotos montadas en esta prueba”** con una × en cada miniatura.
- Al quitar una foto se elimina de la prueba (no queda duplicada), se puede tomar otra y el valor ya escrito se conserva.
- Al volver atrás y confirmar de nuevo, las fotos se sincronizan: nunca se duplican.
- Caché `transformadores-pwa-v5.0.3-2026-11-04` y versión visible 5.0.3.

## v5.0.2 — 2026-11-04

- **El informe ya no mezcla posiciones viejas.** Al tocar **Comenzar captura**, el asistente borra las lecturas y fotos actuales de las pruebas seleccionadas (pide confirmación si hay datos). Así, si se elige “solo la posición actual”, el informe muestra únicamente esa posición, aunque antes hubiera lecturas de otras posiciones o fotos acumuladas.
- **OCR del TTR mejorado.** El lector ahora usa segmentación de bloque (PSM 6) para capturar **todos** los números de la pantalla (tap, ratio, error, tensión), no solo el primero.
- **Selección del valor correcto.** En TTR se elige el número más cercano a la relación teórica de esa posición; si no hay teórica, se prioriza el número con decimales. Debajo del valor aparecen **todos los números detectados** como botones para elegir otro con un toque.
- Aviso “coincide con la teórica” cuando el valor leído está dentro del 5 % de la relación esperada.
- Caché `transformadores-pwa-v5.0.2-2026-11-04` y versión visible 5.0.2.

## v5.0.1 — 2026-11-03

- **Almacenamiento separado de la v4.** La v5 usa claves con prefijo `v5_` y su propia base `unif_informes_v5`; ya no muestra ni modifica los informes de la v4.
- Los informes de la v4 se pueden pasar a la v5 con **Exportar** en la v4 e **Importar** en la v5 (la importación traduce las claves).
- Caché `transformadores-pwa-v5.0.1-2026-11-03` y versión visible 5.0.1.

## v5.0.0 — 2026-11-03

Base: v4.0.0 (2026-10-26).

### Nuevo: modo automático con fotos guiadas

- Selector **Manual / Automático** en la barra. El modo manual queda igual que en la v4.
- Asistente que pide las fotos en el orden del formulario y las adjunta a la prueba correcta.
- **TTR:** opción “solo posición actual” o “todas las posiciones”. Pide la posición actual (bobinas A, B y C) y luego las demás posiciones 1…n sin repetir la actual.
- **Aislamiento:** pide AT–BT, AT–T y BT–T según el tipo de transformador (en monofásico solo AT–BT) y los tiempos de la prueba (puntual, DAR, PI, escalonada o rampa).
- **Devanados:** posiciones de AT y BT, con las tres fases o la única lectura en monofásico.
- **Índice horario:** foto de la placa de conexión adjunta a la prueba.
- Cada valor se pasa a la prueba al confirmarlo; los cálculos y el informe se actualizan solos.

### Nuevo: lector OCR local

- Tesseract.js incluido en `ocr/` (sin enviar fotos a internet).
- Preprocesado de la foto (gris, inversión de fondo oscuro, límite a números) y propuesta del valor con nivel de confianza.
- Selector de unidad por foto (“El equipo muestra”: kΩ/MΩ/GΩ u Ω/mΩ) con conversión automática a la unidad de la prueba.
- **Preparar lector** descarga y cachea los archivos; después funciona sin conexión. El modelo de idioma queda en IndexedDB y no se vuelve a descargar.
- Si la lectura falla o la confianza es baja, el campo queda para escribir a mano.
- En `file://` (doble clic) el lector avisa que debe abrirse desde la URL publicada o un servidor local.

### Otros

- Versión y caché v5 (`transformadores-pwa-v5.0.0-2026-11-03`).
- README con el flujo automático, la preparación del lector y la publicación con `ocr/`.
- El informe muestra la versión de la app.

### Límites conocidos

- La precisión del OCR depende de la foto: pantalla cerca, enfocada y sin reflejo. En LCD con brillo o ángulo puede fallar; por eso nunca se guarda sin confirmación.
- El modo automático no cambia criterios, tensiones de prueba ni topes: esos se ajustan en modo manual.
- Si el equipo cambia de escala y no se ajusta “El equipo muestra”, el valor puede quedar multiplicado o dividido por 1000. La app muestra la conversión para revisarla.
- Las fotos del asistente se guardan a 1600 px (más pesadas que las 1000 px del modo manual).

## v4.0.0 — 2026-10-26

Base: v3 del 12/10/2026.

### Nuevo

- Versión visible en la barra y en el pie del informe.
- **Exportar todo**: respaldo único en JSON con todos los informes guardados.
- **Importar informe o respaldo**.
- Código de empresa/técnico en el consecutivo (`INF-JD-0001`).
- Aviso y bloqueo al guardar un número ya usado por otro informe.
- Observaciones en **Índice horario**.
- Indicador de espacio usado y de almacenamiento persistente.
- Solicitud de almacenamiento persistente.
- Iconos *maskable* 192 y 512.
- `beforeprint` y estilo `@page` A4.
- Validación estricta del JSON importado y de las imágenes.

### Corregido

- Números con separador de miles (`13.200` = 13.200 V) en tensiones.
- Inyección de HTML desde un JSON importado.
- Tarjetas vacías de cliente/equipo en el informe.
- “Pasmount” → “Pad-mounted”.
- Norma de aislamiento: NETA ATS 100.5 en lugar de IEC 60085.
- Aviso de DAR mínimo muy bajo.
- Service worker: solo mismo origen, `index.html` solo en navegaciones.
- Código muerto en TTR.

## v3 — 2026-10-12

- Exportar/importar un informe en JSON.
- Campos de cliente y equipo ampliados.
- Mejoras de impresión y ajuste del grupo Dy5.
- Guardado de informes en IndexedDB con fotos.

## v2 — 2026-10-10

- Informe consolidado con fotos, logo y guardado local.

## v1 — 2026-10-03

- Versión inicial: índice horario, TTR, aislamiento y devanados.
