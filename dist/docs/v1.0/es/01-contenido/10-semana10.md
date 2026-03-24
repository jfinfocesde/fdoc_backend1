---
title: "Semana 10: Interfaces en Java"
position: 10
---

# Interfaces en Java: Contratos de Comportamiento

Las **Interfaces** son una de las herramientas más potentes en la Programación Orientada a Objetos (POO). Imagina que una interfaz es como un **contrato legal**: si una clase firma ese contrato, está obligada a cumplir con todo lo que la interfaz le pida.

---

## 1. ¿Qué es una Interfaz?

En términos simples, una interfaz define **qué debe hacer** una clase, pero no **cómo lo hace**. 

*   **Abstracción Pura:** A diferencia de las clases abstractas (que pueden tener código ya hecho), las interfaces suelen contener solo declaraciones de métodos (aunque esto ha cambiado un poco en versiones recientes de Java).
*   **Contrato:** Si una clase dice que "implementa" una interfaz, Java le obliga a escribir el código de todos los métodos que esa interfaz definió.

### Diferencia clave:
- **Herencia (Clase):** Una clase **ES** un tipo de... (Un Perro es un Animal).
- **Interfaces:** Una clase **HACE** o **TIENE LA CAPACIDAD DE**... (Un Perro puede "Caminar", un Pájaro puede "Volar").

---

## 2. Sintaxis Básica

Para crear una interfaz usamos la palabra clave `interface`. Todos sus métodos son, por defecto, `public` y `abstract`.

```java
// Definición de la interfaz
public interface Reproductor {
    // Solo declaramos el método, no tiene cuerpo {}
    void reproducir();
    void pausar();
    void detener();
}

// Implementación en una clase
public class iPod implements Reproductor {
    
    @Override
    public void reproducir() {
        System.out.println("El iPod está tocando música...");
    }

    @Override
    public void pausar() {
        System.out.println("Música en pausa.");
    }

    @Override
    public void detener() {
        System.out.println("Música detenida.");
    }
}
```

---

## 3. Características Importantes

### A. Implementación Múltiple
A diferencia de la herencia normal (donde solo puedes heredar de una clase), en Java una clase puede implementar **tantas interfaces como quiera**.

```java
public class Pato implements Volador, Nadador, Caminante {
    // El pato debe implementar los métodos de las 3 interfaces
}
```

### B. Constantes
Las interfaces pueden tener variables, pero siempre son `public static final` (constantes). No puedes tener variables normales de instancia.

```java
public interface Configuracion {
    int TIEMPO_ESPERA_MAXIMO = 5000; // Es una constante
}
```

---

## 4. Evolución de las Interfaces (Java 8 y superiores)

Antes de Java 8, las interfaces solo podían tener métodos vacíos. Hoy son más flexibles:

*   **Métodos Default (`default`):** Permiten agregar código a la interfaz para que las clases no tengan que escribirlo obligatoriamente.
*   **Métodos Estáticos (`static`):** Métodos que pertenecen a la interfaz y se llaman sin necesidad de un objeto.
*   **Métodos Privados (`private`):** (Desde Java 9) Para organizar código interno dentro de la interfaz.

```java
public interface Vehiculo {
    void acelerar();

    // Método default: tiene código por defecto
    default void sonarBocina() {
        System.out.println("¡Piiiiii!");
    }

    // Método estático: utilidad general
    static boolean esValido(String placa) {
        return placa.length() == 6;
    }
}
```

---

## 5. Ejemplo Completo: Sistema de Pagos

Este ejemplo simula un sistema donde una tienda puede recibir diferentes formas de pago sin importar cuál sea el método específico.

```java
// El Contrato
public interface MetodoPago {
    void procesarPago(double monto);
    String obtenerNombre();
}

// Implementación 1: PayPal
public class PagoPayPal implements MetodoPago {
    private String correo;

    public PagoPayPal(String correo) {
        this.correo = correo;
    }

    @Override
    public void procesarPago(double monto) {
        System.out.println("Procesando $" + monto + " via PayPal para: " + correo);
    }

    @Override
    public String obtenerNombre() {
        return "PayPal";
    }
}

// Implementación 2: Tarjeta de Crédito
public class PagoTarjeta implements MetodoPago {
    private String nroTarjeta;

    public PagoTarjeta(String nroTarjeta) {
        this.nroTarjeta = nroTarjeta;
    }

    @Override
    public void procesarPago(double monto) {
        System.out.println("Cobrando $" + monto + " a la tarjeta terminada en: " + nroTarjeta.substring(12));
    }

    @Override
    public String obtenerNombre() {
        return "Tarjeta de Crédito";
    }
}

// Clase que usa la interfaz (Desacoplamiento)
public class Tienda {
    public void realizarVenta(MetodoPago metodo, double total) {
        System.out.println("--- Nueva Venta ---");
        System.out.println("Método elegido: " + metodo.obtenerNombre());
        metodo.procesarPago(total);
        System.out.println("¡Venta finalizada con éxito!\n");
    }
}
```

---

## 6. Diferencias: Interfaz vs Clase Abstracta

| Característica | Interfaz | Clase Abstracta |
| :--- | :--- | :--- |
| **Herencia** | Se pueden implementar muchas. | Solo puedes heredar de una. |
| **Variables** | Solo constantes (static final). | Puede tener variables normales. |
| **Constructor** | No tiene. | Sí tiene. |
| **Métodos** | Mayormente abstractos (default/static opcionales). | Puede tener una mezcla de cualquier tipo. |
| **Uso ideal** | Cuando quieres definir **capacidades** comunes. | Cuando quieres compartir **código base** entre parientes. |

---

## 7. Consejos para Principiantes

1.  **Nombres con Adjetivos:** Muchas interfaces terminan en "able" o "ible" (ej: `Serializable`, `Runnable`, `Caminable`), porque describen una **habilidad**.
2.  **No fuerces la herencia:** Si dos cosas no son de la misma familia pero hacen lo mismo (ej: un pájaro y un avión vuelan), usa una **interfaz**.
3.  **Desacoplamiento:** Programa orientado a interfaces, no a implementaciones. Esto permite que tu código sea fácil de cambiar en el futuro.

---

## 8. Ejemplo Medellín: Sistema SITVA (Transporte Integrado)

Para terminar, veamos cómo se aplicaría esto en nuestra ciudad. El **SITVA** (Sistema Integrado de Transporte del Valle de Aburrá) funciona bajo un mismo contrato: todos los medios de transporte deben permitirte entrar con tu tarjeta y llevarte a un destino, pero cada uno funciona de forma distinta.

```java
// El Contrato Universal del SITVA
public interface TransporteSITVA {
    void abordarConCívica();
    void mostrarRecorrido();
    double calcularTarifa();
}

// Implementación del Metro
public class MetroMedellin implements TransporteSITVA {
    @Override
    public void abordarConCívica() {
        System.out.println("Validando tarjeta en el torniquete del Metro... ¡Siga!");
    }

    @Override
    public void mostrarRecorrido() {
        System.out.println("Recorriendo la Línea A (Niquía - La Estrella)");
    }

    @Override
    public double calcularTarifa() {
        return 3210.0; // Tarifa perfil frecuente
    }
}

// Implementación del Metrocable
public class Metrocable implements TransporteSITVA {
    @Override
    public void abordarConCívica() {
        System.out.println("Validando tarjeta en la telecabina... ¡Disfrute la vista!");
    }

    @Override
    public void mostrarRecorrido() {
        System.out.println("Subiendo por la Línea K (Santo Domingo)");
    }

    @Override
    public double calcularTarifa() {
        return 0.0; // Integración gratuita desde el Metro
    }
}

// Implementación de EnCicla (¡Gratis!)
public class EnCicla implements TransporteSITVA {
    @Override
    public void abordarConCívica() {
        System.out.println("Escaneando código en la estación de bicicletas...");
    }

    @Override
    public void mostrarRecorrido() {
        System.out.println("Pedaleando por la ciclorruta de la 65");
    }

    @Override
    public double calcularTarifa() {
        return 0.0; // El sistema EnCicla es gratuito
    }
}

// Uso del polimorfismo con el transporte de Medellín
public class AppMedellin {
    public static void main(String[] args) {
        // Un usuario puede usar diferentes medios de transporte
        TransporteSITVA[] miViaje = {
            new MetroMedellin(),
            new Metrocable(),
            new EnCicla()
        };

        System.out.println("=== MI VIAJE POR MEDELLÍN ===");
        double gastoTotal = 0;

        for (TransporteSITVA transporte : miViaje) {
            transporte.abordarConCívica();
            transporte.mostrarRecorrido();
            gastoTotal += transporte.calcularTarifa();
            System.out.println("Costo tramo: $" + transporte.calcularTarifa());
            System.out.println("----------------------------");
        }

        System.out.println("Gasto total del día: $" + gastoTotal);
    }
}
```

### ¿Por qué este ejemplo es perfecto?
Porque demuestra que aunque el **Metro**, el **Metrocable** y **EnCicla** son máquinas totalmente diferentes, para el usuario (y para Java) todos "implementan" la capacidad de ser un transporte del sistema. Puedes meterlos en una misma lista y tratarlos por igual, ¡eso es el poder de las interfaces!

---
