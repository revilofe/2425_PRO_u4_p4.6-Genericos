# Práctica 4.6: GENERICOS

Apóyate en los siguientes recursos para realizar la práctica:

---

## Guía Completa sobre Clases y Funciones Genéricas en Kotlin

En Kotlin, las clases y funciones genéricas son herramientas poderosas para escribir código reutilizable y seguro. Estas permiten que una clase o función trabaje con cualquier tipo de dato sin perder la seguridad de tipos que caracteriza al lenguaje. Vamos a explorar en detalle cómo funcionan, su sintaxis, sus beneficios y ejemplos prácticos aplicados.

---

### **¿Qué son los genéricos?**

Un tipo genérico es un marcador de posición que se define utilizando `<>`. Este marcador permite que una clase, interfaz o función se adapte a diferentes tipos sin que sea necesario escribir implementaciones específicas para cada tipo.

Por ejemplo:

- `List<T>`: Una lista genérica que puede almacenar elementos de cualquier tipo, como `List<String>` o `List<Int>`.
- `Map<K, V>`: Un mapa genérico que define un tipo para las claves (`K`) y otro para los valores (`V`).

Los genéricos se utilizan ampliamente en las estructuras de datos de Kotlin, como listas y mapas, y también pueden implementarse en nuestras propias clases y funciones para mayor flexibilidad. Por ejemplo, en una lista genérica como `List<String>`, puedes almacenar solo elementos de tipo `String`, lo que evita errores en tiempo de ejecución. Similarmente, los mapas como `Map<Int, String>` permiten asociar claves de tipo `Int` con valores de tipo `String`, asegurando la consistencia del tipo de datos.

---

### **Ventajas de usar genéricos**

1. **Reutilización de código:** Se puede escribir una vez y usar para cualquier tipo.
2. **Seguridad de tipos:** Los errores de tipo se detectan en tiempo de compilación, no en tiempo de ejecución.
3. **Claridad y legibilidad:** Al definir claramente los tipos genéricos, el código es más comprensible.
4. **Flexibilidad:** Permiten trabajar con diferentes tipos de datos sin necesidad de duplicar la lógica del código.

Los genéricos son esenciales para escribir código escalable y modular en proyectos grandes. Por ejemplo, imagina un sistema de gestión de datos en el que diferentes módulos procesan información de diversos tipos (usuarios, productos, pedidos). Utilizando genéricos, podrías implementar un repositorio genérico `Repositorio<T>` que maneje todas las operaciones CRUD de forma uniforme. Esto no solo reduce el código duplicado, sino que también permite agregar nuevas entidades al sistema sin modificar la estructura base, promoviendo una modularidad efectiva y facilitando el mantenimiento.

---

### **Definiendo Clases Genéricas**

Las clases genéricas permiten trabajar con datos de cualquier tipo y son ideales para construir estructuras de datos o utilidades flexibles.

#### **Sintaxis**
```kotlin
class ClaseGenerica<T> {
    // Uso del tipo genérico T dentro de la clase
    private var valor: T? = null

    fun establecerValor(valor: T) {
        this.valor = valor
    }

    fun obtenerValor(): T? {
        return valor
    }
}
```

#### **Ejemplo detallado**

Supongamos que queremos una clase contenedor que almacene un valor de cualquier tipo:

```kotlin
class Contenedor<T>(private var contenido: T) {

    // Método para obtener el valor almacenado
    fun obtenerContenido(): T {
        return contenido
    }

    // Método para actualizar el valor almacenado
    fun actualizarContenido(nuevoContenido: T) {
        contenido = nuevoContenido
    }
}

fun main() {
    // Instancia para almacenar un String
    val contenedorString = Contenedor("Hola Kotlin")
    println(contenedorString.obtenerContenido()) // Salida: Hola Kotlin

    contenedorString.actualizarContenido("Nuevo Valor")
    println(contenedorString.obtenerContenido()) // Salida: Nuevo Valor

    // Instancia para almacenar un Int
    val contenedorInt = Contenedor(42)
    println(contenedorInt.obtenerContenido()) // Salida: 42
}
```

En este ejemplo:
- `T` actúa como un marcador de posición para el tipo.
- Al crear una instancia de `Contenedor`, especificamos el tipo que queremos que maneje (por ejemplo, `String` o `Int`).

Este enfoque elimina la necesidad de escribir clases específicas para cada tipo de dato, reduciendo la redundancia y aumentando la flexibilidad del código. Por ejemplo, en un sistema de inventario, podrías crear una clase genérica `GestorInventario<T>` para manejar diferentes tipos de productos como libros, electrónicos o ropa. Al usar genéricos, puedes definir una sola clase para todas estas categorías, garantizando que los mismos métodos como `agregarProducto`, `eliminarProducto` o `listarInventario` funcionen para cualquier tipo de producto sin duplicar lógica.

---

### **Restricciones de tipos (Bounded Generics)**

A veces, queremos limitar los tipos que un genérico puede aceptar. Esto se hace con la palabra clave `:`, indicando que el tipo genérico debe heredar de una clase o implementar una interfaz específica.

#### **Sintaxis**
```kotlin
class ClaseRestringida<T : Number>(private val numero: T) {
    fun obtenerDoble(): Double {
        return numero.toDouble() * 2
    }
}
```

#### **Ejemplo**
```kotlin
fun main() {
    val claseInt = ClaseRestringida(10) // Acepta Int
    println(claseInt.obtenerDoble()) // Salida: 20.0

    val claseDouble = ClaseRestringida(5.5) // Acepta Double
    println(claseDouble.obtenerDoble()) // Salida: 11.0

    // val claseString = ClaseRestringida("Texto") // ERROR: String no es subclase de Number
}
```

En este caso, `T` solo puede ser un tipo que herede de `Number`, como `Int`, `Float`, o `Double`. Esto asegura que los tipos usados cumplan con ciertos requisitos específicos.

---

### **Funciones Genéricas**

Las funciones genéricas permiten parametrizar el tipo de dato que manejan, ofreciendo una gran flexibilidad y reutilización de código.

#### **Sintaxis**
```kotlin
fun <T> imprimirElemento(elemento: T) {
    println(elemento)
}
```

#### **Ejemplo**
```kotlin
fun <T> intercambiarValores(pareja: Pair<T, T>): Pair<T, T> {
    return Pair(pareja.second, pareja.first)
}

fun main() {
    val pareja = Pair(1, 2)
    val parejaInvertida = intercambiarValores(pareja)
    println(parejaInvertida) // Salida: (2, 1)

    val parejaStrings = Pair("Kotlin", "Java")
    val parejaStringsInvertida = intercambiarValores(parejaStrings)
    println(parejaStringsInvertida) // Salida: (Java, Kotlin)
}
```

En este ejemplo, la función `intercambiarValores` trabaja con cualquier tipo gracias a `T`. Esto simplifica la implementación de algoritmos genéricos que funcionan con distintos tipos de datos.

---

### **Genéricos con Variancia**

La variancia define cómo se comportan los genéricos con la jerarquía de tipos:

1. **Covarianza (`out`):** Permite que un tipo genérico sea sustituido por sus subtipos.
2. **Contravarianza (`in`):** Permite que un tipo genérico sea sustituido por sus supertipos.
3. **Invarianza:** No permite sustitución de tipos.

#### **Ejemplo: Covarianza**
```kotlin
class Caja<out T>(private val contenido: T) {
    fun obtenerContenido(): T {
        return contenido
    }
}

fun procesarCaja(caja: Caja<Any>) {
    println(caja.obtenerContenido())
}

fun main() {
    val cajaString = Caja("Texto en una caja")
    procesarCaja(cajaString) // Funciona debido a la covarianza
}
```

En este caso, `Caja<out T>` permite que `Caja<String>` sea tratada como `Caja<Any>`.

#### **Ejemplo: Contravarianza**
```kotlin
class Procesador<in T> {
    fun procesar(input: T) {
        println("Procesando: $input")
    }
}

fun main() {
    val procesador: Procesador<Number> = Procesador<Int>()
    procesador.procesar(10) // Acepta Int porque Int es un subtipo de Number
}
```

La variancia proporciona un control preciso sobre cómo los tipos pueden ser utilizados, garantizando seguridad y flexibilidad. Por ejemplo, la covarianza (`out`) permite que un tipo genérico sea sustituido por sus subtipos, como en `List<out T>`, donde `List<String>` puede ser tratada como `List<Any>`. Por otro lado, la contravarianza (`in`) permite que un tipo genérico sea sustituido por sus supertipos, como en `Comparator<in T>`, donde un `Comparator<Number>` puede comparar elementos de tipo `Int`. Estas diferencias hacen que el código sea más flexible y seguro en sistemas complejos.

---

### **Aplicaciones de los Genéricos en Kotlin**

1. **Colecciones:** Las listas, mapas y conjuntos en Kotlin son genéricos, lo que garantiza que solo se almacenen tipos esperados.
   ```kotlin
   val listaStrings: List<String> = listOf("Kotlin", "Java")
   val mapa: Map<Int, String> = mapOf(1 to "Uno", 2 to "Dos")
   ```

2. **Clases Utilitarias:** Crear clases o interfaces reutilizables para diversas tareas.
   ```kotlin
   interface Repositorio<T> {
       fun agregar(elemento: T)
       fun obtenerTodos(): List<T>
   }
   ```

3. **Algoritmos Genéricos:** Escribir funciones o clases que funcionen con cualquier tipo.
   ```kotlin
   fun <T : Comparable<T>> encontrarMayor(lista: List<T>): T? {
       return lista.maxOrNull()
   }
   ```

---

### **Ejercicios Prácticos**

#### **Ejercicio 1: Implementa una Clase Genérica para una Pila (Stack)**
Crea una clase genérica `Pila<T>` que permita:
- Apilar elementos (`push`).
- Desapilar elementos (`pop`).
- Obtener el elemento en la cima de la pila sin eliminarlo (`top`).

**Pistas:**
- Usa una lista mutable (`MutableList`) para almacenar los elementos internamente.
- Asegúrate de manejar casos donde la pila esté vacía al intentar desapilar o mirar la cima.

---

#### **Ejercicio 2: Restringe el Tipo Genérico a Números**
Escribe una función genérica `calcularPromedio` que reciba una lista de números (`List<T>`) y devuelva el promedio. Asegúrate de que el tipo genérico esté restringido a subtipos de `Number`.

**Pistas:**
- Usa la restricción `T : Number` en la definición de la función.
- Convierte los números a `Double` utilizando `toDouble()` para realizar cálculos de forma uniforme.

---

#### **Ejercicio 3: Compara Dos Objetos Genéricos**
Crea una función genérica `esMayor` que reciba dos elementos genéricos (`a` y `b`) y devuelva `true` si el primero es mayor que el segundo. Asegúrate de que los elementos implementen la interfaz `Comparable<T>`.

**Pistas:**
- Usa la restricción `T : Comparable<T>`.
- Implementa la comparación utilizando el operador `compareTo`.

---

### **Conclusión**

Los genéricos en Kotlin son una herramienta esencial para escribir código robusto, flexible y seguro. 
- Entender cómo funcionan las clases y funciones genéricas te permite crear APIs reutilizables.
- Las restricciones y la variancia ayudan a controlar qué tipos son aceptados.

Con estas herramientas, puedes aprovechar al máximo la seguridad de tipos y la expresividad de Kotlin para crear aplicaciones escalables y mantenibles. Como próximos pasos, podrías explorar conceptos relacionados como 'sealed classes' para modelar jerarquías de datos de forma segura o aprender sobre patrones de diseño genéricos como repositorios y servicios genéricos. Estas ideas complementan el uso de genéricos y amplían su aplicación en proyectos complejos.



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
