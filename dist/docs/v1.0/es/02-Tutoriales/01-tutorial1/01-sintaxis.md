---
title: "1. Sintaxis Básica"
position: 1
---

```video
---
src: "https://vimeo.com/1161295729?share=copy&fl=sv&fe=ci"
title: "Lógica de programación"
---
```

En Java, todo el código debe estar organizado dentro de clases. Aunque nuestro enfoque inicial sea la lógica procedural, siempre necesitaremos esta "cáscara" para que nuestros programas funcionen.

## Puntos Clave

```feature-list
---
items:
  - title: "Clase"
    icon: "lucide:box"
    description: "El contenedor principal. Su nombre debe coincidir **exactamente** con el nombre del archivo."
  - title: "Case Sensitive"
    icon: "lucide:type"
    description: "`Hola` y `hola` son identificadores diferentes en Java."
  - title: "Main"
    icon: "lucide:play"
    description: "El punto de entrada `public static void main(String[] args)`."
  - title: "Punto y coma"
    icon: "lucide:alert-circle"
    description: "Cada instrucción finaliza obligatoriamente con `;`."
---
```


```tabs
---[tab title="Topic01_Sintaxis.java" lang="java"]---
package com.cesde;

/**
 * TEMA 1: Sintaxis básica y estructura de un programa Java
 */
public class Topic01_Sintaxis {

    // Método estático que ejecutaremos desde el Main principal
    public static void explicar() {
        System.out.println("--- TEMA 1: SINTAXIS BÁSICA ---");

        // Esto es un comentario de una sola línea

        /*
         * Esto es un comentario
         * de múltiples líneas
         */

        System.out.println("Hola, Java!"); // Imprime texto en consola y salta de línea
        System.out.print("Esto se imprime "); // Imprime sin salto de línea
        System.out.print("en la misma línea.\n"); // \n fuerza un salto de línea

        System.out.println("La estructura básica es:");
        System.out.println("public class NombreClase {");
        System.out.println("    public static void main(String[] args) {");
        System.out.println("        // Código aquí");
        System.out.println("    }");
        System.out.println("}");

        System.out.println("--------------------------------\n");
    }
}
```
