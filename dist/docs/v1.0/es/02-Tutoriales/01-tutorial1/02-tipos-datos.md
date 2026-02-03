---
title: "2. Tipos de Datos"
position: 2
---


Java es un lenguaje de **tipado estático**, lo que significa que debemos decirle explícitamente al compilador qué tipo de información vamos a guardar en cada variable. Existen 8 tipos primitivos fundamentales.

## Clasificación

```comparison-table
---
headers:
  - "Categoría"
  - "Tipos"
  - "Uso Común"
rows:
  - ["Enteros", "byte, short, int, long", "`int` para contar, `long` para IDs grandes"]
  - ["Decimales", "float, double", "`double` es el estándar para decimales"]
  - ["Carácter", "char", "Una sola letra: 'A'"]
  - ["Lógicos", "boolean", "`true` o `false`"]
---
```

```tabs
---[tab title="Topic02_TiposDatos.java" lang="java"]---
package com.cesde;

public class Topic02_TiposDatos {

    public static void explicar() {
        System.out.println("--- TEMA 2: TIPOS DE DATOS PRIMITIVOS ---");

        // 1. Enteros
        byte numeroMuyPequeno = 127; // 8 bits (-128 a 127)
        short numeroPequeno = 32000; // 16 bits
        int numeroEntero = 2147483647; // 32 bits (El más usado)
        long numeroLargo = 9223372036854775807L; // 64 bits (Requiere sufijo L)

        // 2. Decimales (Punto flotante)
        float decimalCorto = 3.1416f; // 32 bits (Requiere sufijo f)
        double decimalLargo = 3.14159265359; // 64 bits (Estándar)

        // 3. Carácter
        char letra = 'A'; // Un solo carácter entre comillas simples
        char codigoAscii = 65; // También acepta el valor numérico ASCII

        // 4. Booleano
        boolean esVerdadero = true;
        boolean esFalso = false;

        System.out.println("Int: " + numeroEntero);
        System.out.println("Double: " + decimalLargo);
        System.out.println("Char: " + letra);
        System.out.println("Boolean: " + esVerdadero);

        System.out.println("--------------------------------\n");
    }
}
```
