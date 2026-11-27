# EDNA FERNANDA SANCHEZ CABRERA · Stock Conecta

**Contexto del formulario:** mexico; nivel principiante; situación web declarada: `no_tengo`.

La operación local concuerda con venta e inventario por SKU. La lectura del Excel real de Edna requiere validar su estructura. Su prioridad de agente proveedor y sincronización de Mercado Libre sigue pendiente.

| Solicitud del formulario | Correspondencia comprobada | Estado | Qué falta o debe validarse |
| --- | --- | --- | --- |
| **Registrar ventas sobre disponibilidad propia.** — «mi propio punto de venta» | Registra ventas locales, calcula su total y descuenta únicamente la disponibilidad de bodega después de reservas. Permite revertir una venta una sola vez y conservar el motivo. | Disponible localmente | El alcance es un registro local: no procesa pagos ni emite comprobantes fiscales. |
| **Distinguir y actualizar stock de proveedor y bodega.** — «el stoc con mis proveedores y en bodega se actualice para la venta.» | Muestra por separado bodega, reservas y stock del proveedor. La bodega se actualiza con las operaciones locales y el proveedor mediante un archivo revisado y confirmado. | Cubierto parcialmente | Bodega cambia por operación manual/venta local y proveedor por archivo confirmado; no hay lectura automática ni conciliación de ventas remotas. |
| **Definir y actualizar precios mediante reglas.** — «actualizacion de stoc, precios.» | Calcula el precio a partir del costo propio y el recargo indicado, o permite fijarlo manualmente. Conservar el costo del proveedor por separado evita cambiar el precio sin una decisión explícita. | Disponible localmente | El costo importado del proveedor no cambia automáticamente costo propio o precio. Faltan reglas completas para automatizar esa decisión y las comisiones/envíos/impuestos aplicables. |
| **Actualizar publicaciones de Mercado Libre.** — «publicaciones» | Exporta un catálogo CSV con precios, disponibilidad propia y datos del proveedor para revisión. No modifica publicaciones ni sincroniza con Mercado Libre. | Requiere insumo o conexión | Cuenta/aplicación autorizada, relación SKU/publicación/variación, reglas de precio y stock, servicio de conexión y conciliación. El CSV no publica. |
| **Consultar stock en las páginas del proveedor mediante agente.** — «que mi agente busque stoc en las paginas de mi proveedor» | Permite cargar una copia de los datos del proveedor y conservar su fecha y origen. No hay un agente que visite sus páginas o busque stock automáticamente. | Requiere insumo o conexión | URL del proveedor, método permitido de acceso, significado del stock, presentaciones, frecuencia y conector autorizado. No se ejecuta un agente de consulta. |
| **Leer el Excel que suministre Edna.** — «excel que yo le mando» | Lee archivos XLSX y CSV con los encabezados admitidos, permite seleccionar una hoja y muestra coincidencias y diferencias antes de actualizar. Falta contrastar ese recorrido con el Excel real de Edna. | Cubierto parcialmente | Hay lector real de XLSX/CSV con encabezados definidos y límites documentados. Falta el archivo real para validar su formato o preparar un mapeo de sus columnas. |
| **Disponer de una web para manejar esa operación.** — «me gustaria crear una donde el stoc con mis proveedores y en bodega se actualice para la venta.» | Incluye una web con presentación, método, catálogo, punto de venta y contacto. Los registros funcionan en el navegador de la persona que utiliza la herramienta. | Disponible localmente | La entrega es un espacio individual del navegador. La operación compartida y las actualizaciones externas requieren servicios adicionales. |

### Ajustes realizados en esta revisión

- La portada aclara que XLSX/CSV deben usar los encabezados admitidos, sin prometer interpretar cualquier libro de Excel.
- Se explicita la cobertura parcial del Excel real y la prioridad pendiente de consultar proveedor/sincronizar Mercado Libre.

### Evidencia y verificación dirigida

- Lectura de formulario, cuatro páginas, guía y product/upsert/sell/supplierPreview/applySupplier/catalogCSV.
- Contraste de hashes confirma que no cambió ningún JS, cálculo, clave o esquema.
- IDs, enlaces y fragmentos locales PASS. No se repitieron pruebas de funciones sin cambios.

**Documentación del proyecto:** [Ficha de necesidades y alcance](NECESIDADES_Y_ALCANCE.md) · [Instrucciones](LEEME.txt).
