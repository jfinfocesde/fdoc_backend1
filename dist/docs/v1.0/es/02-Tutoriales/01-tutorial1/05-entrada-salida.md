---
title: "5. Entrada y Salida"
position: 5
---


Interactuar con el usuario es esencial. En aplicaciones de consola, usamos `System.out` para escribir y la clase `Scanner` para leer del teclado.

## Receta para Leer Datos

```steps
### 1. Importar Scanner
`import java.util.Scanner;`

### 2. Crear Objeto
`Scanner sc = new Scanner(System.in);`

### 3. Leer y Limpiar
Usa `nextInt()` para números y recuerda `nextLine()` para consumir el enter sobrante.
```


## Scanner y el "Buffer"
Un error común al leer números y luego texto es que el `enter` queda "flotando" en el buffer.
> [!WARNING]
> Siempre haz un `sc.nextLine()` extra después de leer un número si vas a leer texto después.

```tabs
---[tab title="Topic05_EntradaSalida.java" lang="java"]---
package com.cesde;
import java.util.Scanner;

public class Topic05_EntradaSalida {

    public static void explicar() {
        System.out.println("--- TEMA 5: ENTRADA Y SALIDA ---");

        // Salidas
        System.out.print("Print sin salto. ");
        System.out.println("Println con salto.");
        System.out.printf("Printf formateado: %.2f\n", 3.14159);

        // Entradas (Scanner)
        // Scanner sc = new Scanner(System.in);
        
        /*
        System.out.print("Ingresa edad: ");
        int edad = sc.nextInt();
        
        // LIMPIEZA DEL BUFFER
        sc.nextLine(); 
        
        System.out.print("Ingresa nombre: ");
        String nombre = sc.nextLine();
        */

        System.out.println("Recuerda limpiar el buffer tras leer números.");
        System.out.println("--------------------------------\n");
    }
}
```
