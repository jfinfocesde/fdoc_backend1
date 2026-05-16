---
title: "Avance 3: Persistencia y ORM"
description: "Sprint 2 - Hibernate, PostgreSQL y Lógica de Negocio Final (BackEnd 1)"
position: 3
---

# Avance 3: Persistencia con Hibernate y POO - BackEnd 1

**Fecha de Entrega:** Semana 17
**Rol:** Desarrollador Backend (Java)

## 📌 Objetivo
Finalizar la construcción del núcleo del sistema integrando una base de datos real. El objetivo es transformar el modelo conceptual y la lógica en memoria desarrollada anteriormente en una aplicación robusta que utilice **Hibernate (JPA)** y **PostgreSQL** para la persistencia de datos, manteniendo una interfaz de consola limpia y funcional.

## 📝 Qué debes entregar

1.  **Configuración del Entorno de Persistencia:**
    - Proyecto Maven con el archivo `pom.xml` actualizado con las dependencias de Hibernate y el driver de PostgreSQL.
    - Archivo `persistence.xml` (en `src/main/resources/META-INF/`) configurado correctamente.

2.  **Mapeo de Entidades (ORM):**
    - Mapeo de al menos 2 o 3 entidades principales utilizando anotaciones de **Jakarta Persistence**.
    - Implementación de relaciones entre entidades (uno a muchos, muchos a uno) si el modelo lo requiere.
    - Constructores (incluyendo el vacío), getters, setters y métodos `toString()`.

3.  **Capa de Persistencia Profesional:**
    - Clase `JpaUtil` para gestionar el `EntityManagerFactory` mediante el patrón **Singleton**.
    - Implementación de una capa de **Repositorio** o **DAO** que abstraiga las consultas SQL/JPQL.

4.  **Lógica de Negocio y Consola:**
    - Aplicación funcional que permita realizar operaciones CRUD (Crear, Leer, Actualizar, Eliminar) desde la terminal.
    - Uso correcto de **POO** (Encapsulamiento, Herencia o Polimorfismo según aplique).
    - Gestión de transacciones para asegurar la integridad de los datos.

## ✅ Criterios de Evaluación

Tu profesor (Tech Lead) evaluará los siguientes puntos:

| Criterio | Descripción | Puntaje |
| :--- | :--- | :--- |
| **Instalación y Configuración** | El `pom.xml` y `persistence.xml` están configurados correctamente y permiten la conexión a la BD. | 15% |
| **Mapeo Relacional (ORM)** | Uso correcto de anotaciones JPA para mapear atributos y relaciones entre tablas. | 25% |
| **Implementación de Patrones** | Uso de `JpaUtil` (Singleton) y abstracción de la lógica de persistencia (Repository). | 20% |
| **Funcionalidad CRUD** | La aplicación permite gestionar datos de forma persistente desde la consola sin errores. | 25% |
| **Calidad de Código y POO** | Aplicación de principios de POO, nomenclatura correcta y organización por paquetes. | 15% |

---

> [!IMPORTANT]
> **Nota técnica:** Recuerda que el valor `hibernate.hbm2ddl.auto` debe estar en `update` para que las tablas se creen automáticamente durante tus pruebas. Verifica que el servicio de PostgreSQL esté activo antes de ejecutar tu aplicación.
