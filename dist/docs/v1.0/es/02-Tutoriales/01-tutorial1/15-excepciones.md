---
title: "15. Excepciones"
position: 15
---


Las **excepciones** son errores que ocurren durante la ejecución (runtime). Para evitar que el programa se cierre abruptamente ("crashee"), usamos bloques `try-catch`.

## Estructura

```steps
### 1. Try
Bloque donde colocas el código "peligroso" que podría fallar.

### 2. Catch
Bloque que se activa *solo* si ocurre una excepción específica en el `try`.

### 3. Finally
Bloque opcional que se ejecuta **siempre**, haya error o no. Ideal para cerrar conexiones.
```


```tabs
---[tab title="Topic15_Excepciones.java" lang="java"]---
package com.cesde;

public class Topic15_Excepciones {

    public static void explicar() {
        System.out.println("--- TEMA 15: EXCEPCIONES ---");

        try {
            int divisor = 0;
            int resultado = 10 / divisor; // Error: División por cero
            System.out.println("Resultado: " + resultado);
        } catch (ArithmeticException e) {
            System.out.println("¡Error! No dividas por cero.");
        } catch (Exception e) {
            System.out.println("Error desconocido: " + e.getMessage());
        } finally {
            System.out.println("Fin del intento.");
        }
        
        System.out.println("El programa sigue vivo.");
    }
}
```
