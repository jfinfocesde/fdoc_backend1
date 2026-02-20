---
title: "Semana 3: Tipos de Datos y Transformación de la Información"
description: "Guía profunda y completa sobre los cimientos de la memoria en Java: datos primitivos, el poder de las clases envolventes (Wrappers), y las técnicas fundamentales de Casting y Parseo."
position: 3
category: "fundamentos"
difficulty: "beginner"
tags: ["java", "poo", "primitivos", "wrappers", "casting", "parseo", "autoboxing"]
date: "2026-02-09"
last_updated: "2026-02-20"
author: "Cesde Teacher"
---

+++hero-section
---
title: "El ADN de Java: Primitivos, Wrappers y Conversiones"
subtitle: "Para construir software de calidad comercial, necesitas dominar cómo se almacena, trata y transforma cada byte de tu información."
backgroundImage: "https://images.unsplash.com/photo-1555949963-aa79dcee981c?q=80&w=2070"
overlayOpacity: 0.7
buttons:
  - text: "Comenzar Lectura"
    url: "#1-los-cimientos-tipos-de-datos-primitivos"
    variant: "primary"
    icon: "BookOpenIcon"
  - text: "Documentación Oracle"
    url: "https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html"
    variant: "secondary"
---
+++

Bienvenidos a la tercera semana. En nuestro camino hacia el dominio de la programación orientada a objetos (POO) y de Java como lenguaje profesional, es indispensable detenernos en cómo gestionamos la información a un nivel fundamental. 

En esta guía extensa exploraremos tres pilares críticos:
1. **Los Datos Primitivos**: La forma más pura, rápida y eficiente de manejar valores en memoria.
2. **Las Clases Envolventes (Wrapper Classes)**: La técnica de Java para convertir lo primitivo en objetos reales, permitiéndonos interactuar con arquitecturas modernas.
3. **Casting y Parseo**: Cómo forzar y traducir la información para que fluya de un tipo de dato a otro sin romper nuestras aplicaciones.

---

## 1. Los Cimientos: Tipos de Datos Primitivos

Java es un lenguaje tipado estáticamente, lo que significa que el compilador necesita saber qué tipo de dato tendrá cada variable desde el momento en que la declaras. 

A diferencia de muchos lenguajes modernos (como JavaScript o Python), en Java **no todo es un objeto**. Para realizar operaciones a extrema velocidad y ahorrar memoria RAM, Java introdujo los **tipos primitivos**. Estos datos se guardan estrictamente en la memoria *Stack* (una memoria de acceso ultra rápido y tamaño fijo), no tienen métodos asociados (`.algo()`) y **nunca pueden ser nulos (`null`)**.

Java cuenta con exactamente **8 tipos primitivos**, divididos en 4 categorías:

### A. Números Enteros
No tienen parte decimal. Elegir entre ellos depende exclusivamente de cuánta memoria quieras optimizar y qué tan grande será el número que necesitas almacenar.

*   `byte`: Ocupa solo 1 byte (8 bits). Su rango va de **-128 a 127**. Se usa en sistemas empotrados o procesamiento de archivos a muy bajo nivel.
*   `short`: Ocupa 2 bytes (16 bits). Su rango va de **-32,768 a 32,767**. Muy poco uso en la cotidianidad empresarial.
*   `int`: Ocupa 4 bytes (32 bits). Rango de **-2 mil millones a 2 mil millones**. Es el **estándar absoluto** para contadores, edades, identificadores básicos, etc.
*   `long`: Ocupa 8 bytes (64 bits). Rango inmenso. OBLIGATORIO usarlo cuando manejamos IDs de bases de datos de grandes plataformas, milisegundos de tiempo o distancias en el espacio. **Nota vital:** Debes añadir una `L` al final de su valor: `long habitantes = 8000000000L;`.

### B. Números Decimales (Punto Flotante)
Manejan fracciones y decimales. En computación, el cálculo decimal siempre tiene un pequeño margen de error interno debido a limitaciones arquitectónicas.

*   `float`: Ocupa 4 bytes. Precisión de hasta 7 cifras decimales. Debes colocar una `f` al final: `float temperatura = 36.5f;`.
*   `double`: Ocupa 8 bytes. Precisión de hasta 15 cifras decimales. Es el **estándar** en Java para operaciones matemáticas generales y cálculos científicos: `double precio = 19.99;`.

### C. Caracteres
*   `char`: Ocupa 2 bytes. Almacena **un único símbolo Unicode** (soporta emojis, letras, números, símbolos chinos). Solo permite comillas simples (`' '`), nunca comillas dobles (eso es para los Strings): `char opcion = 'A';`.

### D. Lógicos
*   `boolean`: Ocupa 1 bit lógicamente (aunque la máquina virtual lo maneje diferente según la arquitectura). Solo tiene dos universos posibles: `true` (verdadero) o `false` (falso). Es el árbitro de tus bucles (`while`) y condiciones (`if`).

---

## 2. La Evolución: Clases Envolventes (Wrapper Classes)

Si los primitivos son rápidos y eficientes, ¿por qué necesitamos algo más? El problema surge cuando Java interactúa con el mundo exterior o con sus propias características avanzadas. 

Por ejemplo:
1. Las Listas dinámicas en Java (`ArrayList`) **no aceptan tipos primitivos**. No puedes tener un `ArrayList<int>`.
2. Las bases de datos pueden devolver valores vacíos (`NULL`). Si mi base de datos me dice que la edad de un usuario es nula, no puedo guardarlo en la variable primitiva `int edad;` en Java, porque un `int` primitivo jamás puede ser nulo, por defecto vale `0`. (¡Cero y nulo no significan lo mismo en programación!).

La solución a esto son las **Clases Envolventes (Wrappers)**. Java toma el humilde valor primitivo, lo mete dentro de una 'caja' (lo envuelve) y lo transforma en un verdadero Objeto almacenado en la memoria *Heap*. Ahora sí, ¡ya tiene métodos, ya puede ser nulo, ya entra en las listas!

### Comparativa: La Metamorfosis

```comparison-table
---
headers:
  - "Tipo Primitivo"
  - { text: "Clase Wrapper Correspondiente", highlight: true }
  - "Características de la Clase Envolvente"
rows:
  - ["byte", "Byte", "Al ser objeto, su valor por defecto si no se inicializa es null."]
  - ["short", "Short", "Igual que Byte."]
  - ["int", "Integer", "¡Ojo! Cambia la palabra de int a Integer. Muy usado en List<Integer>."]
  - ["long", "Long", "Permite manejar IDs nulos traídos de la BD."]
  - ["float", "Float", "Proporciona constantes como Float.MAX_VALUE."]
  - ["double", "Double", "Proporciona métodos útiles de conversión matemática."]
  - ["char", "Character", "¡Ojo! Cambia a Character. Métodos útiles como Character.isDigit('1')."]
  - ["boolean", "Boolean", "Puede ser true, false o null (Lógica ternaria en BD)."]
---
```

### Autoboxing y Unboxing: Magia Tras Bambalinas

Antes de Java 5, meter y sacar el valor de su "caja" objeto era un dolor de cabeza manual. Hoy en día, Java utiliza un sistema automático llamado *Autoboxing* (Empaque automático) y *Unboxing* (Desempaque automático).

```java
// AUTOBOXING: El primitivo 10 se envuelve automáticamente en un Objeto Integer.
Integer numeroObjeto = 10; 

// UNBOXING: El objeto se desenvuelve para ser matemático puro de nuevo.
int primitivoPuro = numeroObjeto; 

// Uso en la vida real (Colecciones):
List<Integer> edades = new ArrayList<>();
edades.add(25); // Magia: 25 es un primitivo(int), pero Java le hace Autoboxing a Integer en secreto antes de guardarlo.
```

---

## 3. Transformación: Casting y Parseo de Datos

En el mundo real, los datos nunca te llegan con la etiqueta perfecta. A veces un descuento llega como un número entero (`int 15`) pero el sistema contable exige un decimal (`double 15.0`). Otras veces, un usuario teclea su edad (`"25"`) en un formulario, pero para el código Java eso es simplemente una cadena de Texto (`String`) con la que no puedes sumar ni restar. 

Para resolver estos choques de tipado, usamos dos herramientas fundamentales: **El Casting** y **El Parseo**. Es vital no confundirlos: sus usos son completamente distintos.

### 3.1 Casting (Ajustar de un numérico a otro)

El **Casteo o Conversión de Tipos** ocurre exclusivamente entre tipos de datos compatibles por naturaleza (por ejemplo, primitivos numéricos entre sí). Consiste en enseñarle a Java que trate un tipo de dato como si fuera de otra capacidad.

#### A. Casteo Implícito (Ensanchamiento / Widening)
Ocurre automáticamente sin que el programador haga nada. Se da cuando pasamos de un tipo de dato 'pequeño' (que ocupa menos bytes en memoria) a un tipo de dato 'más grande'. Es **100% seguro** y no hay riesgo de perder información.

```java
int balas = 50;           // La 'caja' de 32 bits tiene el valor 50
double nivelBateria = balas; // La 'caja' doble de 64 bits engulle al 50. 
// nivelBateria ahora vale 50.0 automáticamente. No hay errores de compilación.
```

#### B. Casteo Explícito (Estrechamiento / Narrowing)
Esto es forzar a la máquina. Intentas meter un dato de mayor capacidad (o con decimales) en una variable de menor capacidad. **¡Es peligroso!** Existe un riesgo altísimo de **truncamiento** (pérdida de la parte decimal) o de **desbordamiento** (overflow).

Como es peligroso, Java no lo hace automático; te obliga a tomar responsabilidad de la orden escribiendo entre paréntesis el tipo objetivo: `(nuevoTipo)`.

```java
double notaFinal = 4.8;
// int notaTrucada = notaFinal; // ❌ ERROR en tiempo de compilación. "Possible loss of precision".

// CASTEO EXPLÍCITO: Le digo a Java: "Sé lo que hago, forzaló y recorta las esquinas"
int notaTruncada = (int) notaFinal; 

System.out.println(notaTruncada); // Muestra 4. Perdiste el 0.8 en el proceso. NO redondea, RECORTA.
```

### 3.2 Parseo (Traducir a partir de un String de Texto)

Si intentas hacer un "Casting" de un String a un int (`int e = (int) "25";`) Java se va a quejar radicalmente. "25" en String son simplemente los dibujos de los caracteres '2' y '5' juntos y concatenados, no poseen un valor o lógica aritmética.

Para extraer el verdadero valor numérico atrapado dentro de un texto, debemos convocar el poder de las **Clases Envolventes (Wrappers)** usando sus funciones estáticas de conversión llamadas **`parse...()`**.

```tabs
---[tab title="Parsear a Números" lang="java"]---
public class DemostracionParseo {
    public static void main(String[] args) {
        String inputUsuario = "2026";
        String precioSistema = "9.99";
        
        // Usamos los Wrappers como traductores:
        int anio = Integer.parseInt(inputUsuario);
        double costo = Double.parseDouble(precioSistema);
        
        System.out.println("En 10 años será: " + (anio + 10)); // 2036
        System.out.println("Costo con envío: " + (costo + 2.0)); // 11.99
    }
}
---[tab title="Parsear a Booleano" lang="java"]---
public class LogicaParseo {
    public static void main(String[] args) {
        String estadoInterruptor = "true";
        String trampa = "verdadero";
        
        boolean isEncendido = Boolean.parseBoolean(estadoInterruptor); // true
        
        // IMPORTANTE: Boolean.parseBoolean() solo devuelve 'true' 
        // si lee la palabra exacta "true" (ignorando may/minúsculas). 
        // Cualquier otra palabra del universo devolverá false.
        boolean esReal = Boolean.parseBoolean(trampa); // false!!
        
        System.out.println(isEncendido);
    }
}
---[tab title="La Trampa: Excepciones" lang="java"]---
public class CuidadoParseo {
    public static void main(String[] args) {
        String pesoTexto = "setenta"; // El string no es numérico estructurado
        
        // ¡BOMBA! Esto compila, pero al ejecutarse la aplicación crasheará por completo.
        // Ocurrirá un NumberFormatException (Excepción de Formato de Número).
        int peso = Integer.parseInt(pesoTexto); 
        
        // En aplicaciones reales empresariales, SIEMPRE debemos envolver
        // estas lecturas de Parseo en bloques try-catch que atraparemos en el futuro.
    }
}
---[tab title="Ingeniería Inversa" lang="java"]---
public class VolverAString {
    public static void main(String[] args) {
        // ¿Qué pasa si tengo un double primitivo y necesito enviarlo a React
        // o pintarlo en un PDF donde todo debe ser Texto (String)?
        
        double saldoDolares = 50000.5;
        
        // MÉTODO OFICIAL
        String vistaSaldo = String.valueOf(saldoDolares);
        
        // MÉTODO RÁPIDO Y HACKER (Concatenación de cadena vacía):
        // En Java, sumar (+) cualquier cosa a un string vacío, convierte
        // esa 'cosa' a String inmediatamente.
        String vistaTrampa = "" + saldoDolares; 
    }
}
```

---

+++quiz
---
questions:
  - text: "¿Qué sucederá matemáticamente si ejecutamos la instrucción `int a = (int) 7.99;` en Java?"
    choices:
      - a será igual a 7 porque el casting pierde la parte decimal y en ningún caso redondea automáticamente.
      - a será igual a 8 porque Java aplicará un redondeo científico cercano por defecto.
      - Habrá un error en tiempo de compilación que no te permitirá iniciar el programa.
      - Guardará 7.99 temporalmente pero no te dejará usar la variable a matemáticamente.
    answer: "a será igual a 7 porque el casting pierde la parte decimal y en ningún caso redondea automáticamente."
  - text: "¿Qué método utilizas si estás leyendo un archivo de Excel y obtienes la cadena `\"false\"`, pero lo tú que necesitas para tu ciclo if en Java es evaluar el primitivo booleano como tal?"
    choices:
      - (boolean) \"false\";
      - Boolean.parseBoolean(\"false\");
      - String.toBool(\"false\");
      - Integer.parseBoolean(\"false\");
    answer: "Boolean.parseBoolean(\"false\");"
  - text: "¿Cuál es el propósito principal y la mayor ventaja de usar el Wrapper `Integer` en vez del primitivo `int` en una aplicación comercial?"
    choices:
      - Acelerar el procesamiento de ciclos iterativos *for* y *while* al acceder de forma directa en el procesador gráfico a operaciones de Stack.
      - Poder asignarles nulo (`null`) en caso de representar variables que provengan vacías desde bases de datos externas y poder usarlos dentro de Estructuras Dinámicas como Colecciones o Listas (`List<Integer>`).
      - Minimizar el uso general de la memoria física de la máquina y maximizar el *Garbage Collector*.
      - Ninguna ventaja. Ya que Java 9 está prohibido utilizar Integer en pos de `int`.
    answer: "Poder asignarles nulo (`null`) en caso de representar variables que provengan vacías desde bases de datos externas y poder usarlos dentro de Estructuras Dinámicas como Colecciones o Listas (`List<Integer>`)."
---
+++

```admonition
---
type: tip
title: "Reto Laboratorio: La Terminal del Cajero Bancario"
---
Vas a simular el proceso de fondo de un cajero que procesa dinero con variables de texto:

1. El sistema lee un monto depositado por el usuario con texto plano: `String depositoTexto = "250.75";`.
2. Necesitas que tu programa sume este depósito a un saldo base: `double saldoCuenta = 1000.0;`. Por lo tanto, extrae limpiamente el número del String mediante un **Parseo a Wrapper** correcto.
3. Ahora suma el número depositado más tu saldo real e imprímelo en la terminal.
4. El cajero, por razones de política de seguridad del banco por fraude tributario en depósitos internacionales, te indica que debe forzosamente descartar (eliminar) los valores en centavos para registros fiscales internos del log: Genera una última variable de nombre `int saldoFiscal`, toma el monto total actual de la cuenta, realízale un **Casting Explícito (Narrowing)** a tipo de dato entero para forzar la amputación de los decimales, e imprímelo al final.
```
