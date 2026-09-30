# TriviAlvaro - Proyecto Final de Programación

Este proyecto forma parte del trabajo final de la asignatura **Programación** del ciclo **Desarrollo de Aplicaciones Web (DAW)**. Consiste en una aplicación de trivia multijugador desarrollada en Java, con interfaz gráfica, base de datos y gestión de ficheros, e integra conceptos clave vistos durante el curso.

## Objetivos del Proyecto

- Aplicar de forma práctica los cuatro bloques temáticos principales de la asignatura:
  - Ficheros (JSON)
  - Interfaz Gráfica (Swing)
  - Bases de Datos (MySQL vía JDBC)
  - Hilos (temporizador y procesos concurrentes)
- Consolidar conocimientos de otras asignaturas del ciclo como:
  - Bases de Datos (uso de MySQL)
  - Lenguajes de Marcas (formato JSON)
  - Entornos de Desarrollo (uso de Git y GitHub)

> Proyecto desarrollado de forma guiada en clase: el objetivo era entender cómo se integran ficheros, interfaz gráfica, base de datos e hilos dentro de una misma aplicación.

## Tecnologías Utilizadas

- Java SE 11 o superior
- Swing para la interfaz gráfica
- JDBC + MySQL para la persistencia de datos
- Gson para leer y escribir preguntas desde archivos JSON
- Multithreading para temporizador con cuenta atrás
- Eclipse IDE como entorno de desarrollo
- Git + GitHub para control de versiones

## Estructura del Proyecto

```
src/
│
├── main/               --> Clase principal del programa
├── modelo/             --> Clases Jugador y Pregunta
├── vista/              --> Todas las ventanas del juego (Swing)
├── persistencia/       --> Clase GestorFicheros (JSON)
├── bbdd/               --> Acceso a base de datos MySQL (JDBC)
└── preguntas.json      --> Archivo con preguntas en formato JSON
```

## Funcionalidades Clave

- Inicio de sesión con nombre de usuario
- Lectura de preguntas desde un fichero `.json` estructurado por categorías y niveles
- Temporizador de 15 segundos por pregunta con barra visual y contador numérico
- Cálculo y visualización de estadísticas al finalizar el juego
- Registro de partidas en una base de datos y sistema de ranking

## Créditos y Colaboración

- Autor del proyecto: Álvaro de Vicente
- Asistencia técnica y tutoría: ChatGPT (OpenAI)
- Proyecto guiado paso a paso con enfoque didáctico

## Repositorio

Repositorio oficial del proyecto:  
https://github.com/AlvaroDEVicente/Trivial_DAW

## Licencia

Uso educativo. Todos los derechos reservados.

### IMPORTANTE: Configuración de la base de datos MySQL

Para que el sistema de puntuaciones funcione correctamente, el usuario debe:

1. Tener instalado MySQL en su equipo (por ejemplo, XAMPP, WAMP o instalación directa).
2. Ejecutar el script `instalacion_mysql.sql` incluido en el repositorio. Este script creará automáticamente la base de datos `trivia` y la tabla `estadisticas` necesarias para almacenar resultados.
3. Verificar que las credenciales de conexión indicadas en el archivo `ConexionBD.java` coincidan con las de su sistema (usuario, contraseña, puerto, etc.).

