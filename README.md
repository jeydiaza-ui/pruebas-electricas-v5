# Pruebas de Transformadores (PWA)

Aplicación web para registrar y documentar pruebas de transformadores en campo:

- **Índice horario y cableado** (grupos Yy, Dy, Yd, Dd; polaridad monofásica).
- **Relación de transformación** (TTR o tensión de red, por fase y por posición de tap).
- **Resistencia de aislamiento** (puntual, DAR, PI, escalonada y rampa; corrección a 20 °C).
- **Resistencia de devanados** (corrección por temperatura, desbalance y comparación con fábrica).
- **Informe** con datos de empresa y cliente, tablas, gráficos, fotos, observaciones, impresión a PDF y exportación JSON.

Versión actual: **5.0.6** (2026-11-04).

- App publicada: <https://jeydiaza-ui.github.io/pruebas-electricas-v5/>
- Repositorio: <https://github.com/jeydiaza-ui/pruebas-electricas-v5>
- La versión anterior (v4) sigue disponible en <https://jeydiaza-ui.github.io/pruebas-transformadores./>

## Dos modos de trabajo

### Manual (el de siempre)

Eliges la prueba, cargas las fotos donde quieras y escribes las lecturas. Es el modo recomendado para revisar o corregir datos.

### Automático (fotos guiadas)

El asistente pide cada foto en el orden del formulario, intenta leer el valor y lo pasa a la prueba después de que lo confirmes.

1. Elige el tipo de transformador y las pruebas.
2. Toca **Automático** y completa la configuración:
   - **TTR:** solo la posición actual o todas las posiciones, y cuál es la posición actual.
   - **Aislamiento:** prueba (puntual, DAR, PI, escalonada, rampa), aislamiento (aceite/seco) y unidad.
   - **Devanados:** solo la posición actual o todas, y la posición actual de AT y BT.
3. Toca **Preparar lector** la primera vez (descarga ~7 MB y queda disponible sin internet).
4. La app pide: Índice horario (placa) → TTR (posición actual A/B/C y luego las demás posiciones sin repetir) → aislamiento (AT–BT, AT–T, BT–T con sus tiempos) → devanados (AT y BT por posición).
5. En cada foto puedes confirmar el valor, corregirlo o cambiarlo de unidad si el equipo cambió de escala.
6. Si una foto quedó mal, usa **Quitar foto** o la × de las miniaturas **“Fotos montadas en esta prueba”**; puedes tomar otra sin duplicarla.
7. Toca una foto (en el formulario, en el asistente o en el informe) para verla completa; × o tocar fuera para cerrar.
8. Al final, **Ver informe**.

## Lector de fotos (OCR local)

- Usa **Tesseract.js** incluido en la app (`ocr/`), sin enviar fotos a internet.
- Funciona mejor con la pantalla del instrumento **de cerca, enfocada y sin reflejos**. La app convierte a gris, invierte si el fondo es oscuro y limita el reconocimiento a números.
- **Siempre hay que confirmar**: un dígito mal leído puede cambiar un dictamen. Si la lectura falla, el campo queda para escribir a mano.
- El OCR no adivina la unidad: si el equipo muestra GΩ y la prueba está en MΩ, selecciona **GΩ** en “El equipo muestra” y la app hace la conversión.
- La primera preparación necesita internet. Después funciona sin conexión (archivos en la caché y datos del idioma en IndexedDB).
- **No funciona abriendo el archivo con doble clic (`file://`)**: usa la URL publicada o un servidor local.

## Datos separados de la versión 4

La v5 **no comparte los informes ni las claves con la v4**, aunque las dos estén en `jeydiaza-ui.github.io`:

- La v5 guarda en claves con prefijo `v5_` (por ejemplo `v5_ttr2_3`) y en una base propia `unif_informes_v5`.
- La v4 sigue usando sus claves y `unif_informes`. Abrir o guardar en una no cambia la otra.
- Para pasar un informe de la v4 a la v5: en la v4 usa **Exportar** (o **Exportar todo**) y en la v5 usa **Importar informe o respaldo**. La importación traduce las claves a `v5_`.
- Borrar los datos del sitio en el navegador borra las dos versiones, porque comparten el origen; mantén respaldos.

## Dónde quedan los datos

Todo se guarda **solo en el navegador de ese dispositivo**:

- `localStorage`: datos del trabajo en curso y preferencias.
- `IndexedDB` (`unif_informes`): informes guardados con sus fotos.

No hay servidor, cuenta ni nube. Si se borran los datos del sitio, se cambia de navegador o de dispositivo, los informes desaparecen.

- Usa **Exportar todo** para descargar un respaldo `transformadores_respaldo_AAAA-MM-DD.json`.
- Restaura con **Importar informe o respaldo**.
- La app pide almacenamiento persistente al guardar y muestra el espacio usado; aun así, un respaldo externo es la única protección real.

## Estructura del repositorio

```
index.html                 aplicación completa (4 pruebas embebidas + asistente)
manifest.json              manifiesto PWA
service-worker.js          caché y funcionamiento sin internet (v5.0.6)
icon-192.png / icon-512.png            iconos normales
icon-maskable-192.png / -512.png       iconos para Android (zona segura)
ocr/tesseract.min.js                   lector OCR (interfaz)
ocr/worker.min.js                      worker del lector
ocr/tesseract-core-simd-lstm.wasm.js   motor OCR
ocr/eng.traineddata.gz                 modelo de lenguaje (números)
README.md
CHANGELOG.md
```

## Publicar una versión nueva

El sitio se publica con **GitHub Pages** desde la rama `main` (raíz del repositorio).

1. Cambia `APP_VERSION` en `index.html` y el texto visible `#ver` / `#repver`.
2. Sube `CACHE_NAME` en `service-worker.js` con la misma versión y fecha (por ejemplo `transformadores-pwa-v5.0.6-2026-11-04`).
3. Actualiza `CHANGELOG.md`.
4. Sube **todos** los archivos, incluida la carpeta `ocr/`.
5. Haz commit y push a `main`. GitHub Pages publica en 1–2 minutos.
6. Abre la URL, recarga y verifica que el pie muestre la versión nueva y que “Preparar lector” funcione.

## Decisiones y límites

- **Criterios de aceptación editables.** Los valores por defecto (resistencia mínima, DAR, PI, tolerancias) son referencias de trabajo; ajústalos al procedimiento de tu empresa y a la norma aplicable antes de usarlos como dictamen.
- **Normas citadas como referencia**, no como certificación: IEC 60076-1, IEEE C57.12.90, IEEE 43 y NETA ATS tabla 100.5.
- **Cálculos**: corrección por temperatura 2 por 10 °C en aceite y 1,584 por 10 °C en seco; devanados con K = 234,5 (cobre) y 225 (aluminio).
- **Datos de clientes**: la app no cifra el almacenamiento local. En equipos compartidos, cualquiera que abra el navegador puede ver los informes.
- **Fotos**: el asistente guarda 1600 px JPEG 0,82; el modo manual, 1000 px JPEG 0,72.

## Licencia y responsabilidad

Uso interno. Sin garantía: verifica los resultados antes de emitir un dictamen.
