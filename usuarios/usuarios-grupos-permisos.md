# Gestión de Usuarios, Grupos, Roles y Privilegios

## 1. Tipos de Usuario en Odoo
- **Usuario Interno:** Miembros de la plantilla con acceso al backend de gestión según los módulos asignados. Consumen licencia en planes comerciales y disponen de privilegios operativos.
- **Usuario Portal:** Clientes o proveedores que acceden a una vista web simplificada para consultar sus propios presupuestos, pedidos, albaranes o facturas, sin acceso a la interfaz de administración.
- **Usuario Público:** Visitantes no autenticados que navegan por el catálogo web o eCommerce sin permisos de gestión.

---

## 2. Matriz de Usuarios y Asignación de Roles (Mínimo Privilegio)

| Usuario | Nombre y Apellidos | Correo de Acceso | Puesto / Rol | Tipo de Usuario | Privilegios por Módulo | Justificación Operativa |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **User 1** | Carlos Ruiz Delgado *(Tu Nombre)* | `responsable.ventas@kromastudio.es` | Responsable de Ventas | Interno | - **Ventas:** Administrador<br>- **Inventario:** Usuario<br>- **Facturación:** Ninguno | Supervisa el pipeline de ventas de todo el equipo, aprueba pedidos y coordina disponibilidad con inventario sin intervenir en cobros. |
| **User 2** | Lucía Gómez Ramos | `comercial@kromastudio.es` | Comercial | Interno | - **Ventas:** Solo mostrar documentos propios<br>- **Inventario:** Ninguno<br>- **Facturación:** Ninguno | Gestiona prospectos y elabora ofertas a clientes asignados. No debe ver negociaciones ajenas ni tocar contabilidad. |
| **User 3** | Manuel Ortega Beltrán | `administracion@kromastudio.es` | Técnico de Facturación | Interno | - **Ventas:** Ninguno<br>- **Inventario:** Ninguno<br>- **Facturación:** Responsable de facturación | Emite facturas a partir de pedidos cerrados y registra cobros bancarios; no interviene en el proceso comercial inicial. |

---

## 3. Grupo Personalizado: `Kroma Studio / Comercial Junior`

### A. Herencia de Grupos
- **Grupo heredado:** `Ventas / Usuario: solo mostrar documentos propios` (`sales_team.group_sale_salesman`).
- **Motivo:** Permite al comercial novel operar en la interfaz estándar de ventas sin otorgarle permisos de administración global.

### B. Derechos de Acceso sobre Modelos (ACL)

| Nombre del Permiso | Modelo Técnico | Nombre del Modelo | Lectura (Read) | Escritura (Write) | Creación (Create) | Eliminación (Unlink) | Justificación |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: | :--- |
| **Acceso Presupuestos** | `sale.order` | Pedido de venta | **Sí** | **Sí** | **Sí** | **No** | Puede generar y editar sus cotizaciones, pero no puede eliminar registros históricos ni presupuestos rechazados. |
| **Consulta Catálogo** | `product.template` | Plantilla de producto | **Sí** | **No** | **No** | **No** | Puede revisar precios e información técnica para presupuestar, pero no puede modificar costes ni márgenes. |

- **Usuario asignado al grupo:** Lucía Gómez Ramos (`comercial@kromastudio.es`).

---

## 4. Evidencias de Validación de Permisos
1. **Comercial vs. Contabilidad:** Al autenticarse como `comercial@kromastudio.es`, los módulos de Facturación e Inventario no se muestran en el tablero principal.
2. **Restricción de Borrado:** Al intentar eliminar un presupuesto de prueba con el usuario comercial, el sistema deniega la acción por restricción de permisos del modelo `sale.order`.
3. **Aislamiento Comercial:** Lucía Gómez solo visualiza las ofertas donde figura como comercial asignada; los presupuestos emitidos por el Responsable de Ventas permanecen ocultos.