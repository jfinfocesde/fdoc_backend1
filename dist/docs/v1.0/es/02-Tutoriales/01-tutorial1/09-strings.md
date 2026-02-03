---
title: "9. Strings"
position: 9
---


En Java, `String` es un Objeto, lo que significa que tiene métodos poderosos para la manipulación de texto.
La clase `StringBuilder` se utiliza para construir cadenas eficientemente cuando hay muchas modificaciones (concatenaciones).

```comparison-table
---
headers:
  - "Característica"
  - "String"
  - "StringBuilder"
rows:
  - ["Mutabilidad", "Inmutable (No cambia)", "Mutable (Modificable)"]
  - ["Rendimiento", "Lento en muchas concatenaciones", "Rápido y eficiente"]
  - ["Uso", "Textos fijos, Mensajes", "Bucles, Construcción dinámica"]
---
```


```tabs
---[tab title="Topic09_Strings.java" lang="java"]---
package com.cesde;

public class Topic09_Strings {

    public static void explicar() {
        System.out.println("--- TEMA 9: STRINGS ---");

        String texto = "  Hola Mundo Java  ";

        // Métodos Utiles
        String limpio = texto.trim();
        System.out.println("Limpio: '" + limpio + "'");
        
        System.out.println("Mayúsculas: " + limpio.toUpperCase());
        System.out.println("Contiene 'Mundo': " + limpio.contains("Mundo"));

        // Comparación (IMPORTANTE)
        String a = "hola";
        String b = "HOLA";
        // NUNCA usar '==' para comparar contenido de Strings
        System.out.println("Iguales (IgnoreCase): " + a.equalsIgnoreCase(b));

        // StringBuilder (Para concatenación masiva)
        StringBuilder sb = new StringBuilder();
        sb.append("Paso 1");
        sb.append(" -> Paso 2");
        System.out.println("Builder: " + sb.toString());

        System.out.println("--------------------------------\n");
    }
}
```
