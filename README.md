
# Proyecto JOYERIA

## Descripción
Aplicación de escritorio para gestión de una joyería, desarrollada en .NET (C#, Windows Forms) con base de datos SQL Server. Maneja artículos (inventario) y ventas, con auditoría futura via triggers. Proyecto final para curso de SQL Server.

**Autor**: Andrea Sierra  
**Fecha**: 21/10/2025  

## Requisitos
- SQL Server (Express o superior).
- .NET Framework (para Windows Forms).
- Visual Studio Code o Visual Studio.

## Instalación
1. Clona el repo: `git clone https://github.com/tu-usuario/JOYERIA.git`
2. Ejecuta el script SQL (`JOYERIA.sql`) en SSMS para crear DB, tablas, datos, vistas y SP.
3. Abre el proyecto .NET en VS/VSC.
4. Configura connection string en app.config o código (e.g., `Server=.;Database=JOYERIA;Integrated Security=True;`).
5. Compila y ejecuta la app.

## Estructura
- `/SQL`: Scripts SQL (creación, inserts, SP).
- `/App`: Código C# (Forms para CRUD, conexión a DB).
- `DOCUMENTACION.md`: Detalles de DB, tablas, vistas, SP.

## Uso
- Form Artículos: Agregar, editar, eliminar, listar productos.
- Form Ventas: Registrar ventas (actualiza stock auto), listar ventas.
- Pendiente: Auditoría y más features.

## Contribuciones
Para sugerencias, abre un issue.

## Licencia
MIT License.
