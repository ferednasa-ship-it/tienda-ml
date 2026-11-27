# Stock Conecta · necesidades y alcance

## Respuesta y contexto

**Edna Fernanda Sánchez Cabrera**, México, nivel principiante. Respuesta del 24/11/2026, 7:35:25 p.m. Correo aportado: fer.ednasa@gmail.com. Indicó que vende mercadería por Mercado Libre, no tiene web y busca “mi propio punto de venta, que actualice stoc, precios, publicaciones” y, especialmente, que un agente consulte stock en páginas del proveedor y en el Excel que ella envía. También desea actualizar stock de proveedor y bodega para vender.

## Necesidad inferida

La primera condición para automatizar ventas es una identidad estable por SKU y separar la disponibilidad propia del stock reportado por terceros. Importar una cifra sin fecha ni origen puede producir una promesa de venta incorrecta. Antes de conectar Mercado Libre, conviene probar una operación trazable con sus archivos reales.

## Entrega funcional

| Necesidad | Función entregada | Criterio de aceptación |
|---|---|---|
| Unificar referencias | Crear, editar, buscar y eliminar SKU bajo controles | Un SKU repetido se rechaza; el identificador se mantiene al editar |
| Stock propio y reservas | Registro separado y disponibilidad calculada | Disponible = bodega − reservas, nunca negativo |
| Leer Excel del proveedor | Lector XLSX OpenXML real y CSV, selección de hoja, matching y vista previa | Un XLSX de xlsxwriter y otro de openpyxl se leen; una fórmula sin caché se rechaza |
| Actualizar proveedor | Diferencias por SKU, origen y fecha, confirmación | Solo cambian datos del proveedor; costo propio, bodega y precio permanecen |
| Punto de venta | Venta local y reversión única con motivo | No vende reservas ni stock proveedor; la reversión repone las unidades una vez |
| Revisar publicaciones | Exportación del catálogo completo en CSV | Se identifica disponibilidad propia y datos externos; no se publica automáticamente |
| Conservar registros | Respaldo JSON y restauración validada con confirmación | Archivo inválido no modifica el estado; en almacenamiento bloqueado se avisa y se conserva en memoria |

## Diseño y contenido

Producto orientado al comercio: blanco, frambuesa y berenjena; inicio con ilustración nativa del vínculo bodega/reservas/proveedor, catálogo como área principal y POS diferenciado. Cuatro páginas de contenido real, navegación accesible, 404, tablas desplazables y fuentes locales. Todo comienza vacío. Las únicas cifras sintéticas están en pruebas automatizadas que no se cargan en el sitio.

## Límites deliberados

No hay cobros, comprobantes fiscales, cuenta multiusuario, scraping, lectura remota, cron, API de Mercado Libre ni IA conectada. El precio usa reglas explícitas; no consulta comisiones ni fija impuestos. XLSX tiene límites de tamaño y estructura documentados en LEEME; los formatos avanzados no interpretables se rechazan. Un resultado de fórmula guardado puede estar desactualizado y se advierte en la vista previa.

## Datos faltantes y siguiente integración

Se requieren un Excel real del proveedor y sus URL, permiso/API/feed disponible, significado del stock y sus presentaciones; además, el catálogo de publicaciones/variaciones de Mercado Libre. La fase conectada necesita una aplicación con OAuth y permisos, backend seguro para tokens, política de actualización y conciliación de ventas. No introducir secretos en HTML ni localStorage. Primero autorizar una lectura y contrastarla con la fuente; después definir pruebas y revisión para escrituras de stock/precio.

## Primer ejercicio práctico

Crea un SKU de tu catálogo real con bodega y reservas verificadas. Completa una fila de la plantilla del proveedor con el mismo SKU, fecha y fuente. Prepara la vista previa; confirma solo tras comprobar que la coincidencia corresponde a la misma presentación. Revisa que la bodega no cambió, registra una venta dentro de tu disponible y descarga el respaldo. Si pruebas una reversión, documenta que es un ejercicio y verifica las unidades devueltas.

## Verificación y fuentes

Consulta PRUEBAS.md. La revisión se realizó sin navegador ni publicación. Fuentes técnicas oficiales y licencias en RECURSOS_Y_LICENCIAS.txt, consultadas el 25/11/2026.

## Concordancia revisada el 26 de noviembre

El punto de venta local, la separación entre proveedor y bodega y el cálculo del precio por una regla introducida están disponibles. Leer el Excel que Edna envía está parcialmente cubierto: existe un lector XLSX real, pero falta su archivo para comprobar sus encabezados y estructura. Su prioridad de que un agente consulte las páginas del proveedor y actualice Mercado Libre sigue pendiente de fuentes y conexión; el CSV de catálogo no publica ni sincroniza. La importación del proveedor conserva costo propio y precio: no decide automáticamente que el costo importado deba sustituirlos.
