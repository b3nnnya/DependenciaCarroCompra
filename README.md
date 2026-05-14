# Análisis de Dependencia: Sistema de Carrito de Compras

Este repositorio contiene la solución a la actividad de análisis de código fuente Java para el reconocimiento de relaciones de dependencia.

## i. Identificación de clases y contexto del problema

### Clases identificadas:
*   **`Calculadora`**: Representa un componente utilitario encargado de realizar operaciones aritméticas elementales (suma y multiplicación) con dos números.
*   **`CarroCompra`**: Representa un carrito que gestiona una lista de productos (mediante una matriz bidimensional de cantidades y precios) y determina el costo total de la compra.

### Contexto del problema:
El sistema simula el proceso de pago de un carrito de compras. Para mantener el código organizado y no sobrecargar a la clase `CarroCompra` con responsabilidades matemáticas complejas, esta delega el cálculo del subtotal de cada ítem (cantidad por precio) a un componente externo especializado: la clase `Calculadora`.

---

## ii. Análisis de atributos, métodos y relaciones

### Clase `Calculadora`
*   **Atributos:** 
    *   `n1`, `n2` (Privados, tipo `int`).
*   **Métodos:**
    *   `Calculadora()`: Constructor por defecto (inicializa en 0).
    *   `Calculadora(int num1, int num2)`: Constructor con parámetros.
    *   `sumar()` y `multiplicar()`: Realizan las operaciones correspondientes y retornan el resultado matemático (`int`).
    *   `setN1(int num1)` y `setN2(int num2)`: Modificadores (setters) para actualizar los valores de los atributos.

### Clase `CarroCompra`
*   **Atributos:** 
    *   `productos`: Privado, matriz `int[][]` de 2 filas por 5 columnas.
*   **Métodos:**
    *   `CarroCompra()`: Constructor que inicializa la matriz simulando 5 productos fijos (cantidad 1, precio 1000).
    *   `calcularTotal()`: Método privado que recorre la matriz acumulando la suma de los subtotales.
    *   `subTotal(int cant, int precio)`: Método privado que calcula el valor individual de un ítem.
    *   `mostrarTotal()`: Método público que imprime en la consola el valor final de la compra.

### Relación existente: Dependencia (Uso)
Existe una **Relación de Dependencia** dirigida desde `CarroCompra` hacia `Calculadora` (se lee como: "`CarroCompra` usa a `Calculadora`"). 

**Justificación:** 
Esto se evidencia en el método `subTotal` de la clase `CarroCompra`. En el cuerpo de dicho método, se instancia un objeto local de la clase `Calculadora` (`Calculadora calc = new Calculadora(cant, precio);`) con el único propósito de invocar su método `multiplicar()`. 

Dado que la `Calculadora` es instanciada, utilizada para una tarea específica y desechada exclusivamente durante el ciclo de vida de ese método (no forma parte de los atributos de la clase `CarroCompra`), se establece una dependencia estructural transitoria clara.
