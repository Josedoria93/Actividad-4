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

### 3. Normalización

1. **Primera Forma Normal (1NF)**: Cada atributo debe contener un único valor y las entidades no deben contener grupos repetitivos.
2. **Segunda Forma Normal (2NF)**: Todos los atributos no clave deben depender completamente de la llave primaria.
3. **Tercera Forma Normal (3NF)**: No debe haber dependencias transitivas, es decir, los atributos no clave no deben depender de otros atributos no clave.

### 4. Llaves Foráneas (FK)

**Producto**
* CodigoProveedor → Proveedor(CodigoProveedor)

**Factura**
* CodigoCliente → Cliente(CodigoCliente)
* CodigoVendedor → Empleado(CodigoEmpleado)

**DetalleFactura**
* NumeroFactura → Factura(NumeroFactura)
* CodigoProducto → Producto(CodigoProducto)

**Compras_Proveedores**
* CodigoProveedor → Proveedor(CodigoProveedor)

**Detalles_Compras_Proveedores**
* NumeroCompra → Compras_Proveedores(NumeroCompra)
* CodigoProducto → Producto(CodigoProducto)

### 5. Cardinalidad entre Entidades

1. Proveedor - Producto
* Relación: Un proveedor puede suministrar muchos productos.
* **Cardinalidad**:
* Proveedor (1) a Producto (N)
* Un proveedor (1) puede suministrar muchos productos (N).
* Cada producto (N) es suministrado por un solo proveedor (1).

2. Producto - DetalleFactura
* Relación: Un producto puede aparecer en muchas facturas, y una factura puede incluir muchos productos.
* **Cardinalidad**:
* Producto (1) a DetalleFactura (N)
* Un producto (1) puede aparecer en muchos detalles de facturas (N).
* Un detalle de factura (N) se refiere a un solo producto (1).

3. Factura - DetalleFactura
* Relación: Una factura puede contener muchos detalles, y cada detalle puede incluir un producto.
* **Cardinalidad**:
* Factura (1) a DetalleFactura (N)
* Una factura (1) puede tener muchos detalles (N).
* Un detalle de factura (N) pertenece a una sola factura (1).

4. Cliente - Factura
* Relación: Un cliente puede generar muchas facturas.
* **Cardinalidad**:
* Cliente (1) a Factura (N)
* Un cliente (1) puede tener muchas facturas (N).
* Una factura (N) es emitida a un solo cliente (1).

5. Empleado - Factura
* Relación: Un empleado puede emitir muchas facturas.
* **Cardinalidad**:
* Empleado (1) a Factura (N)
* Un empleado (1) puede emitir muchas facturas (N).
* Una factura (N) es emitida por un solo empleado (1).

6. Proveedor - Compras_Proveedores
* Relación: Un proveedor puede estar asociado a muchas compras.
* **Cardinalidad**:
* Proveedor (1) a Compras_Proveedores (N)
* Un proveedor (1) puede tener muchas compras (N).
* Una compra (N) está asociada a un solo proveedor (1).

7. Compras_Proveedores - Detalles_Compras_Proveedores
* Relación: Una compra puede tener muchos detalles, y cada detalle puede incluir un producto.
* **Cardinalidad**:
* Compras_Proveedores (1) a Detalles_Compras_Proveedores (N)
* Una compra (1) puede tener muchos detalles (N).
* Un detalle de compra (N) pertenece a una sola compra (1).

8. Producto - Detalles_Compras_Proveedores
* Relación: Un producto puede estar en muchas compras, y cada compra puede incluir múltiples productos.
* **Cardinalidad**:
* Producto (1) a Detalles_Compras_Proveedores (N)
* Un producto (1) puede aparecer en muchos detalles de compras (N).
* Un detalle de compra (N) se refiere a un solo producto (1).

### 6. Diagrama Entidad-Relación (E-R)

```
+----------------+       +------------------+       +------------------+
|    Proveedor   |       |    Producto      |       |     Cliente      |
+----------------+       +------------------+       +------------------+
| CodigoProveedor| <-----| CodigoProveedor  |       | CodigoCliente    |
| NombreProveedor|       | CodigoProducto   |       | Nombre           |
| Telefono       |       | Nombre           |       | Apellido         |
| Direccion      |       | TipoMaterial     |       | Direccion        |
| Email          |       | Marca            |       | Telefono         |
+----------------+       | PrecioUnitario   |       | Email            |
                        | Stock            |       +------------------+
                        +------------------+                  
                             |                              
                             |                              
                             |                              
                             |                              
+----------------+       +------------------+       +------------------+
|     Factura    |       |   DetalleFactura |       |    Empleado      |
+----------------+       +------------------+       +------------------+
| NumeroFactura  |       | NumeroFactura    |       | CodigoEmpleado   |
| CodigoCliente  |<----- | CodigoProducto   |       | Nombre           |
| CodigoVendedor |       | Cantidad         |       | Apellido         |
| FechaFactura   |       | PrecioUnitario   |       | Grupo            |
| TipoPago       |       | Subtotal         |       | Salario          |
+----------------+       +------------------+       +------------------+

+--------------------------+       +-----------------------------+
|  Compras_Proveedores     |       | Detalles_Compras_Proveedores |
+--------------------------+       +-----------------------------+
| NumeroCompra             |       | NumeroCompra                |
| CodigoProveedor          |<----- | CodigoProducto             |
| FechaCompra              |       | Cantidad                    |
| TotalCompra              |       | PrecioUnitario              |
+--------------------------+       | Subtotal                    |
                                  +-----------------------------+

```
Este diseño de base de datos permitirá a Don Próspero Buenavida gestionar eficientemente el inventario, la cartera de clientes, proveedores, y empleados, así como obtener informes precisos sobre el rendimiento de la empresa.

### Importancia del Gestor de Bases de Datos Relacionales en una Empresa

Un **gestor de bases de datos relacional** (RDBMS) es crucial para cualquier organización que maneje grandes volúmenes de datos. Permite a las empresas gestionar y organizar sus datos de manera eficiente y segura. La importancia del RDBMS en una empresa radica en varios aspectos clave:

1. **Centralización y Organización de Datos**: Un RDBMS centraliza todos los datos en un solo sistema, lo que facilita su acceso, administración y actualización. Esto asegura que todos los usuarios tengan acceso a la información más reciente y precisa.

2. **Integridad y Consistencia de Datos**: Un RDBMS garantiza que los datos sean consistentes y estén libres de errores mediante el uso de restricciones de integridad y reglas de validación. Esto es fundamental para mantener la calidad de los datos y evitar problemas que podrían surgir de datos incorrectos o inconsistentes.

3. **Seguridad de Datos**: Los RDBMS proporcionan mecanismos avanzados de seguridad, como el control de acceso y la encriptación, para proteger los datos sensibles contra accesos no autorizados y amenazas externas.

4. **Eficiencia en la Recuperación de Información**: Los RDBMS permiten consultas rápidas y eficientes gracias a la optimización de consultas y al uso de índices, lo que mejora la toma de decisiones y la productividad.

5. **Escalabilidad y Flexibilidad**: Permiten a las organizaciones escalar sus bases de datos según sus necesidades, adaptándose a cambios en el volumen de datos y en los requerimientos de la empresa.

### Cinco Funciones del Gestor de Bases de Datos Relacionales

1. **Gestión de Datos**:
   - **Descripción**: Organiza y almacena los datos en tablas relacionadas mediante claves primarias y foráneas, facilitando la administración de grandes volúmenes de datos de manera estructurada.
   - **Importancia**: Permite una organización lógica y eficiente de los datos, lo que facilita el acceso y la manipulación de la información.

2. **Control de Acceso y Seguridad**:
   - **Descripción**: Proporciona mecanismos para definir permisos y accesos a los datos, asegurando que solo los usuarios autorizados puedan realizar ciertas acciones sobre los datos.
   - **Importancia**: Protege la confidencialidad e integridad de los datos, evitando accesos no autorizados y garantizando que los datos sean accesibles solo para quienes tienen permiso.

3. **Realización de Consultas**:
   - **Descripción**: Permite la ejecución de consultas complejas a través del lenguaje SQL (Structured Query Language) para recuperar, actualizar y gestionar los datos.
   - **Importancia**: Facilita la obtención de información específica y detallada, lo que es fundamental para la toma de decisiones empresariales y para la generación de informes.

4. **Respaldo y Recuperación de Datos**:
   - **Descripción**: Ofrece herramientas y procesos para realizar copias de seguridad periódicas y para recuperar datos en caso de fallos o pérdidas.
   - **Importancia**: Asegura la protección de los datos contra pérdidas accidentalmente o debido a fallos en el sistema, garantizando la continuidad del negocio.

5. **Optimización del Rendimiento**:
   - **Descripción**: Implementa técnicas para mejorar el rendimiento de las consultas y operaciones de la base de datos, como el uso de índices y la optimización de consultas.
   - **Importancia**: Mejora la eficiencia de las operaciones de la base de datos, reduciendo el tiempo de respuesta y aumentando la productividad de los usuarios y aplicaciones que interactúan con la base de datos.

### Conclusión

Un gestor de bases de datos relacional es una herramienta indispensable para las organizaciones modernas, proporcionando una estructura sólida para la gestión de datos, garantizando la seguridad, y mejorando la eficiencia operativa. Su capacidad para manejar grandes volúmenes de datos y proporcionar acceso rápido y seguro es esencial para la toma de decisiones informadas y la operación eficaz de cualquier empresa.
