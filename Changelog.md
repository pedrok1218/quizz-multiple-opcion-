# Registro de Cambios (Changelog) - Sistema de Quizz Educativo

Este archivo registra de forma cronológica todos los cambios, mejoras, migraciones y correcciones realizadas en la documentación, diseño arquitectónico e implementación del Sistema de Quizz Educativo (*"Maratón de Cine y Películas Taquilleras"*).

El objetivo es mantener un historial técnico riguroso de las versiones del proyecto para el control de la asignatura en el Profesorado de Informática.

---

## [1.1.0] - 2026-06-17

### Añadido
* **Diseño Arquitectónico:** Incorporación formal del patrón arquitectónico **MVC (Modelo-Vista-Controlador)** para dividir estrictamente la presentación de la lógica de negocio.
* **Patrón de Diseño:** Implementación del patrón **Fachada (Facade)** mediante la clase estructurada `QuizzFachada` para simplificar y unificar las transacciones complejas hacia el backend.
* **Capa de Presentación (Vista):** Proyección e inclusión en el diseño de las interfaces gráficas construidas con **Java Swing** (`LoginVista`, `MenuPrincipalVista` y `JuegoQuizzVista`).
* **Capa de Mediación (Controlador):** Diseño de los manejadores de eventos y escuchadores (`AutenticacionControlador` y `QuizzJuegoControlador`).
* **Documentación Técnica:** Creación del informe explicativo global `Diseño del Sistema - Plataforma de Quizz.MD` y las guías arquitectónicas en formato Markdown para el repositorio.

### Modificado
* **Diagrama de Clases:** Se actualizó el modelo orientado a objetos en PlantUML para reflejar la separación en paquetes (`modelo`, `vista`, `controlador`) y la adición de la firma detallada de métodos funcionales con sus modificadores de visibilidad, parámetros y tipos de retorno.
* **Especificación de Requisitos:** Ajuste en el documento **ESRE** (bajo norma IEEE 830) para integrar los nuevos Requisitos No Funcionales de arquitectura e interfaces de usuario Swing.
* **Casos de Uso:** Actualización del flujo del caso de uso principal `CU-02: Resolver Cuestionario` para visibilizar la intervención directa de los controladores y los métodos de la fachada.

### Corregido
* **Encapsulamiento:** Se corrigió la visibilidad de los atributos del modelo de clases de público a privado (`-`), garantizando la integridad de los datos mediante métodos accesores.

---

## [1.0.0] - 2026-06-17

### Añadido
* **Persistencia Física (Base de Datos):** Diseño e implementación del script DDL en **MySQL** para el esquema relacional `sistema_quizz` ejecutado localmente en entornos XAMPP.
* **Estructura de Tablas:** Creación y normalización en Tercera Forma Normal (3FN) de las 6 tablas esenciales: `USUARIO`, `QUIZZ`, `PREGUNTA`, `OPCION`, `INTENTO` y `RESPUESTA_USUARIO`.
* **Integridad Referencial:** Configuración de restricciones de clave foránea avanzadas utilizando comportamientos destructivos controlados (`ON DELETE CASCADE` en cascada para preguntas/opciones y `ON DELETE RESTRICT` para salvaguardar el historial de usuarios).
* **Especificación Técnica Inicial:** Migración formal de los borradores conceptuales independientes (`ESRE.docx`, `Casos de Uso.docx`, `Diagrama de clases.docx`, `Base de datos.docx` y `TAD.docx`) a archivos técnicos Markdown estructurados para la raíz del proyecto.
* **Temática Pedagógica:** Definición del banco de reactivos orientados a la evaluación interactiva de la *"Maratón de Cine y Películas Taquilleras"*.

### Corregido
* **Normalización de Datos:** Eliminación de dependencias transitivas en el diseño conceptual del MER original. Se resolvió la redundancia de almacenamiento mediante la separación estricta de la tabla transaccional intermedia `RESPUESTA_USUARIO` con una restricción `UNIQUE` compuesta.

---

## [0.1.0] - 2026-06-16

### Añadido
* **Fase de Abstracción y Concepción:** Inicio del proyecto académico para la gestión automatizada de evaluaciones de opción múltiple con corrección síncrona.
* **Definición Teórica (TAD):** Diseño matemático del Tipo Abstracto de Datos `TAD Quizz` estableciendo el sustrato de colecciones indexadas y las firmas operacionales básicas (`crearQuizz`, `agregarPregunta`, `evaluarRespuesta`).
* **Modelado Conceptual:** Primer borrador del Modelo Entidad-Relación y definición de las características de los actores del sistema (Docente/Administrador y Estudiante/Alumno).
* **Selección Tecnológica:** Decisión de implementar la solución utilizando el lenguaje de programación **Java** bajo el Paradigma Orientado a Objetos (POO).