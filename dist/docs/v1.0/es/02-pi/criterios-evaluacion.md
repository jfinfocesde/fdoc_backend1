---
title: "Criterios de Evaluación"
description: "Rúbrica completa y lista de entregables del Proyecto Integrador (BackEnd 1)"
position: 1
---

# Proyecto Integrador: Rúbrica de Evaluación BackEnd 1

Este documento detalla todos los requerimientos técnicos y los criterios bajo los cuales será evaluado el Proyecto Integrador.

> [!IMPORTANT]
> **Adaptación al Proyecto:** Todos los entregables y criterios mencionados a continuación deben ser aplicados y adaptados de forma coherente a la **propuesta de desarrollo y caso de estudio específico** de cada equipo (definido previamente en el módulo de Metodologías Ágiles). No se aceptarán implementaciones genéricas que no tengan relación con el dominio de su proyecto.

---

## 📝 Lista de Entregables

A continuación se detallan los artefactos que deben ser entregados y sustentados durante el desarrollo del proyecto:

### 1. Diseño y Arquitectura
- **Diagrama de Clases (UML)**: Representación gráfica de las entidades del proyecto, detallando atributos privados (`-`), métodos públicos (`+`) y relaciones entre clases.

### 2. Configuración y Entorno
- **Archivo `pom.xml` (Maven)**: Configuración que incluya las dependencias de **Hibernate Core**, **PostgreSQL Driver** y al menos una **dependencia adicional** (libre elección) integrada correctamente.
- **Archivo `persistence.xml`**: Configuración estándar de la unidad de persistencia para la conexión física con la base de datos.

### 3. Modelo de Datos y Persistencia
- **Entidades JPA**: Clases Java correctamente anotadas para el mapeo objeto-relacional.
- **Utilidad Singleton (`JpaUtil`)**: Implementación para la gestión eficiente del `EntityManagerFactory`.
- **Capa Repository**:
  - Interfaz genérica `Repository<T, ID>` con métodos CRUD.
  - Implementación genérica `GenericRepositoryImpl<T, ID>`.
  - Repositorios específicos por cada entidad principal.

### 4. Funcionalidad y Valor Agregado
- **Interfaz de Consola**: Menú interactivo que permita realizar operaciones CRUD reales sobre la base de datos.
- **Integración de Terceros**: Implementación funcional de la librería adicional (ej. exportación a PDF, Excel, envío de correos, etc.) utilizando los datos persistidos.

---

## ✅ Lista de Criterios de Evaluación

La evaluación se basará en el cumplimiento técnico de los siguientes estándares:

### 1. Calidad del Diseño y POO
- **Coherencia**: El diseño debe ser una solución válida para el problema planteado en Metodologías Ágiles.
- **Pilares POO**: Uso correcto de Abstracción y Encapsulamiento (getters/setters, modificadores de acceso).
- **Estándares**: Uso de nomenclatura Java (CamelCase) y notación UML estándar.

### 2. Implementación de Patrones y Persistencia
- **Uso de Genéricos**: Implementación de una arquitectura de repositorios reutilizable mediante genéricos.
- **Abstracción y Desacoplamiento**: Uso de interfaces para separar la definición de las operaciones de su implementación técnica.
- **Transaccionalidad**: Manejo robusto de transacciones (`begin`, `commit`, `rollback`) para asegurar la integridad de la información.
- **Mapeo ORM**: Definición precisa de tablas, llaves primarias y tipos de datos en las entidades.

### 3. Conectividad y Configuración
- **Conexión a PostgreSQL**: Conexión exitosa y uso correcto de `hbm2ddl.auto` para la gestión del esquema.
- **Gestión de Maven**: Configuración limpia de dependencias sin conflictos de versiones.

### 4. Innovación y Autonomía
- **Relación con los Datos**: La dependencia adicional debe tener un caso de uso real que interactúe con los datos de la base de datos.
- **Propuesta Técnica**: Capacidad de investigación del grupo para integrar herramientas externas de forma autónoma.

---

> [!IMPORTANT]
> **Sustentación Técnica**: Cada equipo deberá explicar las decisiones de diseño, la estructura del código y demostrar el funcionamiento en vivo de todas las características solicitadas.
