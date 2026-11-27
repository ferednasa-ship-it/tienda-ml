# Verificación técnica · 26/11/2026

**Resultado: 23 pruebas aprobadas, 0 fallos.** 10 pruebas de núcleo y XLSX + 4 de interfaz + 9 regresiones de la revisión.

## Cómo reproducir

Desde esta carpeta, con Node.js 24 o un runtime compatible:

```bash
node --test pruebas/*.test.cjs
```

El sitio no requiere Node para utilizarse: estas herramientas son únicamente de desarrollo. El arnés de pruebas es un DOM en memoria que ejecuta assets/app.js y assets/core.js reales; no abre navegador, no renderiza páginas, no captura pantallas ni consulta la red. pruebas/dom.json es la estructura semántica extraída de herramientas.html para estos flujos. La revisión se limitó a este proyecto y preservó su esquema de respaldo versión 1.

## Alcance comprobado

- Estado inicial vacío y datos de prueba aislados, nunca cargados por el sitio.
- Validaciones de fechas, números, identificadores y relaciones.
- Operaciones exitosas y rechazo atómico: un dato inválido mantiene el estado anterior.
- Exportaciones y manejo de texto de usuario sin interpretación como HTML; CSV protegido contra fórmulas.
- Formularios reales, confirmaciones, vista previa y almacenamiento local bloqueado con conservación en memoria.
- Cinco páginas con idioma, un h1 por página, IDs únicos, labels de formularios y rutas/anchors locales existentes.
- Sintaxis Node en los JavaScript de assets, ausencia de CDN y existencia de recursos CSS/fuentes.

## Límites de verificación

No hubo inspección visual en navegador por la restricción previa del encargo. La adaptación a 320 px, contraste, foco, menú móvil, tablas con scroll local y movimiento reducido se revisaron en CSS y estructura; no se afirma una captura o prueba visual. No se probó la publicación en Netlify ni una conexión externa, porque no forman parte de la entrega autorizada. La lectura XLSX depende de soporte de DecompressionStream para deflate-raw; el código comunica una alternativa CSV si no existe.

## Casos específicos de Stock Conecta

- Recargo sobre costo, reservas y disponibilidad propia.
- Venta que descuenta únicamente bodega disponible; venta excesiva bloqueada.
- Reversión una sola vez y motivo obligatorio.
- Proveedor con SKU coincidentes y desconocidos, fuente anterior rechazada y catálogo propio intacto.
- Libros XLSX reales creados por xlsxwriter y openpyxl: múltiples hojas, shared strings e inline strings, ceros iniciales de SKU textual, fecha Excel estándar, texto con caracteres XML y fórmula con caché.
- Fórmula sin resultado guardado, archivo corrupto y XML externo rechazados.
- Restauración con vista previa y confirmación, exportación y protección de texto adversarial.

Los XLSX de pruebas/fixtures contienen datos sintéticos etiquetados para QA; no son archivos aportados por Edna. La plantilla de assets/plantilla_proveedor.xlsx está vacía excepto por encabezados.

## Regresiones de la revisión del 26 de noviembre

- Aritmética monetaria decimal exacta y compatibilidad con un respaldo sintético generado por la versión anterior. El esquema y la clave de almacenamiento permanecen iguales.
- Fichas abiertas que ya no pueden sobrescribir operaciones posteriores, lecturas de archivo fuera de orden y restauración bloqueada si cambian los datos durante la confirmación.
- Capacidad de respaldo medida en bytes UTF-8 antes de modificar memoria o almacenamiento. Un archivo con 12.000 entradas de QA se exporta compacto y se restaura; un estado con 15.000 entradas extensas que excede 15 MiB se rechaza sin mutación. Esa prueba aísla el componente real de almacenamiento y respaldo; no es una prueba de rendimiento de tablas.
- Las herramientas siguen iniciando vacías. Todos los registros de estas pruebas son sintéticos y están únicamente en pruebas/.

La estructura semántica del DOM se puede regenerar sin navegador con `python pruebas/generar_dom.py`. Después se ejecuta nuevamente la orden de pruebas anterior.

Stock Conecta conserva precios y totales históricos al validar, restaurar o importar proveedor. El recargo se recalcula al guardar explícitamente una ficha. Se comprobaron tanto XLSX real como cambios de selección durante su lectura, la separación de stock propio/proveedor y el error visible dentro del diálogo.
