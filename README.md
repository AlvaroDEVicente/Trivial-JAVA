# TriviAlvaro · Juego de preguntas en Java

<p>
  <img src="https://img.shields.io/badge/Java-Swing-0A0A0E?style=flat-square&logo=openjdk&logoColor=white" alt="Java con Swing">
  <img src="https://img.shields.io/badge/MySQL-JDBC-0A0A0E?style=flat-square&logo=mysql&logoColor=4479A1" alt="MySQL con JDBC">
  <img src="https://img.shields.io/badge/JSON-Gson-0A0A0E?style=flat-square" alt="JSON con Gson">
  <img src="https://img.shields.io/badge/hilos-temporizador-0A0A0E?style=flat-square" alt="Hilos">
</p>

Aplicación de escritorio de preguntas y respuestas con temporizador por pregunta y ranking de jugadores. Es mi proyecto final de **Programación de 1.º de DAW**, y reúne en una sola aplicación los cuatro bloques de la asignatura: **ficheros, interfaz gráfica, bases de datos e hilos**.

## Cómo se juega

1. El jugador introduce su nombre; no se puede empezar con el campo vacío.
2. Desde el menú empieza la partida o consulta el ranking.
3. Cada pregunta tiene **cuatro opciones y 15 segundos** para responder, con una barra de tiempo y un contador.
4. Tras responder, la aplicación indica si ha acertado y, si no, cuál era la respuesta correcta. A los dos segundos pasa sola a la siguiente.
5. Al terminar se muestra la puntuación, se guarda la partida y el jugador entra en el **ranking de los 10 mejores**.

## Cómo está hecho

### Preguntas desde JSON

Las 30 preguntas viven en `preguntas.json`, cada una con su enunciado, opciones, respuesta correcta, categoría y nivel. `GestorFicheros` las carga con **Gson**, que convierte el JSON directamente en una lista de objetos `Pregunta` usando `TypeToken`. Así, añadir o cambiar preguntas no obliga a tocar el código. Al empezar cada partida se barajan con `Collections.shuffle`, de modo que nunca salen en el mismo orden.

### Temporizador con hilos

La cuenta atrás de cada pregunta corre en un **hilo propio**, para que la interfaz no se congele mientras pasa el tiempo. Ese hilo nunca toca los componentes de Swing directamente: cada actualización de la barra y del contador se envía al hilo de la interfaz con `SwingUtilities.invokeLater`, que es la forma segura de hacerlo en Swing.

- Si el jugador responde antes de tiempo, el hilo se detiene con `interrupt()`.
- Si se acaba el tiempo, la pregunta cuenta como fallada y se muestra la respuesta correcta.
- La pausa de dos segundos antes de la siguiente pregunta usa un `javax.swing.Timer`, que ya se ejecuta en el hilo de la interfaz.

### Interfaz con Swing

Cinco ventanas, cada una en su clase: acceso, menú, juego, resultado y ranking. Cada categoría de pregunta tiene su propio color, para que el jugador la identifique de un vistazo.

### Partidas y ranking en MySQL

Cada partida se guarda en la tabla `estadisticas` (nombre, puntuación y fecha) mediante **JDBC**. El acceso a datos está separado en clases DAO (`EstadisticasDAO` y `RankingDAO`). Todas las consultas usan `PreparedStatement` y las conexiones se cierran solas con `try-with-resources`. El ranking es una consulta de los 10 mejores resultados ordenados por puntuación.

## Estructura

```
src/
├── main/          Punto de entrada de la aplicación
├── modelo/        Jugador y Pregunta
├── vista/         Ventanas Swing: acceso, menú, juego, resultado y ranking
├── persistencia/  GestorFicheros: lectura del JSON con Gson
└── bbdd/          ConexionBD y los DAO de estadísticas y ranking (JDBC)
preguntas.json          Banco de preguntas
instalacion_mysql.sql   Crea la base de datos y la tabla
```

La separación en paquetes sigue el patrón **modelo-vista** con una capa de persistencia aparte: las ventanas no escriben SQL ni leen ficheros, se lo piden a sus clases.

## Ejecutarlo en local

1. Ejecuta `instalacion_mysql.sql` en MySQL (por ejemplo, con XAMPP). Crea la base de datos `trivia` y la tabla `estadisticas`.
2. Revisa el usuario y la contraseña en `src/bbdd/ConexionBD.java`.
3. Añade al proyecto las librerías **Gson** y **MySQL Connector/J**.
4. Ejecuta la clase `Main`. Requiere Java 17 o superior (usa expresiones `switch` con flecha).

---

Proyecto final de Programación · 1.º de DAW · [Álvaro de Vicente](https://github.com/AlvaroDEVicente)
