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

