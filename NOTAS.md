# Mis gastos — notas del proyecto

App personal de ingresos y gastos para iPhone. Funciona sin internet (PWA) y guarda los datos solo en el móvil (IndexedDB).

## Dónde está
- App: https://lplansfernandez-hub.github.io/mis-gastos/
- Repositorio (público, rama main, raíz): https://github.com/lplansfernandez-hub/mis-gastos
- Se actualiza subiendo los archivos cambiados al repositorio (Add file → Upload files → Commit changes). Si cambia el código, subir `sw.js` con el número de `CACHE` aumentado (ahora `mis-gastos-v3`).

## Archivos
- `index.html`: toda la app (HTML, CSS y JS). El bloque entre `/*PURE-START*/` y `/*PURE-END*/` son funciones puras (importación CSV/JSON).
- `sw.js`: service worker para el modo sin internet.
- `manifest.webmanifest` e iconos: instalación en pantalla de inicio.
- `importar_expense_manager.csv`: resumen mensual ene–oct 2026 de la app Expense Manager (72 movimientos). Importar una sola vez.

## Funciones
- Balance del año y de cada mes, calendario con el neto de cada día, hoja inferior para añadir/editar movimientos.
- Gastos: Comida, Transporte, Home, Compras, Inversiones, Otros. Ingresos: Trabajo, Depósito.
- Categorías propias: crear, renombrar y eliminar (si están vacías), en Datos → Gestionar categorías o con "+ Nueva" al apuntar.
- Al guardar un movimiento se cierra la ventana.
- Tocar una categoría del resumen abre sus movimientos del periodo (mes o año), ordenables por fecha o por importe; tocar uno lo abre para editarlo.
- Calendario: los días con ingresos y gastos llevan una franja inferior del color contrario al neto (verde si hubo ingresos en un día negativo, roja si hubo gastos en un día positivo).
- Botón del ojo para ocultar todas las cantidades (se recuerda al reabrir).
- Datos: copia de seguridad JSON (incluye categorías), importar JSON o CSV, exportar CSV.

## Modelo de datos
- Movimiento: `{id, type: "ingreso"|"gasto", amount, cat, note, date: "YYYY-MM-DD", ts}`.
- Base IndexedDB `mis-gastos`: almacén `movs` (movimientos) y `meta` (`lastBackup`, `hideInstall`, `cats`, `hide`).
- `cats`: `{names: {id: nombre}, custom: [{id: "c_…", name, type, v}]}`.

## A tener en cuenta
- En iPhone, la pestaña de Safari y la app de la pantalla de inicio guardan datos por separado. Usar solo el icono de la pantalla de inicio.
- Borrar datos de Safari puede borrar los datos de la app: hacer copias de seguridad y guardarlas en Archivos/iCloud.
- No probada en un iPhone real, solo en navegador simulado.
