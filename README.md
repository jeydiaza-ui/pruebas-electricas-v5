# Pruebas de Transformadores — v2 (5.1.0)

Aplicación web para registrar y documentar pruebas de transformadores en campo:

- **Índice horario y cableado**.
- **Relación de transformación (TTR / red)**.
- **Resistencia de aislamiento**.
- **Resistencia de devanados**.
- **Pruebas de aceite AFQ y PCB** (PDF de laboratorio convertido a imágenes o formato propio).
- **Informe** con datos del cliente y del equipo, tablas, fotos, observaciones, impresión a PDF y exportación JSON.

Versión actual: **5.1.4** (2026-11-04).

- App publicada: <https://jeydiaza-ui.github.io/v2/>
- Repositorio: <https://github.com/jeydiaza-ui/v2>
- Versión anterior: **v1** (4.0.0) en <https://jeydiaza-ui.github.io/v1/>

## Aceite

- Selector **AFQ / PCB / ambos**.
- **PDF de laboratorio:** se convierte a imágenes con PDF.js local y queda dentro del informe.
- **Formato propio AFQ:** datos de la muestra prellenados desde el informe, tabla fija con referencias nuevas / en servicio ≤69 kV / >230 kV; solo se editan resultados y comentarios.
- **Formato propio PCB:** solo se editan los resultados de la tabla.
- **Cliente guardado:** en Datos del cliente puedes elegir un cliente de un informe anterior; el equipo se llena aparte.

## Fotos

- Vista previa al tocar una foto.
- Recuadros uniformes al imprimir, sin cortes entre páginas.
- Exportar JSON incluye las fotos y lecturas actuales.

## Datos

- Almacenamiento propio de la v5 (`v5_` y `unif_informes_v5`), separado de la v1/v4.
- Los informes de la v1 se pueden pasar con Exportar/Importar.
