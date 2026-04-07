---
title: "Semana 9: Polimorfismo en Java"
description: "Domina el arte de las 'muchas formas'. Aprende cómo el polimorfismo permite que un solo contrato gestione múltiples comportamientos, haciendo tu código infinitamente flexible y escalable."
position: 9
---

+++hero-section
---
title: "Polimorfismo en Java"
subtitle: "El superpoder de la POO: un mismo mensaje, mil respuestas diferentes. Aprende a escribir código que se adapta al futuro sin romperse."
backgroundImage: "https://images.unsplash.com/photo-1550751827-4bd374c3f58b?q=80&w=2070"
overlayOpacity: 0.75
buttons:
  - text: "Explorar Conceptos"
    url: "#1-que-es-el-polimorfismo"
    variant: "primary"
    icon: "CubeTransparentIcon"
  - text: "Ver Ejemplos SITVA"
    url: "#ejemplo-sitva"
    variant: "secondary"
    icon: "RocketLaunchIcon"
---
+++

El polimorfismo es, posiblemente, el concepto más elegante y potente de la POO. Mientras que la herencia nos permite reutilizar código, el polimorfismo nos permite **desacoplarnos** de los detalles y programar pensando en **contratos**.

## ¿Por qué lo necesitamos?

+++stat-cards
---
columns: 4
items:
  - icon: "AdjustmentsVerticalIcon"
    value: "Flex"
    label: "Código adaptable"
    color: "purple"
  - icon: "ArrowsRightLeftIcon"
    value: "Swap"
    label: "Intercambio de piezas"
    color: "blue"
  - icon: "LinkIcon"
    value: "Decoupled"
    label: "Menos dependencia"
    color: "teal"
  - icon: "ArrowPathRoundedSquareIcon"
    value: "DRY"
    label: "Reutilización total"
    color: "green"
---
+++

---

## 1. ¿Qué es el Polimorfismo?

La palabra viene del griego: *Poli* (muchos) y *Morfos* (formas). En Java, es la capacidad de un objeto de tomar diferentes formas dependiendo del contexto.

Más formalmente: **Es la capacidad de enviar el mismo mensaje a diferentes tipos de objetos, y que cada uno responda de acuerdo a su propia naturaleza.**

### El ejemplo de la vida real
Imagina el comando **"¡Toca música!"**.
- Si se lo dices a un **Pianista**, usará un piano.
- Si se lo dices a un **Guitarrista**, usará una guitarra.
- Si se lo dices a un **Director de Orquesta**, usará su batuta.

El mensaje es el mismo (**método**), pero la implementación varía (**polimorfismo**).

---

## 2. Tipos de Polimorfismo

Java gestiona el polimorfismo de dos maneras principales, dependiendo de **cuándo** se resuelve la acción:

+++tabs
---[tab title="Estático (Sobrecarga)" lang="java"]---
// Se resuelve en tiempo de COMPILACIÓN.
// El mismo nombre de método, pero diferentes parámetros.

public class Calculadora {
    public int sumar(int a, int b) { return a + b; }
    
    public double sumar(double a, double b) { return a + b; }
    
    public int sumar(int a, int b, int c) { return a + b + c; }
}

// Java sabe exactamente cuál llamar mirando los argumentos.
---[tab title="Dinámico (Sobrescritura)" lang="java"]---
// Se resuelve en tiempo de EJECUCIÓN (Runtime).
// Es el polimorfismo "clásico" basado en herencia.

public class Animal {
    public void hacerSonido() { System.out.println("Sonido..."); }
}

public class Perro extends Animal {
    @Override
    public void hacerSonido() { System.out.println("¡Guau!"); }
}

// Aquí está la magia:
Animal miMascota = new Perro(); // Upcasting
miMascota.hacerSonido(); // Imprime "¡Guau!" porque Java mira el objeto real (Perro)
---
+++

---

## 3. Upcasting y Downcasting

Para que el polimorfismo funcione, Java permite movernos a través de la jerarquía de herencia:

### Upcasting (Hacia arriba) ⬆️
Convertir una referencia de una clase hija a una clase padre. Es **automático y seguro**, porque un `Perro` siempre es un `Animal`.

```java
Animal a = new Perro(); // Correcto y automático
```

### Downcasting (Hacia abajo) ⬇️
Convertir una referencia de una clase padre a una clase hija. **No es automático** y requiere un *cast* explícito. Solo es seguro si el objeto realmente es del tipo al que intentas convertirlo.

```java
Animal a = new Perro();
// ... más tarde ...
Perro p = (Perro) a; // Downcasting explícito
p.ladrar(); // Ahora podemos acceder a métodos específicos de Perro
```

+++admonition
---
type: warning
title: "El operador instanceof"
---
Antes de hacer downcasting, siempre usa `instanceof` para evitar errores de ejecución (`ClassCastException`).
```java
if (a instanceof Perro) {
    Perro p = (Perro) a;
    p.ladrar();
}
```
+++

---

## 4. Ejemplo Maestro: El Sistema SITVA 🚇

Volvamos a Medellín. El sistema de transporte es el mejor ejemplo de polimorfismo. Todos son `Transporte`, pero cada uno se mueve distinto.

+++tabs
---[tab title="1. Dominio" lang="java"]---
public abstract class Transporte {
    private String nombre;
    
    public Transporte(String nombre) { this.nombre = nombre; }
    public String getNombre() { return nombre; }
    
    // Método abstracto: el "mensaje" polimórfico
    public abstract void desplazarse();
}

public class Metro extends Transporte {
    public Metro() { super("Metro de Medellín"); }
    @Override
    public void desplazarse() {
        System.out.println("El Metro se desliza sobre rieles férreos. 🚇");
    }
}

public class Metrocable extends Transporte {
    public Metrocable() { super("Metrocable"); }
    @Override
    public void desplazarse() {
        System.out.println("El Metrocable vuela sobre las montañas por cables. 🚠");
    }
}

public class Tranvia extends Transporte {
    public Tranvia() { super("Tranvía de Ayacucho"); }
    @Override
    public void desplazarse() {
        System.out.println("El Tranvía rueda con neumáticos y guía central. 🚃");
    }
}
---[tab title="2. Ejecución" lang="java"]---
public class SistemaTransporte {
    public static void main(String[] args) {
        // POLIMORFISMO: Una lista de 'Padres' que guarda 'Hijos'
        Transporte[] flotaSitva = {
            new Metro(),
            new Metrocable(),
            new Tranvia(),
            new Metro()
        };

        System.out.println("=== OPERACIÓN SITVA INICIADA ===");
        
        for (Transporte t : flotaSitva) {
            System.out.print(t.getNombre() + ": ");
            // Aquí ocurre el polimorfismo dinámico:
            t.desplazarse(); 
        }
    }
}
---
+++

### Ventaja Crucial
Si mañana Medellín inaugura el **Metro de la 80**, solo creamos una nueva clase `Metro80` que extienda de `Transporte`. ¡El código del `main` (el bucle) **no cambia nada**! Eso es escalabilidad.

---

## 🏫 Actividad — Sistema de Notificaciones

Imagina que estás desarrollando una App móvil. Tu sistema debe enviar notificaciones por diferentes canales, pero no quieres que el núcleo de tu app sepa los detalles técnicos de cada canal.

### El Reto
1.  Crea una clase abstracta `Notificacion` con un método `enviar(String mensaje)`.
2.  Crea tres subclases: `EmailNotificacion`, `SMSNotificacion` y `PushNotificacion`.
3.  En el `main`, crea un `ArrayList<Notificacion>`.
4.  Agrega al menos una de cada tipo.
5.  Recorre la lista y envía el mensaje: *"¡Tienes una nueva actualización disponible!"*.

+++admonition
---
type: tip
title: "Piensa en grande"
---
¿Qué pasaría si el usuario tiene desactivados los SMS? Con polimorfismo, podrías simplemente no agregar el `SMSNotificacion` a la lista y el resto del sistema seguiría funcionando perfectamente.
+++

---

## Resumen: ¿Cuándo usar Polimorfismo?

+++comparison-table
---
headers:
  - "Si quieres..."
  - "¿Usar Polimorfismo?"
  - "Razón"
rows:
  - ["Tratar diferentes objetos como uno solo", "✅ SÍ", "Permite listas genéricas (List<Vehiculo>)."]
  - ["Añadir nuevas clases sin romper el código viejo", "✅ SÍ", "Principio Open/Closed (Abierto a extensión)."]
  - ["Diferenciar lógica compleja de los objetos", "✅ SÍ", "Mantiene el 'main' limpio de IFs y SWITCHes."]
  - ["Solo repetir código de una clase padre", "❌ NO", "Eso es simplemente Herencia básica."]
---
+++

El polimorfismo es lo que convierte a un programador de Java en un **Arquitecto de Software**. ¡Sigue practicando!

