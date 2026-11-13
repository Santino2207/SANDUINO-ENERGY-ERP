# Diagrama de flujo de SANDUINO Energy ERP

Los diagramas están escritos en [Mermaid](https://mermaid.js.org/), que GitHub dibuja directamente en esta página.

## 1. Flujo general del sistema

```mermaid
flowchart TD
    A([Inicio: ejecutar la aplicación]) --> B[init_db: crea tablas, usuario admin<br/>y clave de sistema si no existen]
    B --> C{¿Sistema<br/>bloqueado?}
    C -- Sí --> D[/Aviso: SISTEMA BLOQUEADO/]
    D --> Z([Fin])
    C -- No --> E[Ventana de acceso]
    E --> F{¿Credenciales<br/>válidas y usuario ACTIVO?}
    F -- No --> G[/Mensaje de error/]
    G --> E
    F -- Sí --> H[Backup automático + registro en bitácora]
    H --> I[Ventana principal con pestañas]
    I --> J{Módulo elegido}
    J --> K[Punto de Venta]
    J --> L[Inventario]
    J --> M[Deudores / Fiados]
    J --> N[Arqueo de Caja]
    J --> O[Proveedores]
    J --> P[Reportes]
    J --> Q{¿Rol Admin?}
    Q -- Sí --> R[Usuarios, Auditoría y Backups]
    Q -- No --> I
    K & L & M & N & O & P & R --> S[(Base de datos SQLite)]
    S --> I
    I --> T([Cerrar sesión / salir])
```

## 2. Inicio de sesión

```mermaid
flowchart TD
    A([Usuario presiona Iniciar Sesión]) --> B{¿Usuario y<br/>contraseña completos?}
    B -- No --> B1[/Ingrese sus credenciales/] --> A
    B -- Sí --> C[Calcular hash SHA-256 de la contraseña]
    C --> D{¿Existe el usuario?}
    D -- No --> D1[/Usuario o contraseña inválidos/] --> A
    D -- Sí --> E{¿Hash guardado<br/>coincide?}
    E -- Sí --> G
    E -- No --> F{¿Coincide con clave<br/>en texto plano?}
    F -- No --> D1
    F -- Sí --> F1[Reemplazar la clave por su hash] --> G
    G{¿Estado BLOQUEADO?}
    G -- Sí --> G1[/El usuario se encuentra BLOQUEADO/] --> A
    G -- No --> H[Crear backup automático]
    H --> I[Registrar inicio de sesión en la bitácora]
    I --> J([Abrir ventana principal con usuario y rol])
```

## 3. Venta en el Punto de Venta

```mermaid
flowchart TD
    A([Ingresar código y cantidad]) --> B{¿Código no vacío y<br/>cantidad entera positiva?}
    B -- No --> B1[/Ingrese código y cantidad válida/] --> A
    B -- Sí --> C{¿Existe el producto?}
    C -- No --> C1[/Producto no encontrado/] --> A
    C -- Sí --> D{¿Cantidad ≤ stock?}
    D -- No --> D1[/Stock insuficiente/] --> A
    D -- Sí --> E[Agregar línea al carrito<br/>y recalcular total]
    E --> F{¿Agregar<br/>otro producto?}
    F -- Sí --> A
    F -- No --> G[Elegir medio de pago:<br/>Efectivo, Tarjeta o Transferencia / MP]
    G --> H[Presionar COBRAR Y GENERAR TICKET]
    H --> I{¿Carrito vacío?}
    I -- Sí --> I1[/El carrito está vacío/] --> A
    I -- No --> J[Insertar venta: fecha, usuario,<br/>total y medio de pago]
    J --> K[Por cada línea: insertar detalle<br/>y descontar stock]
    K --> L[Confirmar cambios en la base]
    L --> M[Generar ticket PDF numerado]
    M --> N[Registrar en bitácora]
    N --> O[Vaciar carrito y actualizar<br/>inventario y alerta de stock crítico]
    O --> P([Fin de la venta])
```

## 4. Inventario y alerta de stock

```mermaid
flowchart TD
    A([Abrir pestaña Inventario]) --> B[Leer productos de la base]
    B --> C[Mostrar tabla: código, nombre,<br/>categoría, precio, stock]
    C --> D{¿Stock ≤ stock mínimo?}
    D -- Sí --> E[Estado BAJO: resaltar fila<br/>y sumar al aviso del encabezado]
    D -- No --> F[Estado OK]
    E --> G{Acción}
    F --> G
    G -- Recargar --> B
    G -- Exportar a Excel --> H[Generar archivo .xlsx]
    G -- Eliminar producto --> I{¿Rol Admin?}
    I -- No --> I1[/Acción no permitida/]
    I -- Sí --> J[Borrar producto y registrar en bitácora] --> B
```

## 5. Cierre de caja

```mermaid
flowchart TD
    A([Presionar REALIZAR CIERRE Y ARQUEO DIARIO]) --> B[Determinar la fecha de hoy]
    B --> C[Sumar ventas del día]
    C --> D[Sumar movimientos de hoy por tipo:<br/>APERTURA, INGRESO y EGRESO]
    D --> E["Saldo = ventas + ingresos + apertura − egresos"]
    E --> F[/Mostrar resultado del día/]
    F --> G[Registrar el cierre en la bitácora]
    G --> H([Fin])
```

## 6. Bloqueo global de emergencia

```mermaid
flowchart TD
    A([Admin presiona BLOQUEO GLOBAL]) --> B{¿Confirma la alerta?}
    B -- No --> Z([Cancelar])
    B -- Sí --> C[Marcar sistema_bloqueado = SI]
    C --> D[Registrar en bitácora]
    D --> E[/Aviso de bloqueo/]
    E --> F[Cerrar la ventana principal]
    F --> G([En cada arranque: SISTEMA BLOQUEADO<br/>hasta reactivarlo desde la base de datos])
```
