# Práctica 4.5: EXPRESIONES REGULARES

Apóyate en los siguientes recursos para realizar la práctica:

### Resumen práctico sobre expresiones regulares en Kotlin

Las expresiones regulares (regex) son patrones utilizados para buscar o manipular cadenas de texto. Kotlin hereda las capacidades de regex de Java, ofreciendo una API rica y funcional. Aquí tienes los elementos clave y cómo utilizarlos en Kotlin:

#### 1. **Creación de patrones**
```kotlin
val regex = Regex("patrón")
val match = regex.containsMatchIn("texto a analizar")
```

#### 2. **Métodos comunes**
- **`matches`**: Comprueba si una cadena coincide completamente con el patrón.
- **`find`**: Busca la primera coincidencia.
- **`findAll`**: Encuentra todas las coincidencias.
- **`replace`**: Reemplaza las coincidencias.
- **`split`**: Divide una cadena en partes basándose en el patrón.

#### 3. **Elementos principales de un patrón**
- **Letras y números**: Coinciden literalmente (`a`, `1`).
- **Metacaracteres**:
  - `.`: Cualquier carácter.
  - `\d`: Un dígito.
  - `\w`: Un carácter alfanumérico.
  - `\s`: Un espacio.
- **Cuantificadores**:
  - `*`: 0 o más.
  - `+`: 1 o más.
  - `?`: 0 o 1.
  - `{n,m}`: Entre `n` y `m` repeticiones.
- **Grupos y capturas**:
  - `(abc)`: Grupo capturable.
  - `(?:abc)`: Grupo no capturable.

#### 4. **Ejemplo básico**
```kotlin
fun main() {
    val regex = Regex("\\d{3}-\\d{2}-\\d{4}") // Formato: 123-45-6789
    val input = "Mi número es 123-45-6789."
    println(regex.containsMatchIn(input)) // true
}
```

Por último, hay cientos de paginas que te pueden ayudar. Un ejemplo de una de ella es: [https://regex101.com/](https://regex101.com/). No olvides configurarla para que soporte las expresiones regulares al estilo `java`. 

---

---


### Ejercicios propuestos

#### 1. **Validar un correo electrónico**
Escribe un programa que determine si una cadena tiene el formato correcto de un correo electrónico. Recuerda que un correo tiene las siguientes partes:
1. **Usuario**: Puede contener letras, números, puntos (`.`), guiones (`-`) y signos de suma (`+`).
2. **Dominio**: Está compuesto por letras, números, y puede incluir puntos para subdominios.
3. **Extensión**: Siempre comienza con un punto (`.`) seguido de dos o más letras.

Pista:
- Usa `^[...]` para asegurar que el patrón comience desde el principio.
- Los caracteres alfanuméricos y especiales para el usuario pueden representarse con un conjunto.
- No olvides el carácter `@` para separar usuario y dominio.

---

#### 2. **Buscar números en un texto**
En este ejercicio, deberás extraer todos los números que aparezcan en un texto dado. Por ejemplo, de "Hay 3 gatos y 15 perros", deberías obtener `[3, 15]`.

Pista:
- Utiliza `\\d+` para encontrar uno o más dígitos consecutivos.
- Usa `Regex.findAll` para obtener todas las coincidencias en lugar de detenerte en la primera.

---

#### 3. **Reemplazar palabras prohibidas**
Crea un programa que reemplace una palabra específica como "mala" por "***". Asegúrate de que solo se reemplacen coincidencias exactas de la palabra, no partes de otras palabras (por ejemplo, "malabar" no debe ser reemplazada).

Pista:
- Usa `\\b` para indicar límites de palabra al inicio y al final del patrón.
- La opción `RegexOption.IGNORE_CASE` te permitirá hacer que la búsqueda sea insensible a mayúsculas y minúsculas.

---

#### 4. **Dividir un texto por comas o puntos**
Escribe un programa que divida un texto en partes utilizando comas (`,`) o puntos (`.`) como delimitadores. Por ejemplo, el texto `"Kotlin, es genial. Aprender, a programar."` debería dividirse en `["Kotlin", "es genial", "Aprender", "a programar"]`.

Pista:
- Usa un conjunto de caracteres para indicar que tanto la coma como el punto son válidos delimitadores (`[,.]`).
- Recuerda que puedes usar `.split(regex)` para dividir la cadena en Kotlin.

---

#### 5. **Extraer fechas en formato `dd/mm/yyyy`**
En este ejercicio, deberás encontrar todas las fechas en un texto con el formato `dd/mm/yyyy` y convertirlas al formato ISO `yyyy-mm-dd`. Por ejemplo, de `"Hoy es 25/01/2025 y mañana será 26/01/2025"`, obtendrás `["2025-01-25", "2025-01-26"]`.

Pista:
- Utiliza grupos de captura para dividir las partes del patrón: `(\\d{2})` para el día y el mes, y `(\\d{4})` para el año.
- Después de encontrar las coincidencias, manipula los grupos capturados para reorganizar el formato.


---

> ATENCIÓN: DURANTE LA DOCUMENTACIÓN DE LA PRÁCTICA, ELIMINA TODO AQUELLO QUE NO APLIQUE. PEEEEEEEROOOOOOO, ANTES DE ELIMINAR ALGO, PIENSA SI APLICA O NO.

---

# Título de la Actividad

## Identificación de la Actividad

- **ID de la Actividad:** [ID de la actividad]
- **Módulo:** [Nombre del módulo] (`PROG`, `IS`, `EDES`, etc.)
- **Unidad de Trabajo:** [Número y nombre de la unidad de trabajo]
- **Fecha de Creación:** [Fecha de creación]
- **Fecha de Entrega:** [Fecha de entrega]
- **Alumno(s):**
  - **Nombre y Apellidos:** [Nombre y Apellidos del alumno o integrantes del grupo]
  - **Correo electrónico:** [Correo electrónico g.educaand.es]
  - **Iniciales del Alumno/Grupo:** [Iniciales del alumno o del grupo]

## Descripción de la Actividad

[Descripción detallada de la actividad, objetivos, y contexto necesario para comprenderla. Explicar en qué consiste la actividad y qué se espera que el alumno desarrolle o implemente.]

## Instrucciones de Compilación y Ejecución

1. **Requisitos Previos:**

   - [Lenguaje de programación y versión]
   - [Entorno de desarrollo o dependencias necesarias]
2. **Pasos para Compilar el Código:**

   ```bash
   [Comando para compilar el código]
   ```
3. **Pasos para Ejecutar el Código:**

   ```bash
   [Comando para ejecutar la aplicación]
   ```
4. **Ejecución de Pruebas:**

   ```bash
   [Comandos para ejecutar pruebas, si las hubiera]
   ```

## Desarrollo de la Actividad

### Descripción del Desarrollo

[Explicación de cómo se ha abordado el desarrollo de la actividad, incluyendo las decisiones de diseño, estructura del código y enfoque de resolución de problemas. Se recomienda adjuntar diagramas o capturas de pantalla si es necesario.]

### Código Fuente

[Aquí se incluirá un enlace directo a los archivos de código fuente en el repositorio, por ejemplo, si se está usando GitHub: `src/main.kt` o algún enlace directo.]

[Si hay varios ejercicios, habrá una documentación, por cada uno de los ejercicios.]
[Por cada ejercicio, habrá enlaces embebidos de código a las clases principales y programa principal `main` ]

### Ejemplos de Ejecución

- **Entrada 1:** Descripción de la entrada y valor de prueba.
- **Salida Esperada 1:** Explicación de la salida esperada y el resultado de la prueba.

### Resultados de Pruebas

[Aquí se detallará cómo se ha verificado la funcionalidad del código, incluyendo resultados de pruebas automatizadas o manuales, en caso de que las haya.]

## Documentación Adicional

- **Manual de Usuario:** [Enlace a la documentación del usuario, si existe]
- **Autorización de Permisos:** Verificar que el profesor tenga permisos de lectura en el repositorio para revisar el código.

## Conclusiones

[Resumen de las conclusiones alcanzadas al desarrollar la actividad, las lecciones aprendidas, y posibles mejoras que se puedan implementar en futuras entregas.]

## Referencias y Fuentes

[Aquí se listarán las fuentes consultadas para el desarrollo de la actividad, tales como documentación oficial, artículos, o cualquier recurso externo relevante.]

### Notas Adicionales:

1. **Nombres de Archivos y Repositorios:**
   - Asegúrate de que el nombre del archivo o repositorio siga la estructura definida: `XXX-idActividad-Iniciales`.
2. **Permisos:**
   - Verifica que el profesor tenga los permisos necesarios para acceder al repositorio o documento.
3. **Formato:**
   - Si se entrega en formato PDF o Google Docs, asegúrate de cumplir con el mínimo y máximo de folios establecidos.
4. **Compilación y Ejecución:**
   - Detalla claramente cómo compilar y ejecutar el código, incluyendo las instrucciones en el archivo `README.md`.
