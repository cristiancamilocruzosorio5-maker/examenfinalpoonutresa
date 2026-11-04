# Evidencias: equipo <cruz osorio>, <tique marin>

**Integrantes:** <cristian camilo cruz sosrio> <carlos duvan tique marin>

## 1. Errores de sintaxis corregidos

| # | Archivo | Línea | Mensaje del compilador | Corrección |
|---|---------|-------|------------------------|------------|
| 1 | Adicion.java | 4 | `identifier expected` (implement) | Se cambió `implement` por `implements`. |
| 2 | LineaPedido.java | 11 | `incompatible types: boolean cannot be converted to ProductoMenu` (= en vez de ==) | Se cambió `=` por `==`. |
| 3 | LineaPedido.java | 34 | `attempting to assign weaker access privileges; was public` | Se agregó la palabra reservada `public` en `calcularPrecio()`. |
| 4 | Panaderia.java | 31 | `unclosed string literal` | Se cerró la comilla doble faltante en `"Panadería"`. |
| 5 | Pedido.java | 47 | `variable total might not have been initialized` | Se inicializó la variable `double total = 0;`. |
| 6 | Pedido.java | 80 | ` ';' expected` (en bucle for) | Se cambiaron las comas `,` por puntos y comas `;` en la estructura del bucle for. |
| 7 | Pedido.java | 9 | `cannot assign a value to final variable pagado` | Se eliminó el modificador `final` del atributo `pagado`. |
| 8 | PlatoFuerte.java | 11 | `constructor ProductoMenu in class ProductoMenu cannot be applied to given types` | Se añadió el parámetro `stock` faltante en la llamada a `super(...)`. |
| 9 | Brunch.java | 43 | Incompatibilidad en comparación de Strings con `==` | Se cambió `p.getCodigo() == codigo` por `p.getCodigo().equalsIgnoreCase(codigo)`. |
| 10 | Brunch.java | 54 | `missing return statement` | Se agregó `return null;` al finalizar el método `buscarMesa()`. |
| 11 | Brunch.java | 72 | `unreachable statement` | Se reordenó la instrucción `pedidos.add(pedido);` antes del `return pedido;`. |
| 12 | ProductoMenu.java | Varios | Métodos abstractos no declarados | Se declararon los métodos abstractos `minutosPreparacion()`, `getCategoria()` y `esVegetariano()`. |
| 13 | Mesa.java | Varios | Sobrecarga de constructores para número de mesa | Se implementaron los constructores para recibir tanto `int` como `String`. |
| 14 | Pedido.java | Varios | Método `marcarPagado()` bloqueado | Se ajustó el estado de `pagado` para permitir la transición al cobrar el pedido. |
| 15 | Brunch.java | Varios | Validación de stock y disponibilidad | Se aseguraron las validaciones de control de inventario en `vender()` y `puedeVender()`. |

## 2. Errores de lógica corregidos
| # | Archivo y método | Qué hacía mal | Pista (fila de la tabla) | Cómo lo corregimos |
|---|------------------|---------------|--------------------------|--------------------|
| 1 | `Bebida.calcularPrecio()` | Usaba un operador estricto `>` en vez de `>=` para el tamaño grande de 500 ml, ignorando el recargo del Jugo de mandarina. | Sección 1 (Precios de la carta) | Se cambió a `mililitros >= MILILITROS_TAMANO_GRANDE`. |
| 2 | `ProductoMenu` (atributo stock) | El atributo stock era `static`, lo que hacía que todas las instancias compartieran un inventario global en lugar de ser independiente por producto. | Sección 1 (Stock de la carta) | Se eliminó el modificador `static` de la variable `stock`. |
| 3 | `ProductoMenu.puedeVender()` | Validaba el stock con un operador incorrecto, impidiendo el despacho correcto de las unidades disponibles exactas. | Sección 2 (Disponibilidad y arepa) | Se ajustó la condición a `stock >= cantidad`. |
| 4 | `ProductoMenu.setDisponible()` | Tenía un error de asignación interna (`disponible = disponible;`), por lo que nunca cambiaba el estado del producto. | Sección 2 (Arepa no disponible) | Se corrigió asignando correctamente con `this.disponible = disponible;`. |
| 5 | `LineaPedido.calcularPrecio()` | Si bien en este caso se validó el acumulador, el diseño original requería asegurar que cada unidad multiplicara el precio base más sus adiciones. | Sección 7 (Polimorfismo / Línea de pedido) | Se mantuvo la operación correcta `(producto.calcularPrecio() + sumaAdiciones) * cantidad`. |
| 6 | `Pedido.calcularDescuento()` | Aplicaba el plan familiar utilizando un operador O (`||`) en lugar de exigir ambas condiciones simultáneamente con Y (`&&`). | Sección 5 (Cuentas - Familia) | Se cambió `||` por `&&` (`personas >= 4 && subtotal >= 150000`). |
| 7 | `Pedido.calcularImpoconsumo()` | Calculaba el 8% sobre el subtotal bruto total sin restarle primero el descuento familiar obtenido. | Sección 5 (Cuentas - Familia) | Se aplicó la base restando el descuento previo: `(subtotal - descuento) * 0.08`. |
| 8 | `Pedido.calcularPropina()` | Incluía erróneamente el valor del impoconsumo dentro de la base de cálculo para la propina voluntaria. | Sección 5 (Cuentas - Familia) | Se calculó la propina exclusivamente sobre el subtotal menos el descuento, sin sumar el impoconsumo. |
| 9 | `Pedido.esVegetariano()` | Retornaba `true` prematuramente tras evaluar únicamente el primer elemento de la lista sin revisar los demás. | Sección 4 (Pedidos - Vegetariano) | Se estructuró el bucle para que retorne `false` al encontrar un solo producto no vegetariano, y `true` solo si todos lo cumplen. |
| 10 | `Brunch.abrirPedido()` y `cerrarPedido()` | No validaba adecuadamente si la mesa seleccionada estaba ocupada, y al cobrar olvidaba liberar la mesa para el siguiente grupo. | Sección 6 (Cierre - Mesa libre) | Se integraron las validaciones de `mesa.isOcupada()`, `mesa.ocupar()` y `mesa.liberar()`. |

## 3. Revisión de código
| # | Archivo y método | Por qué era una mala práctica | Qué cambiamos |
|---|------------------|-----------------------------|---------------|
| R1 | `LineaPedido.obtenerEstacion()` | Polimorfismo desaprovechado con `instanceof`, violando OCP ante nuevas clases. | Se implementó el método abstracto `obtenerEstacion()` en `ProductoMenu` y se sobrescribió polimórficamente en cada clase hija. |
| R2 | `Pedido` (Cálculos financieros) | Uso de números mágicos (valores literales sueltos sin contexto como `0.10` o `150000`). | Se declararon constantes estáticas descriptivas (`TASA_DESCUENTO`, `TASA_IMPOCONSUMO`, etc.). |
| R3 | `Pedido` (Métodos de cálculo) | Código duplicado al invocar de forma repetida y redundante la función `calcularSubtotal()`. | Se almacenó el resultado en una variable local al inicio de cada método de cálculo para reutilizarlo. |
| R4 | `Brunch.getMenu()` | Lista interna expuesta que rompía el encapsulamiento al retornar la colección directamente. | Se modificó para retornar una copia defensiva (`new ArrayList<>(menu)`). |
| R5 | `Brunch` (Método privado auxiliar) | Código difícil de leer debido a un método auxiliar con un nombre críptico y de una sola letra (`v()`). | Se refactorizó cambiando su nombre por uno semántico y claro (`validarDisponibilidad()`). |