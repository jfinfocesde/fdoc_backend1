---
title: "16. Archivos"
position: 16
---


Java ofrece el paquete `java.io` para interactuar con el sistema de archivos.

## Conceptos Básicos
- **File**: Representa la ruta al archivo.
- **FileWriter**: Para escribir texto.
- **Scanner**: Para leer texto del archivo.
- **IOException**: Es OBLIGATORIO manejar esta excepción al trabajar con archivos.

## Proceso de Escritura

```steps
### 1. Definir Archivo
Crea un objeto `File` con la ruta deseada. `new File("ruta.txt")`.

### 2. Abrir Flujo
Instancia un `FileWriter` dentro de un bloque `try`.

### 3. Escribir y Cerrar
Usa el método `.write()` para guardar texto y `.close()` para liberar el archivo.
```


```tabs
---[tab title="Topic16_Archivos.java" lang="java"]---
package com.cesde;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Scanner;

public class Topic16_Archivos {

    public static void explicar() {
        System.out.println("--- TEMA 16: ARCHIVOS ---");

        String ruta = "test.txt";
        File archivo = new File(ruta);

        // 1. Escritura
        try {
            FileWriter escritor = new FileWriter(archivo);
            escritor.write("Hola Archivo!\nEsta es una prueba.");
            escritor.close(); // ¡Muy importante cerrar!
            System.out.println("Escritura exitosa.");
        } catch (IOException e) {
            System.out.println("Error escribiendo: " + e.getMessage());
        }

        // 2. Lectura
        if (archivo.exists()) {
            try {
                Scanner lector = new Scanner(archivo);
                while (lector.hasNextLine()) {
                    System.out.println(">> " + lector.nextLine());
                }
                lector.close();
            } catch (IOException e) {
                System.out.println("Error leyendo.");
            }
        }
    }
}
```
