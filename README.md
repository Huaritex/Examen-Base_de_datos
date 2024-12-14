# Examen-Base_de_datos

> [!IMPORTANT]
> # Base de Datos para Tienda de Música


Este repositorio contiene el script SQL para la creación de una base de datos diseñada para gestionar una tienda de música. La base de datos permite el registro de productos, categorías, empleados, clientes y pedidos, incluyendo los detalles de cada pedido.

> [!NOTE]
> ## Esquema de la Base de Datos

El esquema consta de las siguientes tablas:

*   **Categoria:** Almacena las categorías de los productos (ej., Instrumentos de Cuerda, Percusión, Viento).
*   **Productos:** Contiene la información de cada producto disponible en la tienda.
*   **Empleado:** Registra la información de los empleados de la tienda.
*   **Cliente:** Almacena la información de los clientes.
*   **Pedidos:** Contiene la información general de cada pedido realizado.
*   **Detalles_Pedido:** Almacena los detalles de cada pedido, incluyendo qué productos se compraron y en qué cantidad.

A continuación, se detalla la estructura de cada tabla:

### 1. Categoria

| Columna        | Tipo de Dato | Restricciones                               | Descripción                               |
| -------------- | ------------- | ------------------------------------------ | ----------------------------------------- |
| CategoriaID    | INT           | PRIMARY KEY, IDENTITY(1,1), NOT NULL        | Identificador único de la categoría.      |
| NombreCategoria | VARCHAR(50)   | NOT NULL                                    | Nombre de la categoría.                   |

### 2. Productos

| Columna     | Tipo de Dato | Restricciones                               | Descripción                                                              |
| ----------- | ------------- | ------------------------------------------ | ------------------------------------------------------------------------ |
| ProductoID  | INT           | PRIMARY KEY, IDENTITY(1,1), NOT NULL        | Identificador único del producto.                                       |
| nombre      | VARCHAR(50)   | NOT NULL                                    | Nombre del producto.                                                     |
| descripcion | VARCHAR(50)   | NOT NULL                                    | Descripción del producto.                                                |
| marca       | VARCHAR(50)   | NOT NULL                                    | Marca del producto.                                                      |
| modelo      | VARCHAR(50)   | NOT NULL                                    | Modelo del producto.                                                     |
| PrecioVenta | INT           | NOT NULL                                    | Precio de venta del producto.                                            |
| Stock       | INT           | NOT NULL                                    | Cantidad en stock del producto.                                          |
| CategoriaID | INT           | FOREIGN KEY REFERENCES Categoria(CategoriaID) | Clave foránea que referencia a la tabla Categoria. Indica a qué categoría pertenece el producto. |

### 3. Empleado

| Columna    | Tipo de Dato | Restricciones                               | Descripción                               |
| ---------- | ------------- | ------------------------------------------ | ----------------------------------------- |
| EmpleadoID | INT           | PRIMARY KEY, IDENTITY(1,1), NOT NULL        | Identificador único del empleado.         |
| Nombre     | VARCHAR(50)   | NOT NULL                                    | Nombre del empleado.                      |
| Apellido   | VARCHAR(50)   | NOT NULL                                    | Apellido del empleado.                    |
| Cargo      | VARCHAR(50)   | NOT NULL                                    | Cargo del empleado.                       |

### 4. Cliente

| Columna   | Tipo de Dato | Restricciones                               | Descripción                               |
| --------- | ------------- | ------------------------------------------ | ----------------------------------------- |
| ClienteID | INT           | PRIMARY KEY, IDENTITY(1,1), NOT NULL        | Identificador único del cliente.          |
| Nombre    | VARCHAR(50)   | NOT NULL                                    | Nombre del cliente.                       |
| Apellido  | VARCHAR(50)   | NOT NULL                                    | Apellido del cliente.                     |
| Email     | VARCHAR(50)   | NOT NULL                                    | Correo electrónico del cliente.           |
| Telefono  | INT           | NOT NULL                                    | Número de teléfono del cliente.           |
| Direccion | TEXT          |                                            | Dirección del cliente.                    |

### 5. Pedidos

| Columna       | Tipo de Dato | Restricciones                               | Descripción                                                              |
| ------------- | ------------- | ------------------------------------------ | ------------------------------------------------------------------------ |
| PedidoID      | INT           | PRIMARY KEY, IDENTITY(1,1), NOT NULL        | Identificador único del pedido.                                          |
| ClienteID     | INT           | FOREIGN KEY REFERENCES Cliente(ClienteID)   | Clave foránea que referencia a la tabla Cliente. Indica quién realizó el pedido. |
| EmpleadoID    | INT           | FOREIGN KEY REFERENCES Empleado(EmpleadoID)  | Clave foránea que referencia a la tabla Empleado. Indica quién atendió el pedido. |
| FechaPedido   | DATETIME      |                                            | Fecha y hora en que se realizó el pedido.                               |
| Forma\_de\_Pago | VARCHAR(50)   | NOT NULL                                    | Forma de pago utilizada (ej., Efectivo, Tarjeta).                         |
| EstadoPedido  | VARCHAR(50)   | NOT NULL                                    | Estado actual del pedido (ej., Pendiente, Completado, Cancelado).        |

### 6. Detalles\_Pedido

| Columna        | Tipo de Dato | Restricciones                               | Descripción                                                              |
| -------------- | ------------- | ------------------------------------------ | ------------------------------------------------------------------------ |
| DetallePedidoID | INT           | PRIMARY KEY, IDENTITY(1,1), NOT NULL        | Identificador único del detalle del pedido.                               |
| PedidoID       | INT           | FOREIGN KEY REFERENCES Pedidos(PedidoID)    | Clave foránea que referencia a la tabla Pedidos. Indica a qué pedido pertenece el detalle. |
| ProductoID     | INT           | FOREIGN KEY REFERENCES Productos(ProductoID) | Clave foránea que referencia a la tabla Productos. Indica qué producto se incluyó en el pedido. |
| Cantidad       | INT           | NOT NULL                                    | Cantidad del producto en el pedido.                                      |
| PrecioUnitario | INT           | NOT NULL                                    | Precio unitario del producto al momento del pedido.                       |
| EmpleadoID    | INT           | FOREIGN KEY REFERENCES Empleado(EmpleadoID)  | Clave foránea que referencia a la tabla Empleado. Indica quién registró el detalle del pedido. |

> [!TIP]
> ## Relaciones entre las Tablas

Las siguientes relaciones existen entre las tablas:

*   **Productos - Categoria:** Relación de uno a muchos. Una categoría puede tener muchos productos.
*   **Pedidos - Cliente:** Relación de uno a muchos. Un cliente puede realizar muchos pedidos.
*   **Pedidos - Empleado:** Relación de uno a muchos. Un empleado puede atender muchos pedidos.
*   **Detalles\_Pedido - Pedidos:** Relación de uno a muchos. Un pedido puede tener muchos detalles.
*   **Detalles\_Pedido - Productos:** Relación de uno a muchos. Un producto puede aparecer en muchos detalles de pedido.
*   **Detalles_Pedido - Empleado:** Relación de uno a muchos. Un empleado puede registrar muchos detalles de pedido.


