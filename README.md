# Actividad-4
## Estudio de Caso: Diseñar una base de datos relacional para una empresa.

* Para el diseño de la base de datos tenga en cuenta los siguientes pasos:
1. Identifique las entidades con los atributos y tipos de datos correspondientes.
2. Defina para cada entidad una llave primaria (PK).
3. Aplique los principios de normalización en la base de datos relacional.
4. Defina para cada entidad una llave foránea (FK).
5. Defina la cardinalidad que existe entre entidades.
6. Genere el diagrama Entidad-Relación (E-R).
7. Responda la pregunta formulada en el inicio de esta guía de aprendizaje, en la evidencia identificar las funciones del gestor de base de datos.
8. Maneje un lenguaje técnico a través de todo el desarrollo de la evidencia.

### 1. Identificación de Entidades, Atributos y Tipos de Datos

**Entidades y sus Atributos:**

1. **Producto**
   - **CódigoProducto** (PK, VARCHAR): Identificador único del producto.
   - **Nombre** (VARCHAR): Nombre del producto.
   - **TipoMaterial** (VARCHAR): Tipo de material (Construcción, Eléctrico).
   - **CódigoProveedor** (FK, VARCHAR): Identificador del proveedor.
   - **Marca** (VARCHAR): Marca del producto.
   - **PrecioUnitario** (DECIMAL): Precio unitario del producto.
   - **Stock** (INT): Cantidad en inventario.

2. **Cliente**
   - **CódigoCliente** (PK, VARCHAR): Identificador único del cliente.
   - **Nombre** (VARCHAR): Nombre del cliente.
   - **Apellido** (VARCHAR): Apellido del cliente.
   - **Dirección** (VARCHAR): Dirección del cliente.
   - **Teléfono** (VARCHAR): Teléfono del cliente.
   - **Email** (VARCHAR): Correo electrónico del cliente.

3. **Factura**
   - **NúmeroFactura** (PK, INT): Identificador único de la factura.
   - **CódigoCliente** (FK, VARCHAR): Identificador del cliente.
   - **CódigoVendedor** (FK, VARCHAR): Identificador del vendedor.
   - **FechaFactura** (DATE): Fecha de emisión de la factura.
   - **TipoPago** (VARCHAR): Tipo de pago (Crédito, Contado).

4. **DetalleFactura**
   - **NúmeroFactura** (FK, INT): Identificador de la factura.
   - **CódigoProducto** (FK, VARCHAR): Identificador del producto.
   - **Cantidad** (INT): Cantidad de productos en la factura.
   - **PrecioUnitario** (DECIMAL): Precio unitario del producto al momento de la factura.
   - **Subtotal** (DECIMAL): Subtotal por producto (Cantidad * PrecioUnitario).

5. **Proveedor**
   - **CódigoProveedor** (PK, VARCHAR): Identificador único del proveedor.
   - **NombreProveedor** (VARCHAR): Nombre del proveedor.
   - **Teléfono** (VARCHAR): Teléfono del proveedor.
   - **Dirección** (VARCHAR): Dirección del proveedor.
   - **Email** (VARCHAR): Correo electrónico del proveedor.

6. **Empleado**
   - **CódigoEmpleado** (PK, VARCHAR): Identificador único del empleado.
   - **Nombre** (VARCHAR): Nombre del empleado.
   - **Apellido** (VARCHAR): Apellido del empleado.
   - **Grupo** (VARCHAR): Grupo al que pertenece (Vendedor, Administrativo).
   - **Salario** (DECIMAL): Salario del empleado.
     
7. **Compras_Proveedores**
 - **NumeroCompra (PK, INT): Identificador único de la compra.
 - **CodigoProveedor (FK, VARCHAR): Identificador del proveedor que realizó la venta.
 - **FechaCompra (DATE): Fecha en que se realizó la compra.
 - **TotalCompra (DECIMAL(10, 2)): Total de la compra.

8. **Detalles_Compras_Proveedores**
 - **NumeroCompra (FK, INT): Identificador de la compra.
 - **CodigoProducto (FK, VARCHAR): Identificador del producto comprado.
 - **Cantidad (INT): Cantidad de productos comprados.
 - **PrecioUnitario (DECIMAL(10, 2)): Precio unitario del producto en la compra.
 - **Subtotal (DECIMAL(10, 2)): Subtotal por producto (Cantidad * PrecioUnitario).

### 2. Llaves Primarias (PK)

* Cada entidad tiene una llave primaria que es un identificador único:
- **Producto**: CódigoProducto
- **Cliente**: CódigoCliente
- **Factura**: NúmeroFactura
- **DetalleFactura**: (NúmeroFactura, CódigoProducto) - Compuesto
- **Proveedor**: CódigoProveedor
- **Empleado**: CódigoEmpleado
- **Compras_Proveedores**: NumeroCompra
- **Detalles_Compras_Proveedores**: NumeroCompra
- 
### 3. Normalización

1. **Primera Forma Normal (1NF)**: Cada atributo debe contener un único valor y las entidades no deben contener grupos repetitivos.
2. **Segunda Forma Normal (2NF)**: Todos los atributos no clave deben depender completamente de la llave primaria.
3. **Tercera Forma Normal (3NF)**: No debe haber dependencias transitivas, es decir, los atributos no clave no deben depender de otros atributos no clave.

### 4. Llaves Foráneas (FK)

**Producto**
CodigoProveedor → Proveedor(CodigoProveedor)

**Factura**
CodigoCliente → Cliente(CodigoCliente)
CodigoVendedor → Empleado(CodigoEmpleado)

**DetalleFactura**
NumeroFactura → Factura(NumeroFactura)
CodigoProducto → Producto(CodigoProducto)

**Compras_Proveedores**
CodigoProveedor → Proveedor(CodigoProveedor)

**Detalles_Compras_Proveedores**
NumeroCompra → Compras_Proveedores(NumeroCompra)
CodigoProducto → Producto(CodigoProducto)

### 5. Cardinalidad entre Entidades

1. Proveedor - Producto
* Relación: Un proveedor puede suministrar muchos productos.
**Cardinalidad**:
* Proveedor (1) a Producto (N)
* Un proveedor (1) puede suministrar muchos productos (N).
* Cada producto (N) es suministrado por un solo proveedor (1).

2. Producto - DetalleFactura
* Relación: Un producto puede aparecer en muchas facturas, y una factura puede incluir muchos productos.
**Cardinalidad**:
* Producto (1) a DetalleFactura (N)
* Un producto (1) puede aparecer en muchos detalles de facturas (N).
* Un detalle de factura (N) se refiere a un solo producto (1).

3. Factura - DetalleFactura
* Relación: Una factura puede contener muchos detalles, y cada detalle puede incluir un producto.
**Cardinalidad**:
* Factura (1) a DetalleFactura (N)
* Una factura (1) puede tener muchos detalles (N).
* Un detalle de factura (N) pertenece a una sola factura (1).

4. Cliente - Factura
* Relación: Un cliente puede generar muchas facturas.
**Cardinalidad**:
* Cliente (1) a Factura (N)
* Un cliente (1) puede tener muchas facturas (N).
* Una factura (N) es emitida a un solo cliente (1).

5. Empleado - Factura
* Relación: Un empleado puede emitir muchas facturas.
**Cardinalidad**:
* Empleado (1) a Factura (N)
* Un empleado (1) puede emitir muchas facturas (N).
* Una factura (N) es emitida por un solo empleado (1).

6. Proveedor - Compras_Proveedores
* Relación: Un proveedor puede estar asociado a muchas compras.
**Cardinalidad**:
* Proveedor (1) a Compras_Proveedores (N)
* Un proveedor (1) puede tener muchas compras (N).
* Una compra (N) está asociada a un solo proveedor (1).

7. Compras_Proveedores - Detalles_Compras_Proveedores
* Relación: Una compra puede tener muchos detalles, y cada detalle puede incluir un producto.
**Cardinalidad**:
* Compras_Proveedores (1) a Detalles_Compras_Proveedores (N)
* Una compra (1) puede tener muchos detalles (N).
* Un detalle de compra (N) pertenece a una sola compra (1).

8. Producto - Detalles_Compras_Proveedores
* Relación: Un producto puede estar en muchas compras, y cada compra puede incluir múltiples productos.
**Cardinalidad**:
* Producto (1) a Detalles_Compras_Proveedores (N)
* Un producto (1) puede aparecer en muchos detalles de compras (N).
* Un detalle de compra (N) se refiere a un solo producto (1).

### 6. Diagrama Entidad-Relación (E-R)

Aquí tienes una representación textual del diagrama E-R:

```
[Producto] ----< (CódigoProveedor) >---- [Proveedor]
    |
    | (CódigoProducto)
    v
[DetalleFactura] ----< (NúmeroFactura) >---- [Factura] ----< (CódigoCliente) >---- [Cliente]
                     |
                     | (CódigoVendedor)
                     v
                 [Empleado]
```



Este diseño de base de datos permitirá a Don Próspero Buenavida gestionar eficientemente el inventario, la cartera de clientes, proveedores, y empleados, así como obtener informes precisos sobre el rendimiento de la empresa.

