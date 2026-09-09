# Plantilla para la Planeación de una Iteración con Extreme Programming (XP)

## 1. Datos generales de la iteración

**Proyecto:** Calculadora de Desviación Estándar (Java)

**Equipo:** Equipo de Desarrollo Backend

**Número de iteración:** 1

**Fecha de inicio:** 06/09/2026

**Fecha de término:** 13/09/2026

**Duración de la iteración:** 1 semana

**Cliente / Product Owner:** Usuario / Analista de Datos


---

## 2. Objetivo de la iteración

Describir brevemente qué se espera conseguir al finalizar la iteración.

**Objetivo:**

Construir la primera versión funcional de una aplicación de consola en Java que permita calcular la desviación estándar de un conjunto de datos numéricos. 

El sistema debe permitir la carga de datos mediante un archivo CSV o la captura manual por teclado, aplicando validaciones de tipo de dato y permitiendo al usuario seleccionar si el conjunto representa a una población (N) o a una muestra (n-1).

El objetivo debe expresar un resultado verificable y estar relacionado con la entrega de software funcional.

---

## 3. Situación actual del proyecto

### Funcionalidades disponibles al inicio de la iteración

- Estructura base del proyecto y clase Main inicial.
- Definición de los métodos vacíos en la clase Estadistica y Library1.

### Problemas o restricciones conocidas

- Riesgo de excepciones no controladas al leer archivos o convertir texto a números (`IOException`, `NumberFormatException`).
- Posibles datos corruptos, espacios en blanco o delimitadores mixtos en archivos planos.

### Deuda técnica identificada

- Ausencia de pruebas unitarias (TDD) para la validación matemática pura.
- Acoplamiento de rutas de archivos (hardcoding) sin menú dinámico.

---

# 4. Historias de usuario candidatas

Registrar las historias de usuario consideradas para la iteración.

| ID | Historia de usuario | Prioridad | Estimación | Dependencias |
|---|---|---|---:|---|
| HU-01 | Como usuario quiero cargar un CSV para calcular SD | Alta | 3 pts | Ninguna |
| HU-02 | Como usuario quiero seleccionar una columna del CSV | Alta | 2 pts | HU-01 |
| HU-03 | Como usuario quiero introducir datos manualmente | Alta | 2 pts | Ninguna |
| HU-04 | Como usuario quiero validación de datos para evitar errores | Alta | 3 pts | HU-01, HU-03 |
| HU-05 | Como usuario quiero elegir Población o Muestra | Media | 2 pts | Ninguna |
| HU-06 | Como usuario quiero calcular la desviación estándar | Alta | 5 pts | HU-04, HU-05 |
| HU-07 | Como usuario quiero ver media, número de datos y SD | Media | 1 pt | HU-06 |
| HU-08 | Como usuario quiero ver una vista previa de los datos | Baja | 1 pt | HU-01, HU-03 |
| HU-09 | Como usuario quiero recibir mensajes claros de error | Alta | 2 pts | HU-04 |
| HU-10 | Como usuario quiero un menú para reiniciar el cálculo | Media | 3 pts | Todas |

---

# 5. Selección de historias para la iteración

Después de considerar prioridad, esfuerzo, riesgo y capacidad del equipo, seleccionar las historias que se implementarán.

| ID | Historia | Prioridad | Estimación | Seleccionada |
|---|---|---|---:|:---:|
| HU-01 al HU-10 | Todas las historias de la versión MVP | Alta/Media | 24 pts | ✓  |

### Capacidad estimada del equipo

**Capacidad disponible:** 30 puntos

**Esfuerzo total comprometido:** 24 puntos

¿El trabajo comprometido corresponde razonablemente con la capacidad del equipo?

✓  Sí  
☐ No

**Justificación:**

Se abordó la iteración como un MVP (Minimum Viable Product). La implementación estructurada del menú `do-while` y las clases de utilidad permitió unificar varias historias (HU-04, HU-06, HU-07, HU-08) en el mismo flujo de ejecución.

---

# 6. Detalle de historias de usuario

## Historia HU-03

### Historia

**Como** usuario,

**quiero** introducir manualmente un conjunto de valores numéricos,

**para** calcular la desviación estándar cuando no disponga de un archivo CSV.

### Criterios de aceptación

1. Debe preguntar al usuario la cantidad de datos a introducir.
2. Debe permitir introducir múltiples valores mediante consola.
3. Debe aceptar números enteros y decimales.
4. Debe rechazar entradas no numéricas y solicitar la re-captura sin detener el programa.

### Casos de prueba iniciales

| Caso | Entrada / Condición | Resultado esperado |
|---|---|---|
| CP-01 | Ingresar "3" datos: 10, 20.5, 30 | Arreglo devuelto: ["10", "20.5", "30"] |
| CP-02 | Ingresar texto "abc" en lugar de número | Muestra error y vuelve a pedir el dato actual |
| CP-03 | Ingresar "0" o letras como cantidad inicial | Muestra error y cancela/reinicia la operación |

### Tareas técnicas

| ID | Tarea | Responsable / Pareja | Estado |
|---|---|---|---|
| T-01 | Instanciar `Scanner` con `System.in` | Equipo | Terminado |
| T-02 | Implementar ciclo `while` validando cantidad | Equipo | Terminado |
| T-03 | Validar entrada con `Double.parseDouble()` | Equipo | Terminado |

### Consideraciones técnicas

Se debe capturar la excepción `NumberFormatException` internamente en el ciclo de captura para no romper el flujo de la aplicación.

---

# 7. Planeación de Test-Driven Development (TDD)

Para cada funcionalidad importante, definir al menos los primeros casos de prueba antes de implementar el código.

| Historia | Prueba | Comportamiento esperado | Estado |
|---|---|---|---|
| HU-06 | Calcular Media | Suma total dividida entre N debe ser exacta | ✓  GREEN |
| HU-06 | Calcular SD (Población) | Aplicar división entre N y raíz cuadrada correctamente | ✓  GREEN |
| HU-06 | Calcular SD (Muestra) | Aplicar división entre (n-1) y raíz cuadrada correctamente | ✓  GREEN |
| HU-04 | Inyectar letras al cálculo | El método propaga `NumberFormatException` | ✓  GREEN |

### Ciclo esperado

**RED → GREEN → REFACTOR**

**RED:** escribir una prueba que inicialmente falle.

**GREEN:** implementar el código mínimo necesario para hacer pasar la prueba.

**REFACTOR:** mejorar el diseño del código sin modificar su comportamiento.

---

# 8. Planeación de Pair Programming

### Frecuencia de cambio de roles

Cada 30 minutos (Por cada revisión de método lógico).

### Frecuencia de rotación de parejas

Cada 2 horas / días.

---

# 9. Estándares de codificación

Durante la iteración el equipo utilizará los siguientes estándares:

✓  Convenciones de nomenclatura (CamelCase para variables/métodos, PascalCase para clases)

✓  Formato e indentación uniforme

✓  Métodos con una responsabilidad claramente definida (Clean Architecture)

✓  Evitar duplicación

✓  Uso de constantes para valores significativos (ej. Constante de RUTA de archivo)

✓  Manejo adecuado de excepciones (`try-catch` y `throws` específicos)

✓  Documentación mediante Javadoc cuando corresponda

☐ Pruebas automatizadas (Pendiente configuración de JUnit)

✓  Estándar de commits

### Reglas adicionales

1. Los recursos estáticos y archivos de entrada (.csv) deben situarse en `src/main/resources/` según las convenciones de Maven.
2. Uso de enumeraciones (`enum`) en lugar de cadenas de texto para decisiones lógicas estrictas (Población vs Muestra).
3. Uso de expresiones regulares flexibles (`\\s*[,;\\t|]\\s*`) para garantizar la tolerancia a fallos en separadores.

---

# 10. Estrategia de control de versiones

**Repositorio:** GitLab / GitHub

**Rama principal:** main

### Convención para ramas

`feature/HU-01-lectura-csv`

`feature/HU-03-captura-manual`

`feature/HU-06-calculo-estadistico`

### Convención para mensajes de commit

Ejemplo:
`feat: Agregar cálculo de desviación estándar delegando errores aritméticos`
`fix: Corregir precedencia de operadores en cálculo de muestra (n-1)`

---

# 11. Integración continua

Definir qué deberá verificarse antes de integrar cambios.

✓  El proyecto compila correctamente.

✓  Todas las pruebas automatizadas pasan.

✓  No se introducen errores conocidos.

✓  El código cumple los estándares establecidos.

✓  Se realizó revisión de código.

✓  La nueva funcionalidad satisface sus criterios de aceptación.

### Frecuencia de integración

Diaria, tras la validación de cada Historia de Usuario principal.

---

# 12. Refactoring previsto

Registrar áreas del código que podrían requerir mejora durante la iteración.

| Componente | Problema identificado | Refactoring propuesto | Prioridad |
|---|---|---|---|
| `Main.java` | Lógica espagueti o muy lineal | Extraer menú en `do-while` y llamadas auxiliares | Alta |
| `Estadistica.java` | Fallo de conversión matemática | Quitar `try-catch` interno y delegarlo (throws) a `Main` | Alta |
| `Library1.java` | Riesgo de índice fuera de límite | Cambiar ciclo a `for-each` con contadores de fila manuales | Media |

La refactorización deberá realizarse manteniendo exitosas las pruebas automatizadas.

---

# 13. Riesgos de la iteración

| Riesgo | Probabilidad | Impacto | Acción preventiva |
|---|---|---|---|
| Formato de CSV inconsistente | Alta | Medio | Usar Regex multi-separador para `split` |
| Usuario ingresa letras en lugar de números | Alta | Alto | Manejar `NumberFormatException` |
| Cierre inesperado al no encontrar archivo | Media | Alto | Manejar `IOException` validando ruta base Maven |

---

# 14. Seguimiento diario

| Día | Trabajo realizado | Problemas encontrados | Próximo trabajo |
|---|---|---|---|
| 1 | Estructura base Maven y `Library1` | N/A | Regex y lectura dinámica |
| 2 | Lectura NIO y extracción CSV (HU-01,02) | Manejo dinámico de filas/columnas | Matemáticas y clase `Estadistica` |
| 3 | Métodos `media` y `desviacionEstandar` | Precedencia en Muestra (n-1) | Refactorización de errores (throws) |
| 4 | Captura Manual (HU-03) | Reinicio en fallo de parseo | Integración `main` y menú interactivo |
| 5 | Menú final (HU-08,10) | Formato multilínea printf | Cierre y pruebas finales |

---

# 15. Cambios solicitados durante la iteración

XP acepta que los requerimientos pueden cambiar. Registrar los cambios solicitados y la decisión del equipo.

| Fecha | Cambio solicitado | Historia afectada | Decisión |
|---|---|---|---|
| [Fecha] | Adaptar múltiples separadores en el CSV | HU-01 | Incorporar regex flexible (`\\s*[,;\\t|]\\s*`). |
| [Fecha] | Delegar el error aritmético en lugar de atraparlo silenciosamente | HU-04, HU-06 | Incorporar en la iteración actual para cumplir Clean Architecture. |

---

# 16. Criterios de finalización de una historia

Una historia podrá considerarse terminada cuando:

✓  Cumple todos los criterios de aceptación.

✓  Las pruebas automatizadas son satisfactorias (Pruebas de flujo manuales en consola exitosas).

✓  Se realizó refactoring cuando fue necesario.

✓  El código cumple los estándares acordados.

✓  El código fue integrado en la rama correspondiente.

✓  No existen errores conocidos críticos.

✓  El cliente o responsable funcional acepta el resultado.

---

# 17. Resultado de la iteración

## Historias terminadas

| Historia | Estado | Resultado |
|---|---|---|
| HU-01 a HU-10 | Terminadas | Integración exitosa en un menú cohesivo |

## Historias no terminadas

| Historia | Avance | Razón | Acción siguiente |
|---|---:|---|---|
| N/A | % | N/A | N/A |

---

# 18. Retroalimentación del cliente

**Funcionalidades presentadas:**
Sistema de consola completo con menú principal, carga automática de CSV de recursos de Maven, lectura por teclado validada, cálculo estadístico (población y muestra) y visualización enriquecida.

**Comentarios del cliente:**
Flujo muy claro, excelente manejo de fallos sin cerrar abruptamente el programa y validaciones robustas.

**Cambios solicitados:**
Para versiones futuras, permitir seleccionar la ruta del CSV dinámicamente o implementar pruebas unitarias formales con JUnit.

---

# 19. Métricas de la iteración

| Métrica | Resultado |
|---|---:|
| Historias comprometidas | 10 |
| Historias terminadas | 10 |
| Puntos comprometidos | 24 |
| Puntos completados | 24 |
| Pruebas automatizadas | 0 (Uso de pruebas interactivas de consola) |
| Defectos encontrados | 2 (Excepciones silenciosas, precedencia aritmética) |
| Defectos corregidos | 2 |
| Commits realizados | N/A |

---

# 20. Retrospectiva

## ¿Qué funcionó bien?

1. El desglose paso a paso de la lógica.
2. La aplicación de arquitectura limpia al delegar excepciones (throws).
3. El uso de Expresiones Regulares para dar flexibilidad a la lectura plana.

## ¿Qué problemas encontramos?

1. La precedencia matemática estándar en la división `(n-1)`.
2. Las dificultades al usar un `for-each` sin índices nativos.

## ¿Qué debemos mejorar en la siguiente iteración?

1. Incluir el ciclo TDD con JUnit de forma nativa antes de escribir el método matemático.
2. Permitir configurar la ruta del CSV dinámicamente desde el menú.

## Acción de mejora prioritaria

Implementación estricta de pruebas automatizadas (JUnit) en `src/test/java/`.

**Responsable:** Equipo de desarrollo

---

# 21. Planeación preliminar de la siguiente iteración

### Historias candidatas

| ID | Historia | Prioridad |
|---|---|---|
| HU-11 | Elegir ruta del archivo por consola | Media |
| HU-12 | Pruebas Unitarias automatizadas (TDD) | Alta |
| HU-13 | Guardar un log de resultados (`java.util.logging`) | Baja |

### Deuda técnica pendiente

Implementación del plugin `maven-surefire-plugin` y clases de prueba en JUnit.

### Nuevas necesidades identificadas

Crear una clase dedicada a la impresión/UI en lugar de mezclar todo en `Main`.

---

# Lista de verificación XP de la iteración

Antes de finalizar, verificar cuáles prácticas de XP fueron utilizadas:

✓  Planning Game / planeación mediante historias

✓  User Stories

✓  Small Releases (Enfoque MVP Consola)

✓  Pair Programming

☐ Test-Driven Development (Aplicado lógicamente, pendiente JUnit)

✓  Refactoring (Correcciones a Exception Handling)

✓  Simple Design

✓  Continuous Integration (Validaciones constantes)

✓  Collective Code Ownership

✓  Coding Standards (Uso de convenciones Maven)

✓  Retroalimentación frecuente del cliente

### Reflexión final

**¿De qué manera las prácticas de XP ayudaron al equipo a responder a cambios y mantener la calidad del software durante esta iteración?**

El enfoque de *Simple Design* permitió resolver problemas complejos (lectura, separación) con herramientas base. El *Pair Programming* facilitó la detección temprana de defectos lógicos críticos como la precedencia de los operadores matemáticos o el enmascaramiento silencioso de las excepciones, resultando en un código robusto y preparado para escalarse en la siguiente iteración.