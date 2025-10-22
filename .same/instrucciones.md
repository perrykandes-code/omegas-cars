# 📝 Instrucciones de Actualización - Omega Cars

## ⚠️ IMPORTANTE: Actualización de Base de Datos

Para que las nuevas funcionalidades funcionen correctamente, **DEBES actualizar tu base de datos**.

### Opción 1: Base de Datos Nueva (Recomendado si estás empezando)

1. Ejecuta todo el archivo `db/database.sql` en phpMyAdmin o tu gestor de MySQL
2. Esto creará todas las tablas con la estructura correcta

### Opción 2: Actualizar Base de Datos Existente (Si ya tienes datos)

Si ya tienes productos y ventas en tu base de datos, ejecuta SOLO estos comandos SQL:

```sql
-- 1. Crear la nueva tabla de detalle de ventas
CREATE TABLE detalle_ventas (
  id INT AUTO_INCREMENT PRIMARY KEY,
  venta_id INT NOT NULL,
  producto_id INT NOT NULL,
  cantidad INT NOT NULL,
  precio_unitario DECIMAL(10,2) NOT NULL,
  subtotal DECIMAL(10,2) NOT NULL,
  FOREIGN KEY (venta_id) REFERENCES ventas(id) ON DELETE CASCADE,
  FOREIGN KEY (producto_id) REFERENCES productos(id)
);

-- 2. Modificar la tabla ventas (BACKUP PRIMERO!)
-- Si tienes ventas existentes, haz backup primero
ALTER TABLE ventas DROP FOREIGN KEY ventas_ibfk_1;
ALTER TABLE ventas DROP COLUMN producto_id;
ALTER TABLE ventas DROP COLUMN cantidad;
```

**ADVERTENCIA:** El paso 2 modificará tu tabla de ventas existente. Haz un backup antes de ejecutar.

---

## 🆕 Nuevas Funcionalidades

### 1. Gestión de Productos

#### Editar un Producto:
1. Ve a la página de Productos
2. Busca el producto que quieres editar
3. Haz clic en el botón verde **"Editar"**
4. El formulario se llenará automáticamente con los datos
5. Modifica lo que necesites
6. Haz clic en **"Actualizar Producto"**

#### Eliminar un Producto:
1. Ve a la página de Productos
2. Busca el producto que quieres eliminar
3. Haz clic en el botón rojo **"Eliminar"**
4. Confirma la acción en el mensaje de alerta
5. El producto se eliminará permanentemente

### 2. Sistema de Ventas con Carrito

#### Realizar una Venta:
1. Ve a la página de Ventas
2. Llena los **Datos del Cliente** (nombre, email, teléfono)
3. En **Agregar Productos**:
   - Selecciona un producto del desplegable
   - Ingresa la cantidad deseada
   - Haz clic en **"+ Agregar al Carrito"**
4. Repite el paso 3 para agregar más productos
5. Verás el **Carrito de Compra** con todos los productos agregados
6. Revisa los subtotales y el **Total general**
7. Si quieres eliminar un producto del carrito, haz clic en su botón **"Eliminar"**
8. Cuando estés listo, haz clic en **"Generar Factura PDF"**
9. La factura se descargará automáticamente

### 3. Factura PDF Mejorada

La factura ahora incluye:
- Encabezado con nombre de la empresa
- Número de factura único
- Datos completos del cliente
- **Tabla con todos los productos**:
  - Nombre del producto
  - Precio unitario
  - Cantidad
  - Subtotal
- **Total general** destacado
- Fecha y hora de la venta
- Diseño profesional con colores corporativos

---

## 💾 Estructura de Archivos

```
omegas-cars/
├── assets/
│   ├── css/
│   │   ├── products.css    (actualizado)
│   │   └── sales.css       (actualizado)
│   └── js/
├── db/
│   └── database.sql        (actualizado)
├── includes/
├── comprobantes/           (se crea automáticamente)
├── products.php            (actualizado)
└── sales.php               (actualizado)
```

---

## 🔧 Validaciones Implementadas

1. **Stock disponible**: No puedes agregar más productos de los que hay en stock
2. **Confirmación de eliminación**: Alerta antes de eliminar un producto
3. **Carrito vacío**: No puedes generar factura sin productos
4. **Campos requeridos**: Todos los datos del cliente son obligatorios
5. **Actualización automática de stock**: El stock se reduce automáticamente al realizar una venta

---

## 📱 Compatibilidad

- ✅ Diseño responsive (funciona en móviles y tablets)
- ✅ Navegadores modernos (Chrome, Firefox, Safari, Edge)
- ✅ PHP 7.0 o superior
- ✅ MySQL 5.6 o superior

---

## ❓ Soporte

Si encuentras algún problema:
1. Verifica que actualizaste la base de datos correctamente
2. Asegúrate de que la carpeta `comprobantes/` tenga permisos de escritura
3. Revisa los errores en la consola del navegador (F12)
4. Verifica que todos los archivos estén en su lugar

---

¡Listo! Tu sistema Omega Cars ahora tiene funcionalidades completas de gestión de productos y ventas con múltiples productos. 🚗✨
