---
title: "11. Métodos (Funciones)"
position: 11
---


Un método es una porción de código reutilizable que realiza una tarea específica. Ayudan a dividir un programa complejo en partes pequeñas y manejables.

## Sintaxis
`[Modificador] [static] [Tipo Retorno] [Nombre]( [Parámetros] ) { ... }`

- **void**: El método no devuelve nada.
- **static**: Pertenece a la clase, no requiere `new` para usarse.

```tabs
---[tab title="Topic11_Metodos.java" lang="java"]---
package com.cesde;

public class Topic11_Metodos {

    public static void explicar() {
        System.out.println("--- TEMA 11: MÉTODOS ESTÁTICOS ---");

        System.out.println("1. Llamada simple:");
        saludar();

        System.out.println("2. Reutilización:");
        imprimirSeparador();
        saludar();
        imprimirSeparador();
    }

    // Definición de un método simple
    public static void saludar() {
        System.out.println("   ¡Hola desde el método saludar!");
    }

    public static void imprimirSeparador() {
        System.out.println("   .......................");
    }
}
```
