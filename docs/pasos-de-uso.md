# Pasos de uso: manual paso a paso

Instructivos con el lenguaje de la propia pantalla, divididos por rol.

## Para el Vendedor

### Iniciar el turno
1. Abrir SANDUINO Energy desde el acceso directo.
2. Escribir el usuario y la contraseña (el botón del ojo permite ver lo escrito).
3. Presionar **Iniciar Sesión**.
4. Mirar el aviso naranja del encabezado: indica cuántos productos están por agotarse.

### Vender
1. Ir a la pestaña **Punto de Venta**.
2. Escribir el código del producto y la cantidad, y presionar **Añadir al Carrito**.
3. Repetir por cada producto; el total se actualiza solo.
4. Elegir el medio de pago con el cliente.
5. Presionar **Cobrar y Generar Ticket**.
6. Imprimir o entregar el ticket PDF si el cliente lo pide.

### Anotar un fiado
1. Ir a **Deudores / Fiados**.
2. Escribir cliente, monto y concepto.
3. Presionar **Registrar Fiado**.

### Registrar un gasto o un ingreso
1. Ir a **Arqueo de Caja**.
2. Elegir el tipo (INGRESO o EGRESO), escribir el monto y un concepto claro.
3. Presionar **Registrar**.

## Para el Admin

### Agregar o eliminar productos
1. En **Inventario y Stock**, completar el formulario y presionar **Guardar** para sumar un producto.
2. Para eliminar, seleccionar la fila, presionar **Eliminar Producto** y confirmar.

### Administrar usuarios
1. En **Usuarios y Auditoría**, completar usuario, contraseña y rol, y presionar **Crear Usuario**.
2. Para bloquear a alguien, presionar **Bloquear / Desbloquear** e ingresar su ID; el mismo botón lo vuelve a activar.
3. Para borrar una cuenta, presionar **Borrar Usuario** e ingresar su ID.

### Cerrar el día
1. Registrar los ingresos y egresos pendientes.
2. Presionar **Realizar Cierre y Arqueo Diario** y revisar el resumen.
3. Comparar el efectivo físico con el efectivo esperado (ventas en efectivo + apertura + ingresos − egresos).

### Revisar la actividad
En la parte inferior de **Usuarios y Auditoría** se ven las últimas 15 acciones del sistema, con fecha, usuario y descripción.

## Puesta en marcha inicial (Admin / soporte)

1. Ingresar como `admin` con las credenciales iniciales (ver capítulo 22 del manual).
2. Crear un usuario Admin propio para el dueño, con una clave larga y personal.
3. Crear un usuario Vendedor por cada persona que atenderá el mostrador.
4. Cargar el catálogo con código, precio, stock y stock mínimo.
5. Cargar los proveedores principales con rubro y teléfono.
6. Cargar los fiados vigentes.
7. Registrar la apertura de caja con el efectivo inicial.
8. Hacer una venta de prueba y verificar el ticket, el descuento de stock y el cierre.
9. Generar un backup manual y confirmar que se guarda en la carpeta elegida.

## Mensajes del sistema y qué hacer

| Mensaje | Significado | Qué hacer |
|---|---|---|
| Ingrese sus credenciales. | Falta el usuario o la contraseña | Completar ambos campos |
| Usuario o contraseña inválidos. | Datos incorrectos | Revisar mayúsculas y reintentar; si persiste, pedir ayuda al Admin |
| El usuario se encuentra BLOQUEADO. | La cuenta fue bloqueada por el Admin | Pedir al Admin que la desbloquee |
| Ingrese código y cantidad válida. | Falta el código o la cantidad no es un entero | Corregir los datos |
| Producto no encontrado. | El código no existe | Verificar el código o dar de alta el producto |
| Stock Insuficiente | Se pidió más de lo que hay | Reducir la cantidad o revisar el stock |
| El carrito está vacío. | No hay productos para cobrar | Añadir al menos un producto |
| El código ya existe. | Hay otro producto con ese código | Usar otro código |
| Campos incompletos. | Falta un dato obligatorio del producto | Completar código, nombre, precio y stock |

## Reglas prácticas que evitan errores

- Escribir los decimales con **punto** (por ejemplo, `1250.50`) y no con coma.
- No compartir el usuario con otras personas.
- Verificar el medio de pago antes de cobrar: no se puede modificar después.
- Ejecutar siempre la aplicación desde la misma carpeta.
- Cerrar sesión y apagar la computadora de forma ordenada al terminar el día.
