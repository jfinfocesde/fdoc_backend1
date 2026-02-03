---
title: "8. Bucles"
position: 8
---


Estructuras para repetir bloques de código.

## Tipos de Bucles

```comparison-table
---
headers:
  - "Tipo"
  - "Descripción"
  - "Cuándo usarlos"
rows:
  - ["For", "Iteración definida con contador", "Sabes cuántas veces repetir (1 a N)"]
  - ["While", "Iteración basada en condición", "No sabes cuándo terminará (ej: leer hasta fin de archivo)"]
  - ["Do-While", "Igual que While, pero ejecuta al menos una vez", "Menús interactivos"]
---
```

## Anatomía del Bucle FOR

```steps
### 1. Inicialización
Se define una variable de control, comúnmente llamada `i`.
Ejemplo: `int i = 0;`

### 2. Condición
Se evalúa antes de cada iteración. Si es `true`, el bucle continúa.
Ejemplo: `i < 10;`

### 3. Actualización
Ocurre al final de cada vuelta. Modifica la variable de control.
Ejemplo: `i++;`
```


```tabs
---[tab title="Topic08_Bucles.java" lang="java"]---
package com.cesde;

public class Topic08_Bucles {

    public static void explicar() {
        System.out.println("--- TEMA 8: BUCLES ---");

        // 1. FOR (Conoces el número de iteraciones)
        for (int i = 1; i <= 3; i++) {
            System.out.println("Iteración For: " + i);
        }

        // 2. WHILE (Mientras condición sea true)
        int contador = 3;
        while (contador > 0) {
            System.out.println("Cuenta regresiva: " + contador);
            contador--; 
        }

        // 3. DO-WHILE (Garantiza 1 ejecución)
        int num = 10;
        do {
            System.out.println("Se ejecuta aunque num(10) no sea < 5");
        } while (num < 5);

        // 4. Break y Continue
        System.out.print("Pares hasta 6: ");
        for (int i = 0; i < 10; i++) {
            if (i % 2 != 0) continue; // Salta impares
            if (i > 6) break; // Termina si es mayor a 6
            System.out.print(i + " ");
        }

        System.out.println("\n--------------------------------\n");
    }
}
```
