# Cursogramas de SANDUINO Energy ERP

Un cursograma describe un circuito administrativo paso a paso, indicando quién hace cada tarea y de qué tipo es.

| Símbolo | Significado |
|---|---|
| ○ | Operación (se hace o se registra algo) |
| ➡ | Transporte (algo pasa de un sector a otro) |
| □ | Control / inspección |
| ▽ | Almacenamiento / archivo |
| D | Demora / espera |

## 1. Circuito de la venta

| N.º | Paso | Sector | Símbolo |
|---|---|---|---|
| 1 | El cliente pide uno o más productos | Cliente | ○ Operación |
| 2 | El vendedor ingresa código y cantidad | Vendedor | ○ Operación |
| 3 | El sistema valida código, cantidad y stock | Sistema | □ Control |
| 4 | Se agrega la línea al carrito y se recalcula el total | Sistema | ○ Operación |
| 5 | Se elige el medio de pago con el cliente | Vendedor | ○ Operación |
| 6 | El sistema verifica que el carrito no esté vacío | Sistema | □ Control |
| 7 | Se registra la venta y su detalle | Sistema | ▽ Almacenamiento |
| 8 | Se descuenta el stock de cada producto | Sistema | ○ Operación |
| 9 | Se genera el ticket PDF numerado | Sistema | ○ Operación |
| 10 | Se anota la operación en la bitácora | Sistema | ▽ Almacenamiento |
| 11 | Se entrega el ticket y los productos | Vendedor → Cliente | ➡ Transporte |

## 2. Circuito del fiado

| N.º | Paso | Sector | Símbolo |
|---|---|---|---|
| 1 | El cliente retira mercadería a cuenta | Cliente | ○ Operación |
| 2 | Se cargan cliente, monto y concepto | Vendedor | ○ Operación |
| 3 | Se guarda la deuda como PENDIENTE y se anota en la bitácora | Sistema | ▽ Almacenamiento |
| 4 | Espera hasta que el cliente vuelve a pagar | Cliente | D Demora |
| 5 | Se revisa la lista de pendientes | Vendedor | □ Control |
| 6 | Se cobra y se presiona Saldar Deuda con el ID | Vendedor | ○ Operación |
| 7 | La deuda pasa a PAGADO y se anota en la bitácora | Sistema | ▽ Almacenamiento |
| 8 | Se registra el cobro como INGRESO en la caja | Vendedor | ○ Operación |

## 3. Circuito de reposición de stock

| N.º | Paso | Sector | Símbolo |
|---|---|---|---|
| 1 | Cada venta actualiza el stock | Sistema | ○ Operación |
| 2 | El sistema compara el stock con el mínimo y marca BAJO | Sistema | □ Control |
| 3 | El encabezado muestra cuántos productos están en nivel crítico | Sistema | ○ Operación |
| 4 | El Admin exporta el inventario a Excel | Admin | ○ Operación |
| 5 | Se consulta en Proveedores a quién pedir según el rubro | Admin | □ Control |
| 6 | Se envía el pedido al proveedor | Admin → Proveedor | ➡ Transporte |
| 7 | Espera hasta recibir la mercadería | Proveedor | D Demora |
| 8 | Se da de alta el producto o se actualiza su stock | Admin | ○ Operación |
| 9 | La mercadería se guarda en el depósito | Depósito | ▽ Almacenamiento |

## 4. Circuito del cierre diario

| N.º | Paso | Sector | Símbolo |
|---|---|---|---|
| 1 | Al abrir, se registra la APERTURA con el efectivo inicial | Vendedor | ○ Operación |
| 2 | Durante el día se registran ingresos y egresos | Vendedor | ○ Operación |
| 3 | Al terminar, se registran los movimientos pendientes | Admin | ○ Operación |
| 4 | Se presiona Realizar Cierre y Arqueo Diario | Admin | ○ Operación |
| 5 | El sistema suma ventas y movimientos y calcula el saldo | Sistema | ○ Operación |
| 6 | Se compara el efectivo físico con el efectivo esperado | Admin | □ Control |
| 7 | El cierre se anota en la bitácora | Sistema | ▽ Almacenamiento |
| 8 | Se guarda el dinero | Admin | ▽ Almacenamiento |

## 5. Circuito de inicio de sesión y respaldo

| N.º | Paso | Sector | Símbolo |
|---|---|---|---|
| 1 | El usuario ingresa usuario y contraseña | Usuario | ○ Operación |
| 2 | El sistema verifica el hash y que la cuenta esté ACTIVA | Sistema | □ Control |
| 3 | Se crea el backup automático en `backups/` | Sistema | ▽ Almacenamiento |
| 4 | Se registra el inicio de sesión en la bitácora | Sistema | ▽ Almacenamiento |
| 5 | Se abre la ventana principal | Sistema | ○ Operación |

## Resumen de la venta

| Símbolo | Cantidad |
|---|---|
| ○ Operación | 6 |
| □ Control | 2 |
| ▽ Almacenamiento | 2 |
| ➡ Transporte | 1 |
| D Demora | 0 |
| **Total de pasos** | **11** |
