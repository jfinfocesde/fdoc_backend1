---
title: "12. Parámetros"
position: 12
---


Los métodos son más poderosos cuando pueden recibir datos (Input) y devolver resultados (Output).

## Conceptos
- **Parámetros**: Variables recibidas por el método.
- **Retorno (`return`)**: Valor que el método devuelve a quien lo llamó. Si un método no es `void`, **debe** tener un `return`.

```tabs
---[tab title="Topic12_Parametros.java" lang="java"]---
package com.cesde;

public class Topic12_Parametros {

    public static void explicar() {
        System.out.println("--- TEMA 12: PARÁMETROS Y RETORNO ---");

        // 1. Recibir valores
        imprimirDatosPersona("Ana", 28);

        // 2. Retornar valor
        double total = calcularTotal(100.0, 0.19);
        System.out.println("Total con IVA: " + total);

        // 3. Retornar boolean (Validación)
        if (esMayorDeEdad(15)) {
            System.out.println("Pasa");
        } else {
            System.out.println("No pasa");
        }
    }

    // Recibe String e int
    public static void imprimirDatosPersona(String nombre, int edad) {
        System.out.println("Ficha: " + nombre + " (" + edad + " años)");
    }

    // Retorna double
    public static double calcularTotal(double subtotal, double iva) {
        return subtotal + (subtotal * iva);
    }

    // Retorna boolean
    public static boolean esMayorDeEdad(int edad) {
        return edad >= 18;
    }
}
```
