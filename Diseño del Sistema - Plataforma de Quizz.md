# Diseño del Sistema - Plataforma de Quizz Educativo

Este documento detalla las especificaciones de diseño de software y las decisiones arquitectónicas fundamentales adoptadas para el desarrollo del Sistema de Quizz Educativo de Opción Múltiple. 

El sistema ha sido concebido bajo el Paradigma Orientado a Objetos (POO), estructurado mediante el patrón arquitectónico **MVC (Modelo-Vista-Controlador)** y optimizado con el patrón de diseño **Fachada** para garantizar un desacoplamiento efectivo, alta cohesión y una clara separación de responsabilidades.

---

## 1. Elección del Patrón Arquitectónico: MVC

Para evitar el acoplamiento directo entre la interfaz gráfica y el motor de persistencia, el sistema fragmenta sus responsabilidades en tres capas lógicas bien definidas:

### 🟢 Modelo 
Contiene las clases del dominio del problema y encapsula las reglas de negocio, los estados y el acceso a los datos físicos. En nuestro proyecto, el modelo se encuentra constituido estrictamente por:
* `Usuario`: Controla los estados y credenciales de acceso.
* `Quizz`: Gestiona la entidad principal de los cuestionarios maestros.
* `Pregunta`: Maneja de forma atómica los reactivos y su puntuación.
* `Opcion`: Almacena las alternativas lógicas de respuesta.
* `Intento`: Controla la sesión transaccional de juego de cada alumno.
* `RespuestaUsuario`: Persiste de forma síncrona cada selección interactiva.

### 🔵 Vista
Representa la capa de presentación externa con la que interactúa el usuario final en entornos Windows. Está construida utilizando la librería gráfica **Java Swing** y no posee lógica de negocio ni persistencia. Las pantallas proyectadas son:
* `LoginVista`: Ventana de autenticación y registro de alumnos/docentes.
* `MenuPrincipalVista`: Tablero de control desde donde el alumno selecciona los Quizzes disponibles.
* `JuegoQuizzVista`: Interfaz dinámica que renderiza secuencialmente las preguntas (`JLabel`), las opciones múltiples asociadas y los controles de navegación (`JButton`).
* `HistorialResultadosVista`: Pantalla de consulta interactiva de las calificaciones históricas.

### 🟡 Controlador 
Actúa como nexo coordinador. Captura las interacciones y eventos del usuario en las Vistas (mediante clases que implementan `ActionListener`), invoca los servicios del Modelo y actualiza los componentes visuales con los nuevos estados.
* `AutenticacionControlador`: Coordina el flujo de accesos.
* `QuizzJuegoControlador`: Controla los eventos de los botones "Siguiente" y el ciclo de vida del cuestionario activo.

---

## 2. Implementación del Patrón de Diseño: Fachada (Facade)

### Justificación Técnica
La comunicación directa desde los controladores de la Vista hacia las múltiples entidades del Modelo (`Intento`, `RespuestaUsuario`, `Pregunta`) generaría un entramado complejo de dependencias difíciles de mantener. 

Para solucionar esto, se incorporó la clase **`QuizzFachada`** dentro de la capa de control/servicio. Esta clase funciona como un punto único de entrada simplificado que encapsula toda la complejidad transaccional del backend.

### Funcionamiento
Cuando el alumno finaliza el quizz, el controlador no necesita inicializar conexiones de base de datos ni iterar colecciones manualmente; simplemente realiza una llamada atómica a la fachada:
```java
QuizzFachada.procesarCuestionarioCompleto(idUsuario, idQuizz, mapaRespuestas);