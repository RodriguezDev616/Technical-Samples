# Ejemplo de Especificación Funcional - Módulo de Inventario

**Autor:** [Tu Nombre] - Ingeniera de Sistemas
**Contexto:** Optimización de flujo de salida de mercancía para logística 3PL.

## 1. Historia de Usuario
**COMO:** Encargado de Despacho.
**QUIERO:** Que el sistema valide automáticamente la existencia en el inventario antes de generar una etiqueta de envío.
**PARA:** Evitar la venta de productos sin stock y reducir errores en la cadena de suministro.

## 2. Especificaciones Técnicas (Para Desarrolladores)
- **Validación de Base de Datos:** Consultar tabla `inventory_stocks` filtrando por `sku_id` y `warehouse_id`.
- **Lógica:** Si `available_quantity` < `order_quantity`, el sistema debe retornar un error 400 y bloquear el proceso de "Checkout".
- **API:** El endpoint `/api/v1/shipments/create` debe incluir este check de stock como middleware.

## 3. Criterios de Aceptación
- El sistema debe responder en menos de 200ms.
- Si el stock es insuficiente, se debe mostrar un mensaje al usuario indicando la cantidad faltante.
- Cada validación exitosa debe quedar registrada en el log de movimientos del sistema.
