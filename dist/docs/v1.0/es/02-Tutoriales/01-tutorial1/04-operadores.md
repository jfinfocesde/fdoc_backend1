---
title: "4. Operadores"
position: 4
---


Los operadores son símbolos especiales que realizan operaciones específicas en uno, dos o tres operandos, y luego devuelven un resultado.

## Categorías Principales

1.  **Aritméticos**: Matemáticas básicas (+, -, *, /, %).
2.  **Asignación**: Guardar valores (=, +=, -=).
3.  **Relacionales**: Comparar (`true`/`false`).
4.  **Lógicos**: Combinar condiciones (AND, OR, NOT).


```quiz
---
questions:
  - text: "¿Cuál es el resultado de `10 % 3`?"
    choices:
      - "3"
      - "1"
      - "3.33"
    answer: "1"
  - text: "¿Qué operador se usa para AND lógico?"
    choices:
      - "&"
      - "&&"
      - "||"
    answer: "&&"
  - text: "Si x=5, ¿cuánto vale x después de `x++`?"
    choices:
      - "5"
      - "6"
      - "4"
    answer: "6"
---
```

```tabs
---[tab title="Topic04_Operadores.java" lang="java"]---
package com.cesde;

public class Topic04_Operadores {

    public static void explicar() {
        System.out.println("--- TEMA 4: OPERADORES ---");

        int a = 10;
        int b = 3;

        // 1. Aritméticos
        System.out.println("Suma: " + (a + b));
        System.out.println("División (entera): " + (a / b)); // 10 / 3 = 3
        System.out.println("Módulo (residuo): " + (a % b)); // 10 % 3 = 1

        // 2. Asignación Compuesta
        int x = 5;
        x += 2; // x = x + 2 (7)
        System.out.println("Asignación compuesta (+=): " + x);
        x++; // x = 8 (Incremento)

        // 3. Relacionales
        System.out.println("10 > 3: " + (a > b));
        System.out.println("10 == 3: " + (a == b));

        // 4. Lógicos
        boolean mayorDeEdad = true;
        boolean tieneIdentificacion = false;

        // AND (&&): Ambas true
        System.out.println("Entra (AND): " + (mayorDeEdad && tieneIdentificacion));

        // OR (||): Al menos una true
        System.out.println("Entra (OR): " + (mayorDeEdad || tieneIdentificacion));

        // NOT (!): Invertir
        System.out.println("Invertido (!): " + (!tieneIdentificacion));

        System.out.println("--------------------------------\n");
    }
}
```

