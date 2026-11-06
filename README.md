# Modelo Relacional de Bases de Datos 8



## Descripción



Este documento detalla el esquema y la estructura del modelo relacional de bases de datos para un sistema de gestión de inventario, depósitos, proveedores, órdenes de compra y control de stock de productos.

---

## Estructura de Tablas y Atributos



### 1. Producto



* **PK (Clave Primaria):** `id_codigo_de_barra`


* **Atributos:**
* `descripción`


* `peso`


* `dimesiones`


* `Stock`





### 2. Deposito



* **PK (Clave Primaria):** `id_Deposito`


* **Atributos:**
* `nombre`


* `dirección`


* `cargo_responsable`


* `telefono`





### 3. Stock



* **FK (Claves Foráneas):**
* `id_codigo_de_barra` (asociado a la tabla Producto)


* `id_Deposito` (asociado a la tabla Deposito)




* **Atributos:**
* `cantidad_stock`


* `ubicación`


* `fecha_actualización`





### 4. Proveedor



* **PK (Clave Primaria):** `id_CUIL`


* **Atributos:**
* `persona_de_contacto`


* `pais_de_origen`


* `correo_electronico`


* `razón_social`





### 5. Producto-Proveedor



* **FK (Claves Foráneas):**
* `id_CUIL` (asociado a la tabla Proveedor)


* `id_codigo_de_barra` (asociado a la tabla Producto)




* **Atributos:**
* `precio_costo`


* `cantidad_de_stock`


* `condicion_de_pago`





### 6. Orden_de_Compra



* **PK (Clave Primaria):** `id_nroOrden`


* **Atributos:**
* `estado`


* `fecha_de_emisión`


* `deposito_de_deposito`




* **FK (Claves Foráneas):**
* `id_Deposito` (asociado a la tabla Deposito)


* `id_CUIL` (asociado a la tabla Proveedor)





### 7. Detalle-Orden-Compra



* **PK (Clave Primaria):** `id_detalle`


* **Atributos:**
* `precio_Pactado`


* `cantidad_pedida`


* `subtotal`




* **FK (Claves Foráneas):**
* `id_codigo_de_barra` (asociado a la tabla Producto)


* `id_nroOrden` (asociado a la tabla Orden_de_Compra)





---

## Relaciones Principales



* **Producto y Deposito (Stock):** La relación de muchos a muchos entre productos y depósitos para controlar las existencias físicas se gestiona mediante la tabla intermedia `Stock`.


* **Producto y Proveedor (Producto-Proveedor):** Un proveedor ofrece múltiples productos y un producto puede ser provisto por varios proveedores, vinculándose a través de la tabla `Producto-Proveedor` con el `id_CUIL` y el `id_codigo_de_barra`.


* **Orden de Compra y Deposito / Proveedor:** Cada orden de compra se emite hacia un proveedor específico (`id_CUIL`) y está asociada a un depósito de destino (`id_Deposito`).


* **Orden de Compra y Producto (Detalle-Orden-Compra):** Los ítems solicitados en cada orden de compra se estructuran en la tabla `Detalle-Orden-Compra`, relacionando el número de orden con el código de barras del producto.
