# NovaGest

Aplicación web adaptable en español para gestionar productos, ventas e inventario de bodegas y ferreterías.

## Ejecutar

Abre `index.html` en un navegador moderno. No necesita instalar dependencias ni ejecutar un servidor. En el acceso de demostración usa:

- Correo: `admin@novagest.pe`
- Contraseña: `NovaGest2026`

La primera carga incluye productos y ventas de demostración (identificadas como **Demo**). Los cambios se guardan en `localStorage` de ese navegador. Desde **Usuarios y configuración** puedes restablecer los datos.

## Funcionalidad disponible

- Inicio con indicadores, ventas recientes, alertas y resumen de productos destacados.
- Crear, editar, buscar, filtrar y desactivar productos; seguimiento de stock mínimo y valor de inventario.
- Registro de una venta con varias líneas, controles de cantidad, validación del stock y actualización única al confirmar. Cancelar no modifica existencias.
- Historial con detalle de ventas y exportación CSV.
- Reportes basados en las ventas guardadas y descarga CSV compatible con Excel.
- Notificaciones de stock bajo y productos agotados.
- Perfil local, navegación móvil y persistencia local.

## Límites de la demostración

La pantalla de acceso permite únicamente las credenciales de ejemplo y **no constituye autenticación segura**. `localStorage` es almacenamiento local al navegador, no una base de datos compartida, y el JavaScript del navegador no puede garantizar consistencia ante usuarios concurrentes. No uses esta demo para operaciones comerciales reales hasta configurar un backend con autenticación y autorización de servidor.

## Conectar Supabase

`supabase/schema.sql` define las tablas, restricciones, RLS y una función SQL transaccional para registrar ventas y descontar existencias de forma atómica. Para producción:

1. Crea un proyecto Supabase y ejecuta el esquema mediante el SQL Editor.
2. Configura Supabase Auth y una política de perfiles que asocie `usuarios.id_usuario` con `auth.uid()`; no almacenes contraseñas en tu tabla de perfiles.
3. Llama a `registrar_venta` desde un backend autenticado o RPC con las líneas de venta. La función bloquea las filas de producto, valida cantidades y descuenta el stock dentro de una transacción.
4. Añade credenciales públicas mediante configuración de entorno y mantén cualquier clave `service_role` exclusivamente en servidor.
5. Sustituye el almacenamiento de demostración por lecturas/escrituras del backend y limita los permisos por negocio y rol.

No se incluyeron credenciales de Supabase, por lo que la app identifica claramente el modo demo.
