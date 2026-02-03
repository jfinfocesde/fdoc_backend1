---
title: "3. Variables y Constantes"
position: 3
---


Una **variable** es como una caja en la memoria donde guardamos datos. Tiene un nombre y un tipo. Una **constante** es una caja sellada: una vez que guardas algo, no puedes cambiarlo.

## Conceptos
- **Declaración**: Reservar el espacio (`int edad;`)
- **Inicialización**: Darle el primer valor (`edad = 18;`)
- **Inferencia (`var`)**: Dejar que Java adivine el tipo (Java 10+).
- **Constantes (`final`)**: Valores inmutables (`final double PI = 3.14;`).

```tabs
---[tab title="Topic03_Variables.java" lang="java"]---
package com.cesde;

public class Topic03_Variables {

    public static void explicar() {
        System.out.println("--- TEMA 3: VARIABLES Y CONSTANTES ---");

        // Declaración e inicialización
        int edad; // Declaración
        edad = 25; // Inicialización

        int puntos = 100; // Ambas en una línea

        System.out.println("Valor inicial de puntos: " + puntos);

        puntos = 200; // Reasignación
        System.out.println("Valor modificado de puntos: " + puntos);

        // Inferencia de tipos (Java 10+)
        var mensaje = "Hola con var"; // El compilador deduce que es String
        System.out.println(mensaje);

        // Constantes (final)
        // Por convención, usamos MAYÚSCULAS.
        final double PI = 3.14159;
        
        System.out.println("El valor de PI es constante: " + PI);

        // PI = 3.14; // ERROR: no se puede reasignar una constante
        
        System.out.println("--------------------------------\n");
    }
}
```
