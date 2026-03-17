---
title: "Semana 8: Clases abstractas"
position: 9
---


Las clases abstractas en Java son una herramienta poderosa para la programación orientada a objetos, que permite definir la estructura y el comportamiento general de una clase sin tener que implementar todos sus métodos. 

**¿Qué son las clases abstractas?**

* **Plantillas incompletas:** Las clases abstractas actúan como plantillas incompletas para otras clases. No se pueden instanciar directamente (crear objetos de ellas), pero sirven como base para clases concretas que las heredan y completan su implementación.
* **Métodos abstractos:** Una clase abstracta puede contener métodos abstractos, que se declaran pero no se implementan. La responsabilidad de implementar estos métodos recae en las clases que heredan de la clase abstracta. 
* **Definición de comportamiento general:** Las clases abstractas definen un comportamiento general para un tipo de objeto, dejando la implementación específica a las clases derivadas.
* **Abstracción:** El concepto de clase abstracta promueve la abstracción, ocultando la complejidad de la implementación y mostrando únicamente la interfaz necesaria.

**Ejemplo:**

Imaginemos que estamos creando un sistema de gestión de vehículos. Podemos definir una clase abstracta llamada "Vehiculo":

```java
public abstract class Vehiculo {
  private String marca;
  private String modelo;

  public Vehiculo(String marca, String modelo) {
    this.marca = marca;
    this.modelo = modelo;
  }

  public String getMarca() {
    return marca;
  }

  public String getModelo() {
    return modelo;
  }

  // Método abstracto que define el comportamiento de moverse
  public abstract void moverse();
}
```

En este ejemplo:

* `Vehiculo` es una clase abstracta, definida con la palabra clave `abstract`.
* Tiene atributos privados para `marca` y `modelo`, y un constructor para inicializarlos.
* También tiene métodos para obtener la marca y el modelo del vehículo.
* El método `moverse()` es abstracto, ya que solo se declara (con `abstract`) pero no se implementa.

**¿Cómo se utilizan las clases abstractas?**

1. **Herencia:** Las clases concretas heredan de la clase abstracta.
2. **Implementación de métodos abstractos:** Las clases derivadas deben implementar todos los métodos abstractos de la clase padre.
3. **Especialización del comportamiento:** Cada clase derivada puede especializar el comportamiento definido en la clase abstracta.

**Ejemplo de herencia:**

```java
public class Coche extends Vehiculo {

  public Coche(String marca, String modelo) {
    super(marca, modelo);
  }

  @Override
  public void moverse() {
    System.out.println("El coche se mueve sobre ruedas");
  }
}

public class Avion extends Vehiculo {

  public Avion(String marca, String modelo) {
    super(marca, modelo);
  }

  @Override
  public void moverse() {
    System.out.println("El avión se mueve en el aire");
  }
}
```

En este ejemplo:

* `Coche` y `Avion` son clases concretas que heredan de la clase abstracta `Vehiculo`.
* Ambas clases implementan el método abstracto `moverse()` con su propia lógica específica.

**Ventajas de las clases abstractas:**

* **Reutilización de código:** Se reduce la duplicación de código al definir el comportamiento general en una sola clase abstracta.
* **Abstracción:** Se facilita la abstracción de conceptos, ocultando detalles de implementación.
* **Polimorfismo:** Permite crear diferentes tipos de objetos que comparten una misma interfaz (el método `moverse()` en este caso).

## Métodos Abstractos en Java: La Base de la Abstracción

Los métodos abstractos son la pieza clave de las clases abstractas en Java. Son como promesas de comportamiento que se declaran, pero no se implementan. La responsabilidad de definir la lógica de estos métodos recae en las clases que heredan de la clase abstracta.

**Características de los métodos abstractos:**

* **Solo declaración:** Los métodos abstractos solo se declaran, usando la palabra clave `abstract` antes de la declaración del método.
* **No tienen cuerpo:** Los métodos abstractos no tienen cuerpo de código entre llaves (`{}`).
* **Deben ser implementados:** Las clases derivadas (hijas) que heredan de la clase abstracta deben implementar todos los métodos abstractos.
* **Implementación específica:** La implementación del método abstracto puede variar entre las clases derivadas, lo que permite especializar el comportamiento.

**Ejemplo:**

```java
public abstract class Animal {

  // Método abstracto para definir el sonido que emite un animal
  public abstract void hacerSonido();

  // Otros métodos pueden ser concretos
  public void comer() {
    System.out.println("El animal está comiendo");
  }
}
```

En este ejemplo:

* `hacerSonido()` es un método abstracto, solo declarado pero no implementado.
* Las clases que hereden de `Animal` (como `Perro` o `Gato`) deberán implementar `hacerSonido()` con su propio comportamiento específico.
* El método `comer()` es concreto, ya que tiene un cuerpo definido.

**Ventajas de los métodos abstractos:**

* **Abstracción:** Permiten definir un comportamiento común sin necesidad de conocer la implementación exacta.
* **Flexibilidad:** La implementación del método abstracto puede variar entre las clases derivadas, lo que permite adaptarse a diferentes necesidades.
* **Polimorfismo:** Facilitan el polimorfismo, ya que las clases derivadas pueden responder de forma diferente al mismo método.
* **Reutilización:** Promueven la reutilización de código, al definir el comportamiento general en la clase abstracta.

**Ejemplos de uso:**

* **Interfaces gráficas:** Se pueden definir métodos abstractos para el comportamiento de botones, menus, etc. Cada tipo de botón o menu implementaría estos métodos de forma específica.
* **Sistemas de gestión:** Se pueden definir métodos abstractos para operaciones comunes en diferentes tipos de entidades (usuarios, productos, etc.).
* **Diseño de patrones:** Se pueden utilizar para implementar patrones como "Factory Method" o "Template Method".


## Ejemplo de Clase Abstracta con Métodos Abstractos: Sistema de Transporte Público

Este ejemplo ilustra cómo usar clases abstractas y métodos abstractos para modelar un sistema de transporte público en Colombia, con énfasis en la diversidad de modalidades existentes.

**Clase Abstracta:**

```java
public abstract class TransportePublico {
  private String nombreCompania;
  private String tipoTransporte;

  public TransportePublico(String nombreCompania, String tipoTransporte) {
    this.nombreCompania = nombreCompania;
    this.tipoTransporte = tipoTransporte;
  }

  public String getNombreCompania() {
    return nombreCompania;
  }

  public String getTipoTransporte() {
    return tipoTransporte;
  }

  // Métodos abstractos:
  public abstract double calcularTarifa(double distancia);
  public abstract String getMedioPago();
  public abstract String getRuta();
  public abstract int getCapacidad();

  // Método concreto:
  public void mostrarInformacion() {
    System.out.println("Nombre de la compañía: " + nombreCompania);
    System.out.println("Tipo de transporte: " + tipoTransporte);
  }
}
```

**Explicación:**

* La clase `TransportePublico` es abstracta, lo que indica que no se pueden crear instancias directas de ella.
* Tiene atributos para el nombre de la compañía y el tipo de transporte (ej. "Bus", "Metro", "TransMilenio").
* Contiene métodos abstractos:
    * `calcularTarifa(double distancia)`: calcula la tarifa de acuerdo a la distancia, pero la implementación es específica para cada tipo de transporte.
    * `getMedioPago()`: devuelve los medios de pago aceptados (ej. "Efectivo", "Tarjeta", "App").
    * `getRuta()`: devuelve la ruta que recorre el transporte (ej. "Estación A - Estación B").
    * `getCapacidad()`: devuelve la capacidad máxima de pasajeros.
* Tiene un método concreto `mostrarInformacion()` que muestra información general sobre el transporte.

**Clases Derivadas:**

```java
// Clase para buses
public class Bus extends TransportePublico {

  public Bus(String nombreCompania) {
    super(nombreCompania, "Bus");
  }

  @Override
  public double calcularTarifa(double distancia) {
    // Lógica específica para calcular la tarifa de un bus
    return 2000 + distancia * 100; // Ejemplo simple
  }

  @Override
  public String getMedioPago() {
    return "Efectivo, Tarjeta";
  }

  @Override
  public String getRuta() {
    // Implementación específica para la ruta del bus
    return "Terminal - Centro"; 
  }

  @Override
  public int getCapacidad() {
    return 50; // Capacidad típica de un bus
  }
}

// Clase para el Metro de Medellín
public class Metro extends TransportePublico {

  public Metro(String nombreCompania) {
    super(nombreCompania, "Metro");
  }

  @Override
  public double calcularTarifa(double distancia) {
    // Lógica específica para calcular la tarifa del metro
    return 2500; // Tarifa fija en el Metro de Medellín
  }

  @Override
  public String getMedioPago() {
    return "Tarjeta Cívica";
  }

  @Override
  public String getRuta() {
    // Implementación específica para la ruta del metro
    return "Estación A - Estación Z";
  }

  @Override
  public int getCapacidad() {
    return 100; // Capacidad típica de un tren de metro
  }
}
```

**Explicación:**

* Se crean clases derivadas específicas para "Bus" y "Metro".
* Cada clase implementa los métodos abstractos de `TransportePublico` con la lógica específica para ese tipo de transporte.

**Uso del Ejemplo:**

```java
public class EjemploTransporte {

  public static void main(String[] args) {
    // Crear un objeto Bus
    Bus bus = new Bus("Transmilenio");
    bus.mostrarInformacion();
    System.out.println("Tarifa: " + bus.calcularTarifa(10));

    // Crear un objeto Metro
    Metro metro = new Metro("Metro de Medellín");
    metro.mostrarInformacion();
    System.out.println("Tarifa: " + metro.calcularTarifa(5));
  }
}
```

**Beneficios de esta implementación:**

* **Abstracción:** La clase `TransportePublico` define el comportamiento general de un sistema de transporte público, sin preocuparse por detalles específicos de cada tipo de transporte.
* **Flexibilidad:** Se pueden añadir nuevos tipos de transporte (ej. "Tranvía", "Cable Aéreo") simplemente creando nuevas clases derivadas de `TransportePublico`.
* **Reutilización de código:** El código común se define en la clase abstracta, evitando la duplicación en las clases derivadas.

## Interfaces en Java: Contratos de Comportamiento

Las interfaces en Java son una herramienta fundamental de la programación orientada a objetos que define un "contrato" de comportamiento que las clases deben cumplir. A diferencia de las clases abstractas, las interfaces especifican qué métodos debe tener una clase, pero no cómo implementarlos.

**¿Qué son las interfaces?**

* **Contratos de comportamiento:** Las interfaces definen un conjunto de métodos que una clase debe implementar, sin especificar cómo.
* **Abstracción pura:** Todas las declaraciones de métodos en una interfaz son implícitamente abstractas (hasta Java 8).
* **Múltiple implementación:** Una clase puede implementar múltiples interfaces, lo que permite una forma de "herencia múltiple" de comportamiento.
* **Sin estado:** Tradicionalmente, las interfaces no pueden tener variables de instancia (solo constantes).

**Sintaxis básica:**

```java
public interface NombreInterfaz {
    // Constantes (implícitamente public, static, final)
    int CONSTANTE = 100;
    
    // Métodos abstractos (implícitamente public y abstract)
    void metodoAbstracto();
    String otroMetodo(int parametro);
}
```

**Implementación de interfaces:**

```java
public class MiClase implements NombreInterfaz {
    @Override
    public void metodoAbstracto() {
        // Implementación específica
        System.out.println("Implementación del método");
    }
    
    @Override
    public String otroMetodo(int parametro) {
        return "Resultado: " + parametro;
    }
}
```

## Características Avanzadas de las Interfaces (Java 8+)

A partir de Java 8, las interfaces han evolucionado para incluir nuevas características que las hacen más flexibles y poderosas.

**Métodos Default:**

Los métodos default permiten agregar nuevos métodos a las interfaces sin romper las clases que ya las implementan.

```java
public interface Vehiculo {
    void acelerar();
    void frenar();
    
    // Método default con implementación
    default void encender() {
        System.out.println("El vehículo se está encendiendo...");
    }
    
    default void mostrarInfo() {
        System.out.println("Este es un vehículo genérico");
    }
}
```

**Métodos Estáticos:**

Las interfaces pueden tener métodos estáticos que pertenecen a la interfaz misma.

```java
public interface CalculadoraMatematica {
    double calcular(double a, double b);
    
    // Método estático
    static double convertirARadianes(double grados) {
        return grados * Math.PI / 180;
    }
    
    static void mostrarVersion() {
        System.out.println("Calculadora v2.0");
    }
}
```

## Ejemplo Práctico: Sistema de Gestión de Empleados

Este ejemplo muestra cómo usar interfaces para crear un sistema flexible de gestión de empleados.

**Interfaces del sistema:**

```java
// Interfaz para empleados que pueden trabajar
public interface Trabajador {
    void trabajar();
    double calcularSalario();
    
    // Método default
    default void tomarDescanso() {
        System.out.println("Tomando un descanso de 15 minutos");
    }
}

// Interfaz para empleados con responsabilidades de gestión
public interface Gestor {
    void dirigirEquipo();
    void tomarDecisiones();
    int getNumeroEmpleadosACargo();
    
    // Método default
    default void organizarReunion() {
        System.out.println("Organizando reunión de equipo");
    }
}

// Interfaz para empleados que pueden capacitar
public interface Capacitador {
    void darCapacitacion(String tema);
    boolean estaCalificadoPara(String tema);
    
    // Método estático
    static void mostrarTemasPrincipales() {
        System.out.println("Temas: Java, Python, Gestión de Proyectos");
    }
}
```

**Implementaciones concretas:**

```java
// Desarrollador que solo trabaja
public class Desarrollador implements Trabajador {
    private String nombre;
    private double salarioBase;
    
    public Desarrollador(String nombre, double salarioBase) {
        this.nombre = nombre;
        this.salarioBase = salarioBase;
    }
    
    @Override
    public void trabajar() {
        System.out.println(nombre + " está programando");
    }
    
    @Override
    public double calcularSalario() {
        return salarioBase;
    }
}

// Gerente que trabaja y gestiona
public class Gerente implements Trabajador, Gestor {
    private String nombre;
    private double salarioBase;
    private int empleadosACargo;
    
    public Gerente(String nombre, double salarioBase, int empleadosACargo) {
        this.nombre = nombre;
        this.salarioBase = salarioBase;
        this.empleadosACargo = empleadosACargo;
    }
    
    @Override
    public void trabajar() {
        System.out.println(nombre + " está gestionando proyectos");
    }
    
    @Override
    public double calcularSalario() {
        return salarioBase + (empleadosACargo * 200); // Bono por gestión
    }
    
    @Override
    public void dirigirEquipo() {
        System.out.println(nombre + " está dirigiendo un equipo de " + empleadosACargo + " personas");
    }
    
    @Override
    public void tomarDecisiones() {
        System.out.println(nombre + " está tomando decisiones estratégicas");
    }
    
    @Override
    public int getNumeroEmpleadosACargo() {
        return empleadosACargo;
    }
}

// Líder técnico que trabaja, gestiona y capacita
public class LiderTecnico implements Trabajador, Gestor, Capacitador {
    private String nombre;
    private double salarioBase;
    private int empleadosACargo;
    private String[] especialidades;
    
    public LiderTecnico(String nombre, double salarioBase, int empleadosACargo, String[] especialidades) {
        this.nombre = nombre;
        this.salarioBase = salarioBase;
        this.empleadosACargo = empleadosACargo;
        this.especialidades = especialidades;
    }
    
    @Override
    public void trabajar() {
        System.out.println(nombre + " está liderando el desarrollo técnico");
    }
    
    @Override
    public double calcularSalario() {
        return salarioBase + (empleadosACargo * 300) + (especialidades.length * 500);
    }
    
    @Override
    public void dirigirEquipo() {
        System.out.println(nombre + " está dirigiendo el equipo técnico");
    }
    
    @Override
    public void tomarDecisiones() {
        System.out.println(nombre + " está tomando decisiones técnicas");
    }
    
    @Override
    public int getNumeroEmpleadosACargo() {
        return empleadosACargo;
    }
    
    @Override
    public void darCapacitacion(String tema) {
        if (estaCalificadoPara(tema)) {
            System.out.println(nombre + " está dando capacitación sobre: " + tema);
        } else {
            System.out.println(nombre + " no está calificado para enseñar: " + tema);
        }
    }
    
    @Override
    public boolean estaCalificadoPara(String tema) {
        for (String especialidad : especialidades) {
            if (especialidad.equalsIgnoreCase(tema)) {
                return true;
            }
        }
        return false;
    }
}
```

**Uso del sistema:**

```java
public class SistemaEmpleados {
    public static void main(String[] args) {
        // Crear diferentes tipos de empleados
        Desarrollador dev = new Desarrollador("Ana", 3000000);
        Gerente gerente = new Gerente("Carlos", 5000000, 5);
        LiderTecnico lider = new LiderTecnico("María", 4500000, 3, 
            new String[]{"Java", "Python", "Arquitectura"});
        
        // Polimorfismo con interfaces
        Trabajador[] empleados = {dev, gerente, lider};
        
        System.out.println("=== TRABAJO DIARIO ===");
        for (Trabajador empleado : empleados) {
            empleado.trabajar();
            System.out.println("Salario: $" + empleado.calcularSalario());
            empleado.tomarDescanso(); // Método default
            System.out.println();
        }
        
        System.out.println("=== GESTIÓN ===");
        Gestor[] gestores = {gerente, lider};
        for (Gestor gestor : gestores) {
            gestor.dirigirEquipo();
            gestor.organizarReunion(); // Método default
            System.out.println();
        }
        
        System.out.println("=== CAPACITACIÓN ===");
        if (lider instanceof Capacitador) {
            Capacitador capacitador = (Capacitador) lider;
            capacitador.darCapacitacion("Java");
            capacitador.darCapacitacion("React");
        }
        
        // Método estático
        Capacitador.mostrarTemasPrincipales();
    }
}
```

## Diferencias entre Clases Abstractas e Interfaces

| Aspecto | Clases Abstractas | Interfaces |
|---------|-------------------|------------|
| **Herencia** | Una clase puede heredar de una sola clase abstracta | Una clase puede implementar múltiples interfaces |
| **Métodos** | Pueden tener métodos abstractos y concretos | Métodos abstractos, default y estáticos (Java 8+) |
| **Variables** | Pueden tener variables de instancia | Solo constantes (public static final) |
| **Constructor** | Pueden tener constructores | No pueden tener constructores |
| **Modificadores** | Métodos pueden tener cualquier modificador | Métodos son implícitamente public |
| **Uso** | Cuando hay código común a compartir | Cuando se define un contrato de comportamiento |

## Ventajas de las Interfaces

* **Flexibilidad:** Permiten implementación múltiple, proporcionando mayor flexibilidad en el diseño.
* **Desacoplamiento:** Reducen el acoplamiento entre clases al definir contratos claros.
* **Polimorfismo:** Facilitan el polimorfismo y el intercambio de implementaciones.
* **Testabilidad:** Mejoran la testabilidad al permitir crear mocks e implementaciones de prueba.
* **Evolución:** Los métodos default permiten evolucionar las interfaces sin romper el código existente.

## Cuándo Usar Interfaces vs Clases Abstractas

**Usa Interfaces cuando:**
* Necesites implementación múltiple
* Quieras definir un contrato de comportamiento
* Las clases que implementan la interfaz no están relacionadas jerárquicamente
* Necesites máxima flexibilidad

**Usa Clases Abstractas cuando:**
* Tengas código común que compartir entre clases relacionadas
* Quieras proporcionar una implementación parcial
* Las clases están relacionadas jerárquicamente
* Necesites variables de instancia o constructores

Las interfaces son una herramienta poderosa que, combinada con clases abstractas, proporciona un sistema robusto para crear aplicaciones bien estructuradas y mantenibles en Java.





