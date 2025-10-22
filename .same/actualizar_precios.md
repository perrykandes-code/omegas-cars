# 🔄 Actualización: Sistema de Doble Precio

## ⚠️ IMPORTANTE: Ejecutar en tu Base de Datos

Para agregar la funcionalidad de **Precio Original** y **Precio con Descuento**, necesitas ejecutar este comando SQL en tu base de datos:

---

## 📋 Comando SQL para Actualizar

```sql
-- Agregar columna precio_descuento a la tabla productos
ALTER TABLE productos
ADD COLUMN precio_descuento DECIMAL(10,2) DEFAULT NULL AFTER precio;
```

---

## ✅ Cómo Ejecutar

### Opción 1: phpMyAdmin
1. Abre phpMyAdmin
2. Selecciona la base de datos `omega_cars`
3. Ve a la pestaña **SQL**
4. Pega el comando anterior
5. Haz clic en **Continuar**

### Opción 2: MySQL Command Line
```bash
mysql -u tu_usuario -p omega_cars
# Pega el comando ALTER TABLE
```

### Opción 3: Desde tu aplicación PHP
Crea un archivo temporal `actualizar_db.php` con este contenido:

```php
<?php
include('includes/db.php');

$sql = "ALTER TABLE productos
        ADD COLUMN precio_descuento DECIMAL(10,2) DEFAULT NULL AFTER precio";

if ($conn->query($sql) === TRUE) {
    echo "✅ Base de datos actualizada correctamente";
} else {
    echo "❌ Error: " . $conn->error;
}

$conn->close();
?>
```

Luego:
1. Sube el archivo a tu servidor
2. Accede a `http://tu-dominio.com/actualizar_db.php`
3. **ELIMINA el archivo** después de la actualización

---

## 🎯 ¿Qué hace este cambio?

- ✅ Agrega una nueva columna `precio_descuento` a la tabla `productos`
- ✅ Es **opcional** (NULL por defecto)
- ✅ **NO afecta** los productos existentes
- ✅ Permite decimales (formato: 10,2)

---

## 📊 Nuevas Funcionalidades

### 1. **En Productos**
- Campo "Precio Original" (obligatorio)
- Campo "Precio con Descuento" (opcional)
- Si agregas descuento, se muestra:
  - ~~Precio original tachado~~
  - **Precio con descuento destacado**
  - Etiqueta animada con el % de descuento

### 2. **En Ventas**
- El selector muestra productos con "OFERTA" cuando tienen descuento
- El carrito muestra el precio original tachado
- Se usa automáticamente el precio con descuento para calcular el total

### 3. **En Factura PDF**
- Muestra precios con descuento cuando aplica
- Línea adicional mostrando "Precio con descuento" y el %
- **AHORRO TOTAL** en verde al final
- Cálculo correcto del total a pagar

---

## 💡 Ejemplo de Uso

### Agregar Producto con Descuento:
1. Ve a **Productos**
2. Clic en **Agregar Nuevo Producto**
3. Llena los campos:
   - Marca: Toyota Corolla
   - Descripción: 2024, Automático
   - **Precio Original: 25000.00**
   - **Precio con Descuento: 22000.00** ← ¡Nuevo!
   - Stock: 5
4. Guardar

### Resultado:
- En el catálogo verás:
  - ~~$25,000.00~~
  - **$22,000.00**
  - **-12%** (en etiqueta naranja animada)

---

## 🔍 Verificar la Actualización

Después de ejecutar el comando SQL, verifica con:

```sql
DESCRIBE productos;
```

Deberías ver la columna `precio_descuento` en la lista.

---

## ⚡ Compatibilidad

- ✅ **Productos sin descuento**: Funcionan igual que antes
- ✅ **Productos existentes**: No se ven afectados
- ✅ **Ventas antiguas**: Siguen funcionando normalmente

---

## 🎨 Vista Previa del Diseño

### Tarjeta de Producto CON descuento:
```
┌─────────────────────────┐
│ Toyota Corolla          │
│ 2024, Automático        │
│                         │
│ $25,000.00  $22,000.00  │
│    ────        ⭐       │
│              -12%       │
│                         │
│ [Editar] [Eliminar]     │
└─────────────────────────┘
```

### Tarjeta de Producto SIN descuento:
```
┌─────────────────────────┐
│ Honda Civic             │
│ 2023, Manual            │
│                         │
│ $20,000.00              │
│                         │
│ [Editar] [Eliminar]     │
└─────────────────────────┘
```

---

¡Listo! Con esta actualización tu sistema ahora maneja precios con descuento de forma profesional. 🚗✨
