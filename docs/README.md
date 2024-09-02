# BASE DE DATOS TIENDA

## Descripción del Proyecto

Este proyecto consiste en la creación de una base de datos relacional para una tienda ficticia utilizando MySQL. La base de datos está diseñada para gestionar productos, clientes, pedidos y los detalles de los pedidos. Incluye la estructura de las tablas necesarias y datos de ejemplo para probar y demostrar su funcionalidad. Este proyecto es ideal para quienes deseen aprender a manejar conceptos básicos y avanzados de SQL, incluyendo DML (Data Manipulation Language), DDL (Data Definition Language), relaciones entre tablas, y consultas avanzadas.

## Estructura de la Base de Datos

La base de datos `Tienda` contiene las siguientes tablas:

1. Productos: Almacena información sobre los productos disponibles en la tienda.
   - `id_producto`: Identificador único para cada producto (clave primaria).
   - `nombre`: Nombre del producto.
   - `descripcion`: Descripción detallada del producto.
   - `precio`: Precio del producto.
   - `stock`: Cantidad disponible en inventario.

2. Clientes: Guarda la información de los clientes de la tienda.
   - `id_cliente`: Identificador único para cada cliente (clave primaria).
   - `nombre`: Nombre completo del cliente.
   - `email`: Dirección de correo electrónico del cliente (debe ser única).
   - `telefono`: Número de teléfono del cliente.

3. Pedidos: Registra los pedidos realizados por los clientes.
   - `id_pedido`: Identificador único para cada pedido (clave primaria).
   - `id_cliente`: Referencia al cliente que realizó el pedido (clave foránea).
   - `fecha`: Fecha en la que se realizó el pedido.
   - `total`: Total de la compra realizada.

4. DetallePedidos: Contiene los detalles de cada pedido.
   - `id_detalle`: Identificador único para cada detalle de pedido (clave primaria).
   - `id_pedido`: Referencia al pedido al que pertenece el detalle (clave foránea).
   - `id_producto`: Referencia al producto incluido en el detalle (clave foránea).
   - `cantidad`: Cantidad del producto pedido.
   - `precio_unitario`: Precio unitario del producto en el momento del pedido.

## Restaurar la Base de Datos

Para restaurar la base de datos `Tienda` en tu entorno local utilizando MySQL Workbench o cualquier otro cliente MySQL, sigue los pasos a continuación:

1. Crear la Base de Datos: Primero, asegúrate de que MySQL esté en ejecución en tu sistema. Luego, crea la base de datos ejecutando el siguiente comando:

    ```sql
    CREATE DATABASE IF NOT EXISTS Tienda;
    ```

2. Seleccionar la Base de Datos: Selecciona la base de datos `Tienda` para usarla:

    ```sql
    USE Tienda;
    ```

3. Ejecutar el Script SQL: Ejecuta el script SQL proporcionado que contiene la creación de tablas y la inserción de datos. Puedes copiar y pegar el siguiente código en MySQL Workbench o en la línea de comandos de MySQL:

    ```sql
    -- Código para crear tablas y datos (Pega aquí el script SQL completo proporcionado anteriormente)
    ```

4. Verificar la Instalación: Asegúrate de que las tablas se han creado correctamente y que los datos de ejemplo han sido insertados ejecutando consultas simples, como:

    ```sql
    SELECT * FROM Productos;
    SELECT * FROM Clientes;
    SELECT * FROM Pedidos;
    SELECT * FROM DetallePedidos;
    ```

## Instrucciones Relevantes

- Consultar Productos: Para ver todos los productos disponibles en la tienda, puedes ejecutar la siguiente consulta:

    ```sql
    SELECT * FROM Productos;
    ```

- Agregar Nuevos Clientes: Puedes añadir nuevos clientes utilizando la siguiente instrucción de inserción:

    ```sql
    INSERT INTO Clientes (nombre, email, telefono) VALUES ('Carlos López', 'carlos.lopez@example.com', '1122334455');
    ```

- Generar Informe de Ventas: Para obtener un informe de los productos más vendidos por cada cliente, puedes ejecutar la consulta avanzada:

    ```sql
    SELECT c.nombre AS nombre_cliente, 
           p.nombre AS producto_mas_comprado, 
           MAX(dp.cantidad) AS cantidad_total
    FROM Clientes c
    JOIN Pedidos pe ON c.id_cliente = pe.id_cliente
    JOIN DetallePedidos dp ON pe.id_pedido = dp.id_pedido
    JOIN Productos p ON dp.id_producto = p.id_producto
    GROUP BY c.id_cliente, p.id_producto
    HAVING MAX(dp.cantidad) = (
        SELECT MAX(dp2.cantidad)
        FROM Pedidos pe2
        JOIN DetallePedidos dp2 ON pe2.id_pedido = dp2.id_pedido
        WHERE pe2.id_cliente = c.id_cliente
    )
    ORDER BY c.nombre;
    ```

- Seguridad de Datos: Asegúrate de manejar adecuadamente la seguridad y el acceso a la base de datos en un entorno de producción. Implementa autenticación y permisos adecuados para proteger la información confidencial de los clientes y las transacciones.

## Conclusión

Este proyecto de base de datos de tienda proporciona una estructura sólida para gestionar información de productos, clientes y pedidos. Es un punto de partida excelente para desarrollar aplicaciones de comercio electrónico o para aprender y practicar conceptos avanzados de SQL en un entorno de base de datos relacional.


