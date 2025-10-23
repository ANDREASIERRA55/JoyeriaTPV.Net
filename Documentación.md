# Documentación del Proyecto JOYERIA

## Introducción
- Este proyecto es una base de datos para una joyería, desarrollada en SQL Server como parte de un proyecto final.
- Se integra con una aplicación de escritorio en .NET (C#, Windows Forms) usando Visual Studio Code. 
- La base de datos gestiona artículos (productos como joyas, relojes y accesorios) y ventas, con una tabla de auditoría futura via triggers.

**Autor**: Andrea Sierra  
**Fecha**: 21/10/2025  
**Versión**: 1.0  

## Estructura de la Base de Datos
- **Nombre de la DB**: JOYERIA
- **Tablas Principales**: ARTICULOS (productos), VENTAS (transacciones).
- **Tabla Adicional**: AUDITORIA (para logs de cambios, se poblará con triggers).
- **Relaciones**: VENTAS tiene una FK a ARTICULOS (Id_Articulos_FK) con ON DELETE CASCADE, lo que elimina ventas asociadas si se borra un artículo.
- **Datos de Ejemplo**: Incluidos para testing (10 artículos, 5 ventas).

## Tablas

### TABLA ARTICULOS
Almacena información de productos en la joyería.

| Columna          | Tipo          | Descripción                          | Constraints |
|------------------|---------------|--------------------------------------|-------------|
| Id_Articulo     | INT           | ID único del artículo (auto-incremental) | PRIMARY KEY, IDENTITY(1,1) |
| Nombre          | VARCHAR(50)   | Nombre del producto                  | NOT NULL    |
| Categoria       | VARCHAR(50)   | Categoría (e.g., Joyas, Relojes)     | -           |
| NombreProveedor | VARCHAR(50)   | Nombre del proveedor                 | -           |
| Precio          | DECIMAL(10,2) | Precio unitario                      | NOT NULL    |
| Stock           | INT           | Cantidad en inventario               | DEFAULT 0   |

**Datos de Ejemplo**:
- Anillo de plata con circonitas (Precio: 89.99, Stock: 15)
- Colgante de oro blanco 18k con diamante (Precio: 450.50, Stock: 8)
- ... (ver script para más).

### TABLA VENTAS
Registra transacciones de ventas.

| Columna          | Tipo          | Descripción                          | Constraints |
|------------------|---------------|--------------------------------------|-------------|
| Id_Venta        | INT           | ID único de la venta (auto-incremental) | PRIMARY KEY, IDENTITY(1,1) |
| FechaHora       | DATETIME      | Fecha y hora de la venta             | DEFAULT GETDATE(), NOT NULL |
| Id_Articulos_FK | INT           | ID del artículo vendido              | NOT NULL, FK a ARTICULOS (ON DELETE CASCADE) |
| Cantidad        | INT           | Cantidad vendida                     | NOT NULL    |
| Total           | DECIMAL(12,2) | Total de la venta (Cantidad * Precio)| NOT NULL    |

**Datos de Ejemplo**:
- Venta de 2 anillos (Total: 179.98)
- Venta de 1 colgante (Total: 450.50)
- ... (ver script para más).

### TABLA AUDITORIA (Pendiente)
Para logs de operaciones (INSERT, UPDATE, DELETE).

| Columna         | Tipo          | Descripción                          |
|-----------------|---------------|--------------------------------------|
| Id_Auditoria    | BIGINT        | ID único del log                     |
| FechaHora       | DATETIME      | Fecha y hora del cambio              |
| UsuarioSQL      | VARCHAR(128)  | Usuario que realizó la acción        |
| TablaAfectada   | VARCHAR(50)   | Tabla modificada (e.g., ARTICULOS)   |
| ID_Afectado     | INT           | ID del registro afectado             |
| Tipo_Operacion  | CHAR(1)       | 'I' (Insert), 'U' (Update), 'D' (Delete) |
| NombreProducto  | VARCHAR(50)   | Nombre del producto afectado         |
| CampoAfectado   | VARCHAR(50)   | Columna cambiada (e.g., Precio)      |
| ValorAnterior   | VARCHAR(MAX)  | Valor antes del cambio               |
| ValorNuevo      | VARCHAR(MAX)  | Valor después del cambio             |
| TotalVenta      | DECIMAL(12,2) | Total de venta (si aplica)           |

Se poblará con triggers en ARTICULOS y VENTAS.

## Vistas
Vistas para consultas simplificadas.

### vw_VistaArticulo
Muestra detalles de artículos sin IDs.

```sql
SELECT Nombre, Categoria, NombreProveedor, Precio, Stock FROM ARTICULOS;
