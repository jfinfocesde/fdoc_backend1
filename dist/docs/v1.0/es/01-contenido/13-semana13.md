---
title: "Semana 13: Gestores de Dependencias en Java"
position: 13
---

# Gestores de Dependencias en Java: Maven y Gradle

En el mundo real de la programación, rara vez escribimos todo el código desde cero. A menudo utilizamos **librerías** y **frameworks** creados por otros desarrolladores para resolver problemas comunes (como conectarse a una base de datos, crear una interfaz gráfica o consumir una API REST). A estos componentes externos los llamamos **dependencias**.

Imagina que estás construyendo una casa. No fabricas tus propios ladrillos, ni fundes tu propio acero; los compras a proveedores. Los gestores de dependencias son como los camiones de reparto que traen exactamente los materiales que necesitas, en las versiones correctas, directo a tu obra.

---

## 1. ¿Qué es un Gestor de Dependencias?

Un gestor de dependencias es una herramienta que automatiza el proceso de:
1. **Descargar librerías:** Busca en internet (en repositorios centrales) las librerías que tu proyecto necesita y las descarga.
2. **Gestionar versiones:** Asegura que uses la versión correcta de cada librería, evitando conflictos.
3. **Dependencias transitivas:** Si la librería "A" que necesitas depende a su vez de la librería "B", el gestor descargará ambas automáticamente.
4. **Compilar y empaquetar:** Transforma tu código fuente y las librerías en un programa ejecutable (como un archivo `.jar`).

En el ecosistema Java, los dos gestores más populares son **Maven** y **Gradle**.

---

## 2. Apache Maven

Maven es el gestor de dependencias más tradicional y utilizado en Java. Utiliza un archivo de configuración llamado `pom.xml` (Project Object Model) basado en XML.

### El Archivo `pom.xml`

Es el corazón de cualquier proyecto Maven. Aquí defines la información de tu proyecto y qué librerías necesitas.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>

    <!-- 1. Identificación de tu proyecto -->
    <groupId>com.miempresa</groupId>       <!-- Organización -->
    <artifactId>mi-aplicacion</artifactId>  <!-- Nombre del proyecto -->
    <version>1.0-SNAPSHOT</version>         <!-- Versión actual -->

    <!-- 2. Configuración de Java -->
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <!-- 3. Lista de Dependencias -->
    <dependencies>
        <!-- Ejemplo: Librería para convertir objetos a JSON (Gson) -->
        <dependency>
            <groupId>com.google.code.gson</groupId>
            <artifactId>gson</artifactId>
            <version>2.10.1</version>
        </dependency>
    </dependencies>
</project>
```

### Ciclo de vida de Maven (Comandos principales)
Maven divide la construcción en "fases". Al ejecutar una fase, se ejecutan todas las anteriores.
* `mvn clean`: Borra los archivos compilados de ejecuciones anteriores (limpia el proyecto).
* `mvn compile`: Compila tu código fuente Java.
* `mvn test`: Ejecuta las pruebas automatizadas (unit tests).
* `mvn package`: Empaqueta tu código compilado en un archivo distribuible, como un JAR.
* `mvn install`: Guarda el paquete en tu repositorio local para usarlo en otros de tus proyectos.

---

## 3. Gradle

Gradle es un gestor de dependencias más moderno que surgió como una alternativa más flexible y rápida a Maven. En lugar de XML, utiliza un DSL (Domain Specific Language) basado en **Groovy** o **Kotlin**, lo que hace que los archivos de configuración sean más cortos y programables. Es el estándar en el desarrollo de aplicaciones para Android.

### El Archivo `build.gradle`

Equivale al `pom.xml` de Maven, pero mucho más conciso.

```groovy
// 1. Plugins (herramientas adicionales)
plugins {
    id 'java'
}

// 2. Identificación del proyecto
group = 'com.miempresa'
version = '1.0-SNAPSHOT'

// 3. ¿De dónde se descargan las librerías?
repositories {
    mavenCentral() // Usa el mismo repositorio principal que Maven
}

// 4. Lista de Dependencias
dependencies {
    // Ejemplo: Librería Gson
    implementation 'com.google.code.gson:gson:2.10.1'
    
    // Librería solo para pruebas
    testImplementation 'org.junit.jupiter:junit-jupiter-api:5.9.2'
}
```

### Comandos principales de Gradle
* `gradle build`: Compila, prueba y empaqueta el proyecto.
* `gradle clean`: Limpia el directorio de construcción.
* `gradle test`: Ejecuta las pruebas.

---

## 4. ¿Maven o Gradle? ¿Cuál elegir?

| Característica | Maven | Gradle |
| :--- | :--- | :--- |
| **Configuración** | XML (Estricto, largo, declarativo). | Groovy/Kotlin (Conciso, programable). |
| **Curva de aprendizaje** | Baja (Las convenciones son estrictas). | Media/Alta (Mucha flexibilidad). |
| **Rendimiento** | Normal. | Muy rápido (Usa caché avanzada y ejecución incremental). |
| **Uso principal** | Proyectos Java empresariales (Spring Boot, etc.). | Proyectos Android, proyectos muy grandes o personalizados. |

**Recomendación:** Para empezar y para la mayoría de proyectos backend o de escritorio sencillos, **Maven** es excelente porque es muy estándar y casi no requiere configuración (funciona "out of the box"). Cuando necesites configuraciones complejas de construcción o desarrolles para Android, **Gradle** es la elección.

---

## 5. Repositorios de Dependencias

¿De dónde saca Maven o Gradle las librerías?
El lugar principal se llama **Maven Central Repository** (https://mvnrepository.com/). Es una inmensa base de datos pública y gratuita donde los creadores de librerías suben sus componentes. 

Cuando pides una dependencia en tu `pom.xml`, tu gestor va a Maven Central, busca las coordenadas exactas (`groupId`, `artifactId`, `version`) y la descarga a tu computadora (a una carpeta oculta en tu usuario, usualmente `.m2`).

---

## 6. Ejemplos Prácticos de Integración

A continuación, veremos dos ejemplos prácticos completos de cómo un gestor de dependencias (Maven) nos permite crear aplicaciones poderosas consumiendo librerías externas de manera sencilla.

---


## Proyecto Demo: Consumo de API REST con Retrofit

Este proyecto es un ejemplo básico de cómo consumir una API REST desde Java usando la librería **Retrofit**. El programa obtiene una lista de usuarios de una API mock, realiza todas las operaciones CRUD (Crear, Leer, Actualizar, Eliminar) y las imprime en consola.

---

## 1. Estructura del Proyecto

```bash
demo/
├── pom.xml                                    # Configuración de Maven (dependencias)
├── README.md                                  # Esta documentación
└── src/
    └── main/
        └── java
            └── com
                └── example
                    ├── Main.java              # Punto de entrada del programa
                    ├── User.java              # Modelo de datos del usuario
                    ├── Address.java           # Modelo de datos de la dirección
                    └── UserService.java       # Definición de la API (todas las operaciones)
```

---

## 2. ¿Qué es Maven y cómo funciona?

**Maven** es una herramienta que gestiona:
- **Dependencias**: Librerías externas que necesita tu proyecto (como Retrofit)
- **Compilación**: Convierte tu código Java en un programa ejecutable
- **Ejecución**: Permite correr tu programa fácilmente

### El archivo `pom.xml`

`pom.xml` es el archivo de configuración de Maven. Aquí se definen todas las dependencias:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>

    <!-- Identificación del proyecto -->
    <groupId>com.example</groupId>       <!-- Nombre de la organización -->
    <artifactId>demo</artifactId>        <!-- Nombre del proyecto -->
    <version>1.0-SNAPSHOT</version>     <!-- Versión -->

    <!-- Versión de Java que usamos -->
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <!-- Lista de dependencias (librerías externas) -->
    <dependencies>
        <!-- Retrofit: Sirve para hacer peticiones HTTP a APIs REST -->
        <dependency>
            <groupId>com.squareup.retrofit2</groupId>
            <artifactId>retrofit</artifactId>
            <version>3.0.0</version>
        </dependency>

        <!-- Gson: Convierte JSON (texto) a objetos Java y viceversa -->
        <dependency>
            <groupId>com.google.code.gson</groupId>
            <artifactId>gson</artifactId>
            <version>2.14.0</version>
        </dependency>

        <!-- Converter-Gson: Integration entre Retrofit y Gson -->
        <dependency>
            <groupId>com.squareup.retrofit2</groupId>
            <artifactId>converter-gson</artifactId>
            <version>3.0.0</version>
        </dependency>
    </dependencies>
</project>
```

---

## 3. Instalación de Dependencias

### Opción A: Desde Visual Studio Code

1. Instala la extensión **"Extension Pack for Java"** de Microsoft
2. Instala la extensión **"Maven for Java"**
3. Al abrir el proyecto, VS Code detectará automáticamente el `pom.xml`
4. Las dependencias se descargarán automáticamente

### Opción B: Desde Línea de Comandos

```bash
# Navega a la carpeta del proyecto
cd C:\Users\jhonf\Desktop\Ejercicios\demo

# Descarga todas las dependencias
mvn dependency:resolve

# Compila el proyecto
mvn compile

# Ejecuta el programa
mvn exec:java -Dexec.mainClass="com.example.Main"
```

### Opción C: Usando Gradle (alternativa a Maven)

Si prefieres Gradle en lugar de Maven, crea un archivo `build.gradle`:

```groovy
plugins {
    id 'java'
}

group = 'com.example'
version = '1.0-SNAPSHOT'

repositories {
    mavenCentral()
}

dependencies {
    implementation 'com.squareup.retrofit2:retrofit:3.0.0'
    implementation 'com.google.code.gson:gson:2.14.0'
    implementation 'com.squareup.retrofit2:converter-gson:3.0.0'
}
```

---

## 4. Explicación Detallada de Cada Archivo

### 4.1. `Address.java` - Modelo de la Dirección

```java
package com.example;

public class Address {
    private String street;   // Calle
    private String city;    // Ciudad
    private String country; // País

    public String getStreet() { return street; }
    public String getCity() { return city; }
    public String getCountry() { return country; }

    public void setStreet(String street) { this.street = street; }
    public void setCity(String city) { this.city = city; }
    public void setCountry(String country) { this.country = country; }
}
```

**¿Qué hace este archivo?**
- Define la estructura de datos para una dirección
- Cada usuario tiene una dirección anidada (un objeto dentro de otro)
- Los `getters` permiten leer los datos; los `setters` permiten modificarlos

---

### 4.2. `User.java` - Modelo del Usuario

```java
package com.example;

public class User {
    private String id;         // Identificador único (UUID)
    private String name;       // Nombre
    private String email;      // Correo electrónico
    private String phone;      // Teléfono
    private Address address;    // Objeto Address (dirección anidada)
    private String birthdate;   // Fecha de nacimiento
    private boolean isActive;   // Si está activo o no

    // Getters para cada campo
    public String getId() { return id; }
    public String getName() { return name; }
    public String getEmail() { return email; }
    public String getPhone() { return phone; }
    public Address getAddress() { return address; }
    public String getBirthdate() { return birthdate; }
    public boolean isActive() { return isActive; }

    // Setters para cada campo
    public void setId(String id) { this.id = id; }
    public void setName(String name) { this.name = name; }
    public void setEmail(String email) { this.email = email; }
    public void setPhone(String phone) { this.phone = phone; }
    public void setAddress(Address address) { this.address = address; }
    public void setBirthdate(String birthdate) { this.birthdate = birthdate; }
    public void setActive(boolean isActive) { this.isActive = isActive; }
}
```

**¿Qué hace este archivo?**
- Define la estructura de un usuario
- Coincide con el JSON que devuelve la API
- `Address address` es un objeto dentro de User (relación "tiene una")

---

### 4.3. `UserService.java` - Definición de la API (CRUD Completo)

```java
package com.example;

import java.util.List;
import retrofit2.Call;
import retrofit2.http.Body;
import retrofit2.http.DELETE;
import retrofit2.http.GET;
import retrofit2.http.PATCH;
import retrofit2.http.POST;
import retrofit2.http.PUT;
import retrofit2.http.Path;

public interface UserService {

    // GET /users - Obtener todos los usuarios
    @GET("users")
    Call<List<User>> getUsers();

    // GET /users/{id} - Obtener un usuario por su ID
    @GET("users/{id}")
    Call<User> getUserById(@Path("id") String id);

    // POST /users - Crear un nuevo usuario (genera UUID automáticamente)
    @POST("users")
    Call<User> createUser(@Body User user);

    // PUT /users/{id} - Actualización completa (reemplaza todo el objeto)
    @PUT("users/{id}")
    Call<User> updateUser(@Path("id") String id, @Body User user);

    // PATCH /users/{id} - Actualización parcial (mezcla solo los campos enviados)
    @PATCH("users/{id}")
    Call<User> patchUser(@Path("id") String id, @Body User user);

    // DELETE /users/{id} - Eliminar un usuario por su ID
    @DELETE("users/{id}")
    Call<Void> deleteUser(@Path("id") String id);
}
```

**¿Qué hace este archivo?**
- Define una **interfaz** (un contrato) para comunicarse con la API
- Cada método corresponde a una operación HTTP diferente
- `@Path("id")` inserta el valor del parámetro en la URL
- `@Body` indica que el objeto se envía en el cuerpo de la petición

**Anotaciones de Retrofit:**

| Anotación | Método HTTP | Descripción |
|-----------|------------|-------------|
| `@GET` | GET | Obtener datos |
| `@POST` | POST | Crear nuevos datos |
| `@PUT` | PUT | Reemplazar datos completamente |
| `@PATCH` | PATCH | Actualizar datos parcialmente |
| `@DELETE` | DELETE | Eliminar datos |

---

### 4.4. `Main.java` - Programa Principal

```java
package com.example;

import java.io.IOException;
import java.util.List;
import retrofit2.Response;
import retrofit2.Retrofit;
import retrofit2.converter.gson.GsonConverterFactory;

public class Main {
    public static void main(String[] args) {

        // PASO 1: Configurar Retrofit
        // ============================================
        Retrofit retrofit = new Retrofit.Builder()
                .baseUrl("https://playground.mockoon.com/")
                .addConverterFactory(GsonConverterFactory.create())
                .build();


        // PASO 2: Crear el servicio
        // ============================================
        UserService service = retrofit.create(UserService.class);


        // PASO 3: Ejecutar operaciones CRUD
        // ============================================

        // --- GET /users: Obtener todos los usuarios ---
        Response<List<User>> responseGetAll = service.getUsers().execute();
        if (responseGetAll.isSuccessful() && responseGetAll.body() != null) {
            for (User u : responseGetAll.body()) {
                System.out.println(u.getId() + " | " + u.getName() + " | " + u.getEmail());
            }
        }

        // --- GET /users/{id}: Obtener un usuario por ID ---
        String userId = "4d529d30-a87e-4b67-b858-fc54055bc7e1";
        Response<User> responseGetById = service.getUserById(userId).execute();

        // --- POST /users: Crear un nuevo usuario ---
        User newUser = new User();
        newUser.setName("Carlos García");
        newUser.setEmail("carlos@ejemplo.com");
        // ... configurar otros campos ...
        Response<User> responseCreate = service.createUser(newUser).execute();

        // --- PUT /users/{id}: Reemplazo completo ---
        User updatedUser = new User();
        updatedUser.setName("María López");
        // ... todos los campos ...
        Response<User> responsePut = service.updateUser(userId, updatedUser).execute();

        // --- PATCH /users/{id}: Actualización parcial ---
        User patchedUser = new User();
        patchedUser.setEmail("nuevo.email@ejemplo.com");
        // Solo se actualizan los campos proporcionados
        Response<User> responsePatch = service.patchUser(userId, patchedUser).execute();

        // --- DELETE /users/{id}: Eliminar usuario ---
        Response<Void> responseDelete = service.deleteUser(userId).execute();

    }
}
```

---

## 5. Operaciones CRUD Explicadas

### ¿Qué es CRUD?

CRUD son las cuatro operaciones básicas de cualquier sistema de almacenamiento:

| Operación | HTTP | Descripción | Ejemplo |
|-----------|------|-------------|---------|
| **C**reate | POST | Crear nuevo registro | Crear un usuario |
| **R**ead | GET | Leer/Obtener registros | Ver lista de usuarios |
| **U**pdate | PUT/PATCH | Actualizar registro | Cambiar email de usuario |
| **D**elete | DELETE | Eliminar registro | Borrar usuario |

---

### Diferencia entre PUT y PATCH

```
Supongamos que el usuario original es:
{
  "id": "123",
  "name": "Juan",
  "email": "juan@mail.com",
  "phone": "123456",
  "isActive": true
}

=== PUT /users/123 ===
Envías:
{ "name": "Pedro", "email": "pedro@mail.com" }

Resultado: El usuario queda con SOLO name y email,
todos los demás campos se borran (nulos/false).

=== PATCH /users/123 ===
Envías:
{ "name": "Pedro", "email": "pedro@mail.com" }

Resultado: Solo se actualizan name y email,
los demás campos permanecen igual.
```

---

---

## 7. Ejemplo de JSON y Conversión

### JSON que devuelve la API:
```json
[
  {
    "id": "4d529d30-a87e-4b67-b858-fc54055bc7e1",
    "name": "Juan Pérez",
    "email": "juan@ejemplo.com",
    "phone": "123456789",
    "address": {
      "street": "623 Jailyn Village",
      "city": "Pasadena",
      "country": "IA 54138"
    },
    "birthdate": "1990-05-15",
    "isActive": true
  }
]
```

### Conversión a Objetos Java:

```bash
JSON Array []          →    Java List<>
  └─ JSON Object {}    →    Java User
       ├─ id           →    user.setId("4d529d30-...")
       ├─ name         →    user.setName("Juan Pérez")
       ├─ email        →    user.setEmail("juan@ejemplo.com")
       ├─ phone        →    user.setPhone("123456789")
       ├─ address      →    user.setAddress(Address)
       │     ├─ street →    address.setStreet("623 Jailyn Village")
       │     ├─ city   →    address.setCity("Pasadena")
       │     └─ country →  address.setCountry("IA 54138")
       ├─ birthdate    →    user.setBirthdate("1990-05-15")
       └─ isActive     →    user.setActive(true)
```

---

## 8. Comandos Útiles de Maven

| Comando | Descripción |
|---------|-------------|
| `mvn compile` | Compila el proyecto |
| `mvn exec:java -Dexec.mainClass="com.example.Main"` | Ejecuta el programa |
| `mvn clean` | Limpia archivos compilados |
| `mvn dependency:resolve` | Descarga las dependencias |
| `mvn dependency:tree` | Muestra el árbol de dependencias |
| `mvn package` | Crea un archivo JAR |

---

---

## 10. Requisitos Previos

Para ejecutar este proyecto necesitas:

1. **Java Development Kit (JDK) 17 o superior**
   - Descargar: https://adoptium.net/
   - Verificar instalación: `java -version`

2. **Maven** (opcional, si no usas VS Code)
   - Descargar: https://maven.apache.org/download.cgi
   - Verificar instalación: `mvn -version`

3. **Conexión a Internet**
   - Necesaria para descargar las dependencias
   - Necesaria para hacer la petición a la API

---

## 11. Conceptos Clave Resumidos

| Concepto | Explicación Simple |
|----------|-------------------|
| **API REST** | Un servicio web que sigue reglas específicas para comunicarse |
| **HTTP** | El protocolo que usa la web para transferir datos |
| **GET** | Solicitar datos (como leer una página web) |
| **POST** | Crear nuevos datos en el servidor |
| **PUT** | Reemplazar un registro completamente |
| **PATCH** | Actualizar solo algunos campos de un registro |
| **DELETE** | Eliminar un registro |
| **JSON** | Formato de texto para intercambiar datos |
| **Retrofit** | Librería que facilita hacer peticiones HTTP desde Java |
| **Gson** | Librería que convierte JSON a objetos Java |
| **Maven** | Herramienta que gestiona dependencias y compilación |
| **Dependencia** | Librería externa que tu proyecto necesita |
| **CRUD** | Create, Read, Update, Delete - operaciones básicas |
| **UUID** | Identificador único universal (ej: "4d529d30-a87e-4b67-b858-fc54055bc7e1") |


---

## Proyecto Demo2: Juego 2D con FXGL

Este proyecto es un ejemplo básico de cómo crear un juego 2D simple usando **FXGL** (un framework de juegos basado en JavaFX). El programa muestra una ventana con un personaje cuadrado de color azul que puede moverse con las teclas WASD.

---

## 1. Estructura del Proyecto

```bash
demo2/
├── pom.xml                                    # Configuración de Maven (dependencias)
├── README.md                                  # Esta documentación
└── src/
    └── main/
        └── java
            └── com
                └── example
                    ├── Main.java              # Punto de entrada del programa
                    └── MiJuego.java           # Clase principal del juego (extiende GameApplication)
```

---

## 2. ¿Qué es Maven y cómo funciona?

**Maven** es una herramienta que gestiona:
- **Dependencias**: Librerías externas que necesita tu proyecto (como FXGL)
- **Compilación**: Convierte tu código Java en un programa ejecutable
- **Ejecución**: Permite correr tu programa fácilmente

### El archivo `pom.xml`

`pom.xml` es el archivo de configuración de Maven. Aquí se definen todas las dependencias:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>

    <!-- Identificación del proyecto -->
    <groupId>com.example</groupId>       <!-- Nombre de la organización -->
    <artifactId>demo2</artifactId>       <!-- Nombre del proyecto -->
    <version>1.0-SNAPSHOT</version>     <!-- Versión -->

    <!-- Versión de Java que usamos -->
    <properties>
        <maven.compiler.source>21</maven.compiler.source>
        <maven.compiler.target>21</maven.compiler.target>
    </properties>

    <!-- Lista de dependencias (librerías externas) -->
    <dependencies>
        <!-- FXGL: Framework de juegos 2D basado en JavaFX -->
        <dependency>
            <groupId>com.github.almasb</groupId>
            <artifactId>fxgl</artifactId>
            <version>23.3</version>
        </dependency>
    </dependencies>
</project>
```

---

## 3. Instalación de Dependencias

### Opción A: Desde Visual Studio Code

1. Instala la extensión **"Extension Pack for Java"** de Microsoft
2. Instala la extensión **"Maven for Java"**
3. Al abrir el proyecto, VS Code detectará automáticamente el `pom.xml`
4. Las dependencias se descargarán automáticamente

### Opción B: Desde Línea de Comandos

```bash
# Navega a la carpeta del proyecto
cd C:\Users\jhonf\Desktop\Ejercicios\demo2

# Descarga todas las dependencias
mvn dependency:resolve

# Compila el proyecto
mvn compile

# Ejecuta el programa
mvn exec:java -Dexec.mainClass="com.example.Main"
```

---

## 4. Explicación Detallada de Cada Archivo

### 4.1. `Main.java` - Punto de Entrada

```java
package com.example;
import com.almasb.fxgl.app.GameApplication;

public class Main {
    public static void main(String[] args) {
        // Este método estático de GameApplication busca la clase que
        // extiende de ella y arranca el ciclo de vida del juego.
        GameApplication.launch(MiJuego.class, args);
    }
}
```

**¿Qué hace este archivo?**
- Es el punto de entrada del programa
- Llama a `GameApplication.launch()` pasando la clase `MiJuego` como parámetro
- FXGL internamente busca una clase que extienda `GameApplication` y ejecuta su ciclo de vida

---

### 4.2. `MiJuego.java` - Clase Principal del Juego

```java
package com.example;

import com.almasb.fxgl.app.GameApplication;
import com.almasb.fxgl.app.GameSettings;
import com.almasb.fxgl.entity.Entity;
import javafx.scene.input.KeyCode;
import javafx.scene.paint.Color;
import javafx.scene.shape.Rectangle;
import javafx.scene.text.Text;

import static com.almasb.fxgl.dsl.FXGL.*;

public class MiJuego extends GameApplication {

    private Entity jugador;

    @Override
    protected void initSettings(GameSettings settings) {
        settings.setWidth(800);           // Ancho de la ventana
        settings.setHeight(600);           // Alto de la ventana
        settings.setTitle("FXGL Separado"); // Título de la ventana
        settings.setVersion("1.0");        // Versión del juego
    }

    @Override
    protected void initGame() {
        // Fondo simple
        getGameScene().setBackgroundColor(Color.LIGHTGRAY);

        // Jugador
        jugador = entityBuilder()
                .at(100, 100)
                .viewWithBBox(new Rectangle(40, 40, Color.BLUE))
                .buildAndAttach();

        // Texto de ayuda
        addUINode(new Text("Usa WASD para moverte"), 20, 30);
    }

    @Override
    protected void initInput() {
        onKey(KeyCode.W, () -> jugador.translateY(-5));
        onKey(KeyCode.S, () -> jugador.translateY(5));
        onKey(KeyCode.A, () -> jugador.translateX(-5));
        onKey(KeyCode.D, () -> jugador.translateX(5));
    }
}
```

**¿Qué hace este archivo?**
- Extiende `GameApplication` que proporciona el ciclo de vida del juego
- Define la configuración de la ventana (ancho, alto, título)
- Crea un jugador (rectángulo azul) en una posición inicial
- Configura los controles de teclado (WASD para mover)

---

## 5. Métodos del Ciclo de Vida de FXGL

FXGL proporciona varios métodos que puedes sobrescribir para controlar el juego:

| Método | Descripción |
|--------|-------------|
| `initSettings(GameSettings settings)` | Configura las propiedades de la ventana (tamaño, título) |
| `initGame()` | Se ejecuta una vez al iniciar el juego. Aquí se crean las entidades |
| `initInput()` | Configura los controles de teclado y mouse |
| `initPhysics()` | Configura las propiedades de la física (gravedad, colisiones) |
| `onUpdate(long t)` | Se ejecuta constantemente (60 veces por segundo). Ideal para lógica del juego |

---

## 6. Sistema de Entidades en FXGL

En FXGL, todo en el juego es una **Entity** (entidad). Las entidades tienen:

- **Position** (posición):Dónde está en la pantalla
- **View** (vista):Lo que se ve (imagen, forma, texto)
- **Bounding Box** (caja de colisión):Para detectar colisiones

### Crear una Entidad

```java
jugador = entityBuilder()
    .at(100, 100)                                    // Posición (x, y)
    .viewWithBBox(new Rectangle(40, 40, Color.BLUE)) // Visual + caja de colisión
    .buildAndAttach();                               // Crear y añadir al juego
```

---

## 7. Sistema de Entrada (Controles)

### Eventos de Teclado

```java
onKey(KeyCode.W, () -> jugador.translateY(-5));  // Al presionar W: mover arriba
onKey(KeyCode.S, () -> jugador.translateY(5));    // Al presionar S: mover abajo
onKey(KeyCode.A, () -> jugador.translateX(-5));   // Al presionar A: mover izquierda
onKey(KeyCode.D, () -> jugador.translateX(5));     // Al presionar D: mover derecha
```

### Métodos de Movimiento de Entity

| Método | Descripción |
|--------|-------------|
| `translateX(n)` | Mueve la entidad n píxeles en el eje X |
| `translateY(n)` | Mueve la entidad n píxeles en el eje Y |
| `translate(nx, ny)` | Mueve la entidad en ambos ejes |

---

---

## 9. Comandos Útiles de Maven

| Comando | Descripción |
|---------|-------------|
| `mvn compile` | Compila el proyecto |
| `mvn exec:java -Dexec.mainClass="com.example.Main"` | Ejecuta el programa |
| `mvn clean` | Limpia archivos compilados |
| `mvn dependency:resolve` | Descarga las dependencias |
| `mvn dependency:tree` | Muestra el árbol de dependencias |
| `mvn package` | Crea un archivo JAR |

---

---

## 11. Requisitos Previos

Para ejecutar este proyecto necesitas:

1. **Java Development Kit (JDK) 21 o superior**
   - Descargar: https://adoptium.net/
   - Verificar instalación: `java -version`

2. **Maven** (opcional, si no usas VS Code)
   - Descargar: https://maven.apache.org/download.cgi
   - Verificar instalación: `mvn -version`

---

## 12. Próximos Pasos para Extender el Juego

Una vez que entiendas este ejemplo básico, puedes:

1. **Añadir sprites**: Reemplazar el `Rectangle` por imágenes
2. **Añadir física**: Usar `initPhysics()` para gravedad y colisiones
3. **Añadir enemigos**: Crear más entidades con IA básica
4. **Añadir puntuación**: Usar `FXGL.incScore(n)` y mostrar en pantalla
5. **Añadir sonidos**: Usar `FXGL.play("sound.wav")`
6. **Crear niveles**: Gestionar múltiples `GameScene` o usar sistemas de escenas de FXGL

---

## 13. Conceptos Clave Resumidos

| Concepto | Explicación Simple |
|----------|-------------------|
| **FXGL** | Framework de juegos 2D gratuito para Java |
| **GameApplication** | Clase base que proporciona el ciclo de vida del juego |
| **Entity** | Objeto en el juego (jugador, enemigo, obstáculo) |
| **GameSettings** | Configuración de la ventana del juego |
| **Bounding Box** | Caja de colisión para detectar cuándo dos entidades se tocan |
| **translateX/Y** | Mover una entidad en los ejes X o Y |
| **onKey()** | Evento que se ejecuta al presionar una tecla |
| **Maven** | Herramienta que gestiona dependencias y compilación |
| **Dependencia** | Librería externa que tu proyecto necesita |
| **JavaFX** | Biblioteca gráfica de Java que FXGL utiliza internamente |
---

## Proyecto Demo3: Generador de PDF con OpenPDF

Este proyecto es un ejemplo básico de cómo crear documentos PDF usando **OpenPDF** (una librería Java de código abierto). El programa genera un archivo PDF simple con un título y datos de ejemplo.

---

## 1. Estructura del Proyecto

```bash
demo3/
├── pom.xml                    # Configuración de Maven (dependencias)
├── README.md                  # Esta documentación
└── src/
    └── main/
        └── java
            └── com
                └── example
                    └── Main.java      # Genera un PDF simple
```

---

## 2. ¿Qué es Maven y cómo funciona?

**Maven** es una herramienta que gestiona:
- **Dependencias**: Librerías externas que necesita tu proyecto (como OpenPDF)
- **Compilación**: Convierte tu código Java en un programa ejecutable
- **Ejecución**: Permite correr tu programa fácilmente

### El archivo `pom.xml`

`pom.xml` es el archivo de configuración de Maven:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>

    <!-- Identificación del proyecto -->
    <groupId>com.example</groupId>
    <artifactId>demo3</artifactId>
    <version>1.0-SNAPSHOT</version>

    <!-- Versión de Java -->
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <!-- Dependencias -->
    <dependencies>
        <!-- OpenPDF: Librería para crear PDFs -->
        <dependency>
            <groupId>com.github.librepdf</groupId>
            <artifactId>openpdf</artifactId>
            <version>1.3.35</version>
        </dependency>
    </dependencies>
</project>
```

---

## 3. Instalación y Ejecución

### Opción A: Desde Visual Studio Code

1. Instala la extensión **"Extension Pack for Java"** de Microsoft
2. Instala la extensión **"Maven for Java"**
3. Al abrir el proyecto, VS Code detectará automáticamente el `pom.xml`
4. Las dependencias se descargarán automáticamente

### Opción B: Desde Línea de Comandos

```bash
# Navega a la carpeta del proyecto
cd C:\Users\jhonf\Desktop\Ejercicios\demo3

# Descarga todas las dependencias
mvn dependency:resolve

# Compila el proyecto
mvn compile

# Ejecuta el programa
mvn exec:java -Dexec.mainClass="com.example.Main"
```

---

## 4. Explicación del Archivo Main.java

```java
package com.example;

import com.lowagie.text.Document;          // Documento PDF
import com.lowagie.text.FontFactory;      // Factory para crear fuentes
import com.lowagie.text.pdf.PdfWriter;   // Escritor de PDF
import java.io.FileOutputStream;          // Salida a archivo

public class Main {
    public static void main(String[] args) throws Exception {
        // 1. Crear un documento PDF
        var doc = new Document();

        // 2. Crear el escritor que genera el archivo
        PdfWriter.getInstance(doc, new FileOutputStream("reporte.pdf"));

        // 3. Abrir el documento para agregar contenido
        doc.open();

        // 4. Agregar título
        var titleFont = FontFactory.getFont(FontFactory.HELVETICA_BOLD, 18);
        doc.add(new com.lowagie.text.Paragraph("Reporte de Sistema", titleFont));
        doc.add(new com.lowagie.text.Paragraph(" "));  // Espacio vacío

        // 5. Agregar datos
        var normalFont = FontFactory.getFont(FontFactory.HELVETICA, 12);
        doc.add(new com.lowagie.text.Paragraph("Estado: Operativo", normalFont));
        doc.add(new com.lowagie.text.Paragraph("Sector: Java Backend", normalFont));

        // 6. Cerrar el documento (genera el archivo)
        doc.close();

        System.out.println("PDF generado: reporte.pdf");
    }
}
```

---

## 5. Conceptos Clave de OpenPDF

### 5.1. Document

El `Document` es el contenedor del PDF. Debes:
1. **Crearlo**: `new Document()`
2. **Abrirlo**: `doc.open()` antes de agregar contenido
3. **Cerrarlo**: `doc.close()` al terminar

### 5.2. Paragraph

Un `Paragraph` representa un bloque de texto. Puede contener:
- Texto plano
- Fuente personalizada
- Espaciado

```java
doc.add(new Paragraph("Texto"));              // Texto simple
doc.add(new Paragraph(" ", font));           // Espacio (saltos de línea)
```

### 5.3. FontFactory

Permite crear fuentes con diferentes estilos:

| Constante | Descripción |
|-----------|-------------|
| `FontFactory.HELVETICA` | Fuente sans-serif |
| `FontFactory.HELVETICA_BOLD` | Sans-serif bold |
| `FontFactory.TIMES_ROMAN` | Fuente serif |
| `FontFactory.COURIER` | Fuente monoespaciada |

Parámetros: `FontFactory.getFont(nombre, tamaño)`

### 5.4. PdfWriter

`PdfWriter` conecta el `Document` con un archivo de salida:

```java
PdfWriter.getInstance(doc, new FileOutputStream("reporte.pdf"));
```

---

---

## 7. Comandos Útiles de Maven

| Comando | Descripción |
|---------|-------------|
| `mvn compile` | Compila el proyecto |
| `mvn exec:java -Dexec.mainClass="com.example.Main"` | Ejecuta el programa |
| `mvn clean` | Limpia archivos compilados |
| `mvn dependency:resolve` | Descarga las dependencias |
| `mvn dependency:tree` | Muestra el árbol de dependencias |
| `mvn package` | Crea un archivo JAR |

---

---

## 9. Requisitos Previos

Para ejecutar este proyecto necesitas:

1. **Java Development Kit (JDK) 17 o superior**
   - Descargar: https://adoptium.net/
   - Verificar instalación: `java -version`

2. **Maven** (opcional, si no usas VS Code)
   - Descargar: https://maven.apache.org/download.cgi
   - Verificar instalación: `mvn -version`

---

## 10. Elementos Disponibles en OpenPDF

OpenPDF ofrece muchos más elementos para crear PDFs complejos:

| Elemento | Descripción |
|---------|-------------|
| `Paragraph` | Bloque de texto |
| `Table` | Tabla con filas y celdas |
| `Image` | Imagen insertada |
| `List` | Lista con viñetas |
| `Chapter` / `Section` | Estructura jerárquica |
| `Anchor` | Hipervínculo |
| `Barcode` | Código de barras |

---

## 11. Próximos Pasos para Extender

Una vez que entiendas este ejemplo básico, puedes:

1. **Añadir tablas**: Usar `Table` para datos estructurados
2. **Añadir imágenes**: Usar `Image.getInstance(path)`
3. **Añadir formato**: Combinas fuentes, colores y tamaños
4. **Añadir páginas**: `doc.newPage()` para múltiples páginas
5. **Añadir encabezados/pie de página**: Usar `PdfPageEvent`
6. **Crear facturas o reportes**: Combinar tablas, imágenes y párrafos

---

## 12. Conceptos Clave Resumidos

| Concepto | Explicación Simple |
|----------|-------------------|
| **OpenPDF** | Librería Java para crear archivos PDF |
| **Document** | Contenedor del PDF que se genera |
| **Paragraph** | Bloque de texto en el PDF |
| **FontFactory** | Factory para crear fuentes (tipo, tamaño, estilo) |
| **PdfWriter** | Conecta el Document con un archivo de salida |
| **Maven** | Herramienta que gestiona dependencias y compilación |
| **Dependencia** | Librería externa que el proyecto necesita |
