---
title: "6. Librería Math"
position: 6
---


Java incluye una clase utilitaria llamada `Math` (java.lang.Math) que contiene métodos estáticos para realizar operaciones matemáticas complejas.

## Métodos Comunes

```feature-list
---
items:
  - title: "Math.pow"
    icon: "lucide:calculator"
    description: "Calcula la potencia (`base` elevado a `exp`)."
  - title: "Math.sqrt"
    icon: "lucide:radical"
    description: "Devuelve la raíz cuadrada positiva de un número."
  - title: "Math.random"
    icon: "lucide:shuffle"
    description: "Genera un número pseudoaleatorio doble entre 0.0 y 1.0."
  - title: "Math.round"
    icon: "lucide:circle-dot"
    description: "Redondea un valor decimal al entero más cercano."
---
```


```tabs
---[tab title="Topic06_Math.java" lang="java"]---
package com.cesde;

public class Topic06_Math {

    public static void explicar() {
        System.out.println("--- TEMA 6: LIBRERÍA MATH ---");

        double a = 9.0;
        double b = 2.0;

        // Operaciones Básicas
        System.out.println("Potencia (9^2): " + Math.pow(a, b));
        System.out.println("Raíz cuadrada de 9: " + Math.sqrt(a));
        System.out.println("Valor absoluto de -50: " + Math.abs(-50));

        // Máximo y Mínimo
        System.out.println("Máx (10, 20): " + Math.max(10, 20)); // 20

        // Redondeo
        System.out.println("Redondeo (3.6): " + Math.round(3.6)); // 4
        System.out.println("Ceil (Techo 3.1): " + Math.ceil(3.1)); // 4.0
        System.out.println("Floor (Piso 3.9): " + Math.floor(3.9)); // 3.0

        // Aleatorio
        double random = Math.random();
        System.out.println("Aleatorio (0.0-1.0): " + random);
        System.out.println("Aleatorio (1-100): " + (int)(random * 100 + 1));

        // Constantes
        System.out.println("PI: " + Math.PI);

        System.out.println("--------------------------------\n");
    }
}
```
