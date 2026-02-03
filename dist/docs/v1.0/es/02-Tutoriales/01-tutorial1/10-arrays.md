---
title: "10. Arrays"
position: 10
---

Estructuras de datos de tamaño fijo que almacenan múltiples valores del mismo tipo.

## Conceptos Clave
- **Índice Base 0**: El primer elemento es `array[0]`.
- **Tamaño Fijo**: Una vez declarado `new int[5]`, no puede crecer a 6.
- **Clase Arrays**: Helper útil (`Arrays.sort`, `Arrays.toString`).

```tabs
---[tab title="Topic10_Arrays.java" lang="java"]---
package com.cesde;
import java.util.Arrays;

public class Topic10_Arrays {

    public static void explicar() {
        System.out.println("--- TEMA 10: ARRAYS ---");

        // 1. Declaración Directa
        int[] numeros = { 10, 50, 20, 40, 30 };

        // 2. Declaración con Tamaño
        int[] edades = new int[5]; // [0, 0, 0, 0, 0]
        edades[0] = 18;

        // 3. Clase Arrays (Helpers)
        Arrays.sort(numeros); // Ordenar
        System.out.println("Ordenado: " + Arrays.toString(numeros));

        // 4. Recorrer (For Tradicional)
        // Útil si necesitas el índice 'i' para modificar
        for (int i = 0; i < numeros.length; i++) {
            numeros[i] *= 2;
        }

        // 5. Recorrer (For-Each)
        // Útil solo para leer
        System.out.print("Valores x2: ");
        for (int n : numeros) {
            System.out.print(n + " ");
        }
        
        System.out.println("\n--------------------------------\n");
    }
}
```
