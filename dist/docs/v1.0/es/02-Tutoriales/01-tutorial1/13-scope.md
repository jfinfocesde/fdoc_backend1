---
title: "13. Scope (Ámbito)"
position: 13
---


El **Scope** define dónde "vive" y es visible una variable.

## Tipos de Ámbito
1.  **Variables de Clase (Static)**: Viven en toda la clase. Cualquier método puede usarlas.
2.  **Variables Locales**: Viven solo dentro del método donde se crearon. Mueren al terminar el método.
3.  **Variables de Bloque**: Viven solo dentro de las llaves `{ ... }` (ej: dentro de un `if` o `for`).

```tabs
---[tab title="Topic13_Scope.java" lang="java"]---
package com.cesde;

public class Topic13_Scope {

    // Variable Global (Estática)
    static int variableGlobal = 100;

    public static void explicar() {
        System.out.println("--- TEMA 13: SCOPE ---");
        System.out.println("Global inicial: " + variableGlobal);

        // Variable Local
        int variableLocal = 10;
        System.out.println("Local main: " + variableLocal);

        cambiarValores();
        System.out.println("Global modificada: " + variableGlobal);
        
        // Bloque aislado
        {
            int blockVar = 999;
            System.out.println("Bloque: " + blockVar);
        }
        // blockVar no existe aquí
    }

    public static void cambiarValores() {
        variableGlobal = 200; // Accede a global
        int otraLocal = 50; // Solo existe aquí
        System.out.println("Local método: " + otraLocal);
    }
}
```
