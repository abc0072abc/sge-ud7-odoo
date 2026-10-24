# Proceso de Venta Completo: Del Presupuesto a la Factura

En este apartado documento todo el flujo de venta que he realizado en Odoo, desde la creación de la primera oferta hasta el cobro de la factura, asegurándome de que cada acción la hace el usuario con el rol que le toca y sin usar la cuenta de administrador.

---

## 1. Tabla de pasos, usuarios y documentos generados

| Paso | Qué se hace | Quién lo hace | Su rol | Documento | Estado final |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **1. Presupuesto** | Crea el presupuesto con 3 productos, 10% de descuento en el monitor, validez de 30 días y pago a 30 días | Lucía Gómez (`comercial@kromastudio.es`) | Comercial | `S00003` | Presupuesto enviado |
| **2. Confirmar pedido** | Revisa la oferta de Lucía y la confirma para pasarla a pedido en firme | Agustín Borreguero Castro (`responsable.ventas@kromastudio.es`) | Responsable de Ventas | `S00003` | Pedido de venta |
| **3. Entrega de almacén** | Valida la salida de los productos físicos del almacén | Agustín Borreguero Castro (`responsable.ventas@kromastudio.es`) | Responsable de Ventas / Inventario | `WH/OUT/00001` | Hecho |
| **4. Factura** | Crea la factura del pedido, comprueba los importes y la publica | Manuel Ortega (`administracion@kromastudio.es`) | Facturación | `INV/2026/00001` | Publicado |
| **5. Pago** | Registra el pago completo recibido por el banco | Manuel Ortega (`administracion@kromastudio.es`) | Facturación | `INV/2026/00001` | Pagado |

---

## 2. Control de existencias (Stock)

Antes de hacer la venta comprobé el stock inicial y al terminar la entrega validé que las unidades habían bajado correctamente:

- **Tableta Gráfica Pro Pen 16"** (Bien con seguimiento):
  - Teníamos: **15 unidades**
  - Se entregan en el albarán: **2 unidades**
  - Quedan en stock: **13 unidades**

- **Monitor Colorimeter 27" 4K** (Bien con seguimiento):
  - Teníamos: **8 unidades**
  - Se entrega en el albarán: **1 unidad**
  - Quedan en stock: **7 unidades**

- **Servicio de Calibración in situ** (Servicio):
  - No descuenta stock físico porque es un servicio técnico.

---

## 3. Documentos adjuntos

Los PDF oficiales generados directamente desde Odoo están subidos en esta misma carpeta:
- Presupuesto: [`presupuesto.pdf`](./presupuesto.pdf)
- Factura: [`factura.pdf`](./factura.pdf)