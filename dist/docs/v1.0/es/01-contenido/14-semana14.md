---
title: "Semana 14: Hibernate desde Cero"
position: 14
---

# Guía Definitiva: Hibernate desde Cero (Sin Spring Boot)

Esta guía proporciona el **ecosistema completo y profesional** para implementar persistencia de datos en Java 24 utilizando Hibernate 6. Aprenderás a configurar un proyecto desde la base, manejar entidades, y aplicar patrones de diseño como **Singleton** y **Repository**.

Veremos dos enfoques:
1.  **Enfoque Directo:** Ideal para entender cómo funciona el `EntityManager` y las transacciones.
2.  **Enfoque Profesional:** Utiliza abstracciones para crear aplicaciones escalables.

---

## 📂 Estructura del Proyecto

Para que el proyecto funcione correctamente, los archivos deben estar organizados siguiendo el estándar de Maven:

```text
hibernate-project/
├── pom.xml                                   # Raíz del proyecto
└── src/
    └── main/
        ├── java/                             # Código fuente Java
        │   └── org/
        │       └── example/
        │           ├── Main.java             # Clase Principal
        │           ├── User.java             # Entidad Usuario
        │           ├── Product.java          # Entidad Producto
        │           ├── util/
        │           │   └── JpaUtil.java      # Utilidad Singleton JPA
        │           └── repository/           # Capa de Persistencia (Enfoque 2)
        │               ├── Repository.java
        │               ├── UserRepository.java
        │               ├── ProductRepository.java
        │               └── impl/
        │                   └── GenericRepositoryImpl.java
        └── resources/
            └── META-INF/
                └── persistence.xml           # Configuración de JPA/Hibernate
```

---

## ⚙️ Configuración Común (Estructura Base)

Antes de elegir un enfoque, necesitamos configurar las bases del proyecto.

### 1. Configuración del Proyecto (`pom.xml`)

El archivo `pom.xml` gestiona las librerías necesarias. Aquí definimos qué herramientas externas necesita nuestro proyecto para funcionar.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>orm</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>24</maven.compiler.source>
        <maven.compiler.target>24</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <!-- Hibernate Core: El motor que traduce objetos Java a tablas SQL -->
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate-core</artifactId>
            <version>6.6.2.Final</version>
        </dependency>

        <!-- PostgreSQL Driver: El "traductor" que permite a Java hablar con la base de datos -->
        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <version>42.7.10</version>
        </dependency>
    </dependencies>
</project>
```

**Explicación de Dependencias:**
*   **Hibernate Core**: Es el ORM (Object-Relational Mapping). Su función es evitar que escribas SQL manualmente, mapeando tus clases a tablas de forma automática.
*   **PostgreSQL Driver**: Sin este conector, Java no sabría cómo conectarse físicamente al servidor de PostgreSQL.

---

### 2. Configuración de JPA (`persistence.xml`)

Este archivo es el estándar de Java para configurar la persistencia. Debe ubicarse exactamente en: `src/main/resources/META-INF/persistence.xml`.

```xml
<persistence xmlns="https://jakarta.ee/xml/ns/persistence" version="3.0">
    <persistence-unit name="miUnidadPersistencia">
        <class>org.example.User</class>
        <class>org.example.Product</class>

        <properties>
            <!-- Parámetros de Conexión (PostgreSQL Prisma) -->
            <property name="jakarta.persistence.jdbc.driver" value="org.postgresql.Driver"/>
            <property name="jakarta.persistence.jdbc.url" value="jdbc:postgresql://db.prisma.io:5432/postgres?sslmode=require"/>
            <property name="jakarta.persistence.jdbc.user" value="ceb0eee7816dce660ca0d4659dc8e6cfe01a318623a61a69b1085dffdea919c9"/>
            <property name="jakarta.persistence.jdbc.password" value="sk_hPfVJQxw5fHBL2aro_4Ls"/>

            <!-- Configuración Hibernate -->
            <property name="hibernate.dialect" value="org.hibernate.dialect.PostgreSQLDialect"/>
            
            <!-- hbm2ddl.auto: 'update' crea o modifica las tablas automáticamente según tus clases -->
            <property name="hibernate.hbm2ddl.auto" value="update"/>
            
            <!-- Muestra el SQL que Hibernate genera internamente en la consola -->
            <property name="hibernate.show_sql" value="true"/>
            <property name="hibernate.format_sql" value="true"/>
        </properties>
    </persistence-unit>
</persistence>
```

> [!TIP]
> El valor `hibernate.hbm2ddl.auto` en `update` es ideal para desarrollo, pero en producción se recomienda usar `validate` o herramientas de migración profesional.

---

### 3. Modelos de Datos (Entidades)

Las entidades son clases Java que representan tablas en la base de datos. Usamos anotaciones de **Jakarta Persistence** para definir este mapeo.

#### `User.java` (`src/main/java/org/example/User.java`)
```java
package org.example;

import jakarta.persistence.*;

@Entity
@Table(name = "users") // Nombre de la tabla en la DB
public class User {

    @Id // Define la llave primaria
    @GeneratedValue(strategy = GenerationType.IDENTITY) // Auto-incremental
    private Long id;

    private String username;
    private String email;

    public User() {} // Constructor vacío obligatorio para Hibernate

    public User(Long id, String username, String email) {
        this.id = id;
        this.username = username;
        this.email = email;
    }

    // Getters y Setters...
}
```

#### `Product.java` (`src/main/java/org/example/Product.java`)
```java
package org.example;

import jakarta.persistence.*;

@Entity
@Table(name = "products")
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private Double price;

    public Product() {}
    
    // Getters y Setters...
}
```

---

### 4. Utilidades (`JpaUtil.java`) (`src/main/java/org/example/util/JpaUtil.java`)

Crear una `EntityManagerFactory` es un proceso costoso en términos de recursos. Por ello, aplicamos el patrón **Singleton** para asegurar que solo exista una instancia en toda la aplicación.

```java
package org.example.util;

import jakarta.persistence.EntityManager;
import jakarta.persistence.EntityManagerFactory;
import jakarta.persistence.Persistence;

public class JpaUtil {
    // La instancia única se crea una sola vez al cargar la clase
    private static final EntityManagerFactory emf = buildEntityManagerFactory();

    private static EntityManagerFactory buildEntityManagerFactory() {
        try {
            return Persistence.createEntityManagerFactory("miUnidadPersistencia");
        } catch (Throwable ex) {
            System.err.println("Error crítico al iniciar Hibernate: " + ex);
            throw new ExceptionInInitializerError(ex);
        }
    }

    public static EntityManager getEntityManager() {
        return emf.createEntityManager(); // EntityManager es ligero, se crea por cada operación/sesión
    }

    public static void close() {
        if (emf != null && emf.isOpen()) {
            emf.close();
        }
    }
}
```

---

## 🚀 Enfoque 1: Operaciones CRUD Directas (Simplificado)

En este enfoque, utilizamos el `EntityManager` directamente para interactuar con la base de datos. Es la forma más rápida de aprender cómo Hibernate gestiona los objetos.

### 1. Conceptos Clave
- `em.persist(entity)`: Guarda un nuevo registro en la base de datos.
- `em.find(Class, id)`: Busca un registro por su clave primaria.
- `em.createQuery(jpql)`: Ejecuta consultas personalizadas utilizando el lenguaje de Hibernate (JPQL).
- `em.getTransaction().begin()` / `commit()`: Delimita el inicio y fin de una operación que modifica datos.

### 2. Clase Principal (`Main.java`) (`src/main/java/org/example/Main.java`)

```java
package org.example;

import jakarta.persistence.EntityManager;
import org.example.util.JpaUtil;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        // 1. Obtener el gestor de entidades
        EntityManager em = JpaUtil.getEntityManager();

        try {
            System.out.println("--- Ejemplo Hibernate Simplificado ---");

            // 2. Crear y persistir un Usuario (Requiere Transacción)
            User user = new User();
            user.setUsername("JuanPerez_" + System.currentTimeMillis());
            user.setEmail("juan@mail.com");

            em.getTransaction().begin();
            em.persist(user); // Hibernate prepara el INSERT
            em.getTransaction().commit(); // Se ejecuta el SQL físicamente
            System.out.println("Usuario guardado: " + user.getUsername());

            // 3. Listar Usuarios usando JPQL
            System.out.println("\n--- Lista de Usuarios ---");
            List<User> users = em.createQuery("SELECT u FROM User u", User.class).getResultList();
            users.forEach(u -> System.out.println("ID: " + u.getId() + " | Name: " + u.getUsername()));

        } catch (Exception e) {
            // Si algo falla, deshacemos los cambios para evitar datos corruptos
            if (em.getTransaction().isActive()) em.getTransaction().rollback();
            e.printStackTrace();
        } finally {
            // 4. Cerrar recursos siempre
            em.close();
            JpaUtil.close();
        }
    }
}
```

---

## 🏛️ Enfoque 2: Capa de Persistencia Profesional (Patrón Repository)

Este enfoque abstrae la lógica de acceso a datos, permitiendo que el resto de la aplicación no sepa que estamos usando Hibernate. Es el estándar en la industria.

### 1. Interfaz Genérica `Repository.java` (`src/main/java/org/example/repository/Repository.java`)
Define el contrato estándar para cualquier entidad del sistema.
```java
package org.example.repository;

import java.util.List;
import java.util.Optional;

public interface Repository<T, ID> {
    void save(T entity);
    Optional<T> findById(ID id);
    List<T> findAll();
    void delete(T entity);
    void update(T entity);
}
```

### 2. Implementación Genérica `GenericRepositoryImpl.java` (`src/main/java/org/example/repository/impl/GenericRepositoryImpl.java`)
Aquí reside la lógica reutilizable para todas nuestras entidades, manejando transacciones de forma segura y automática.
```java
package org.example.repository.impl;

import jakarta.persistence.EntityManager;
import org.example.repository.Repository;
import java.util.List;
import java.util.Optional;

public class GenericRepositoryImpl<T, ID> implements Repository<T, ID> {
    protected final EntityManager em;
    private final Class<T> entityClass;

    public GenericRepositoryImpl(EntityManager em, Class<T> entityClass) {
        this.em = em;
        this.entityClass = entityClass;
    }

    @Override
    public void save(T entity) {
        executeInTransaction(() -> em.persist(entity));
    }

    @Override
    public Optional<T> findById(ID id) {
        return Optional.ofNullable(em.find(entityClass, id));
    }

    @Override
    public List<T> findAll() {
        return em.createQuery("FROM " + entityClass.getSimpleName(), entityClass).getResultList();
    }

    @Override
    public void delete(T entity) {
        executeInTransaction(() -> em.remove(em.contains(entity) ? entity : em.merge(entity)));
    }

    @Override
    public void update(T entity) {
        executeInTransaction(() -> em.merge(entity));
    }

    // Método utilitario para asegurar que las operaciones se realicen dentro de una transacción
    protected void executeInTransaction(Runnable action) {
        try {
            em.getTransaction().begin();
            action.run();
            em.getTransaction().commit();
        } catch (RuntimeException e) {
            if (em.getTransaction().isActive()) em.getTransaction().rollback();
            throw e;
        }
    }
}
```

### 3. Repositorios Específicos

#### `UserRepository.java` (`src/main/java/org/example/repository/UserRepository.java`)
```java
public class UserRepository extends GenericRepositoryImpl<User, Long> {
    public UserRepository(EntityManager em) { super(em, User.class); }
}
```

#### `ProductRepository.java` (`src/main/java/org/example/repository/ProductRepository.java`)
```java
public class ProductRepository extends GenericRepositoryImpl<Product, Long> {
    public ProductRepository(EntityManager em) { super(em, Product.class); }
}
```

### 4. Clase Principal Profesional (`Main.java`) (`src/main/java/org/example/Main.java`)
```java
public class Main {
    public static void main(String[] args) {
        EntityManager em = JpaUtil.getEntityManager();
        UserRepository userRepository = new UserRepository(em);

        try {
            System.out.println("--- Ejecutando enfoque Repository ---");
            User user = new User();
            user.setUsername("JavaPro_" + System.currentTimeMillis());
            userRepository.save(user);
            
            userRepository.findAll().forEach(u -> System.out.println(u.getUsername()));
        } finally {
            em.close();
            JpaUtil.close();
        }
    }
}
```

---

## 🎓 Conclusión y Mejores Prácticas

1.  **Transacciones**: Siempre envuelve operaciones de escritura (`save`, `update`, `delete`) en una transacción para mantener la integridad de los datos.
2.  **Cierre de Recursos**: Asegúrate de cerrar el `EntityManager` al finalizar para evitar fugas de memoria y agotar las conexiones de la BD.
3.  **EntityManager vs Factory**: Recuerda que la Factory es pesada (Singleton) y el Manager es ligero (uno por hilo/sesión).
