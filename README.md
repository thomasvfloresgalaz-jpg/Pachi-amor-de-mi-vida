# Dulce Control ♡ — versión inicial

Aplicación PWA independiente para Android. Gestión local de productos, paquetes, producción, inventario, ventas en efectivo/transferencia, caja, gastos, estadísticas y respaldos.

## GitHub → Render
1. Crea un repositorio nuevo llamado `dulce-control` en GitHub.
2. Sube **todos los archivos de esta carpeta a la raíz** del repositorio (no subas solamente el ZIP).
3. En Render, crea **New → Web Service**, conecta ese repositorio y usa:
   - Runtime: **Node**
   - Build command: `npm install`
   - Start command: `npm start`
   - Health check path: `/healthz`
4. Espera el despliegue y abre la URL HTTPS de Render en Chrome Android.
5. Menú de Chrome → **Agregar a pantalla principal** o **Instalar aplicación**.

## Importante
- Datos guardados en **IndexedDB del navegador del teléfono**, no en GitHub ni Render. No se sincronizan entre dispositivos.
- Exporta periódicamente el respaldo JSON desde **Más → Descargar respaldo** y guárdalo fuera del teléfono. Borrar datos del sitio o desinstalar puede borrar la información.
- Catálogo inicial vacío. Los paquetes utilizan unidades del stock de productos individuales.
- En modo Resumen, ingresa **solo ventas aún no registradas**. No repitas ventas rápidas ya guardadas.
- La cuadratura usa fondo inicial, ventas en efectivo y gastos pagados desde caja. Para retiros no relacionados con gastos, registra un movimiento de caja claramente identificado como retiro (la versión inicial los muestra en gastos; se mejorará con un libro de movimientos específico).
- El saldo ventas menos gastos **no es utilidad neta**.
- No se incluyen personajes ni imágenes oficiales de Hello Kitty; el diseño usa guiños discretos como moñitos.

## Actualizaciones
Cualquier commit nuevo en la rama conectada puede activar el despliegue automático de Render. Los datos locales permanecen normalmente al actualizar archivos del mismo origen, pero haz respaldo antes de cambios grandes.

## Actualización 1.0.2
- Diseño más delicado, botones redondeados y navegación inferior suavizada.
- Al crear/editar un dulce, ingresar cantidad disponible directamente; el sistema guarda la diferencia como movimiento.
- Productos con precio unitario $0 para los que se venden exclusivamente en bolsitas.
- Bolsitas con precio independiente, descontando los dulces que contienen. Ejemplos: 3 alfajores por $1.000 y 4 cuchuflís por $1.000.
- Sin campo de fotografía.
- Montos en pesos chilenos con signo $ y separador de miles en formularios de dinero.
- Caja explicada paso a paso y compras de ingredientes aclaradas.
- Los datos existentes en IndexedDB no se borran al actualizar los archivos.

## Versión 1.0.3
Barra inferior reducida a las proporciones originales (v1), conservando los iconos estilizados de v1.0.2. Sin cambios en los datos o funciones.


## Versión 1.0.5 — Pachi
- Barra inferior compacta con iconos SVG de trazos finos, sin símbolos geométricos improvisados.
- Transiciones suaves al cambiar de pantalla y abrir formularios.
- Bolsitas independientes: nombre, unidades por bolsita, cantidad de bolsitas listas y precio; no exige producto individual.
- Deslizar tarjetas de productos y bolsitas hacia la izquierda para mostrar Eliminar. La eliminación pide confirmación y bloquea artículos con ventas históricas.
- Se conservan las bolsitas antiguas y los registros de IndexedDB; las bolsitas antiguas vinculadas siguen funcionando.
- Para ventas existentes, exporta respaldo JSON antes de actualizar.


## Versión 1.0.6 — Compras simplificadas
- Cantidad y precio por unidad, total automático.
- Métodos de pago para compras: Efectivo, Tarjeta y Dinero personal.
- Compras anteriores se mantienen compatibles, incluso si tienen métodos antiguos.
- La caja resta solo las compras registradas como efectivo; tarjeta y dinero personal quedan en el historial sin restarse del efectivo.
- Los métodos de pago de ventas no se modificaron.


## Versión 1.0.8 — Eliminar compras registradas por error
- En **Más → Compras y gastos**, cada compra registrada tiene un botón visible **Eliminar**, incluso si existen otras compras iguales.
- Antes de borrar, se solicita una confirmación con el nombre, monto y fecha de la compra.
- Tras eliminar, se recalculan automáticamente las compras del día, las estadísticas y el efectivo esperado en Caja. Los cierres ya guardados permanecen intactos para que puedas revisar la diferencia si corresponde.
- No se modifican el inventario, los productos, las ventas ni las demás compras.
- La lista permite pulsar **Ver más compras** para corregir registros más antiguos.
- Los registros anteriores y el almacenamiento IndexedDB se conservan al actualizar la versión, siempre que uses el mismo dominio y navegador. Haz respaldo antes de reemplazar los archivos.


## Nuevo en v1.0.8: insumos y reabastecimientos

- Compras de insumos iguales se agrupan por nombre (sin diferenciar mayúsculas, tildes o espacios dobles).
- Cada grupo muestra compras, cantidad disponible, inversión disponible y último precio.
- Reabastecer prellena el último precio y método de pago, y permite ajustar cantidad, precio y fecha. Se crea una nueva compra sin reemplazar historial.
- Marcar todo agotado: retira el valor de compra de ese insumo del indicador de insumos disponibles en Caja, pero NO altera los gastos históricos ni el cuadre de efectivo.
- Cada compra puede marcarse Agotado, Reactivar o Eliminar. Reactivar es útil ante errores.
- El historial de precios/compras anteriores se puede desplegar debajo del grupo.
- Las compras antiguas se consideran insumos disponibles hasta que se marquen agotadas; si alguna compra era un gasto que no es insumo, eliminarla y volver a anotarla como «Otro gasto» (con respaldo previo) o dejarla disponible para corrección futura.
- El formulario de compra permite elegir «Insumo» (predeterminado) u «Otro gasto»; los gastos no aparecen como insumos disponibles.
- No se añadieron alertas «queda poco», cálculo de costos de producción ni nuevas reglas sobre dinero personal, según preferencia.

**Importante:** el indicador de insumos disponibles es el valor de las compras aún no marcadas como agotadas, y NO equivale a inventario exacto, efectivo disponible ni beneficio. Si se consumió parte de un paquete seguirá contando completo hasta marcarlo agotado.

Antes de reemplazar archivos, utilizar «Más → Descargar respaldo JSON». No borrar datos del navegador ni instalar con otro dominio si se necesita conservar el progreso.
