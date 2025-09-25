# Data Classes en Kotlin - Explicación Detallada

Este documento explica en profundidad la línea de código:

```kotlin
data class Message(val author: String, val body: String)
```

## ¿Qué es una Data Class?

Una **data class** es un tipo especial de clase en Kotlin diseñada específicamente para **almacenar datos**. Es una forma concisa de crear clases que principalmente contienen información.

## Desglose de la sintaxis

### `data class`
- **Palabra clave especial** que le dice a Kotlin que genere automáticamente métodos útiles
- Diferente de una `class` normal

### `Message`
- **Nombre de la clase** - representa un mensaje en nuestra aplicación
- Sigue la convención PascalCase

### `(val author: String, val body: String)`
- **Constructor primario** - se define directamente en la declaración de la clase
- **`val`**: Las propiedades son **inmutables** (no pueden cambiar después de crearse)
- **`author: String`**: Primera propiedad, almacena quién escribió el mensaje
- **`body: String`**: Segunda propiedad, contiene el contenido del mensaje

## ¿Qué genera automáticamente Kotlin?

Cuando usas `data class`, Kotlin crea estos métodos por ti:

### 1. `equals()` y `hashCode()`

```kotlin
val msg1 = Message("Juan", "Hola")
val msg2 = Message("Juan", "Hola")
println(msg1 == msg2) // true - compara el contenido, no la referencia
```

### 2. `toString()`

```kotlin
val msg = Message("Ana", "¿Cómo estás?")
println(msg) // Imprime: Message(author=Ana, body=¿Cómo estás?)
```

### 3. `copy()`

```kotlin
val original = Message("Carlos", "Mensaje original")
val copia = original.copy(body = "Mensaje modificado")
// copia = Message("Carlos", "Mensaje modificado")
```

### 4. `componentN()` (destructuring)

```kotlin
val msg = Message("Luis", "Texto del mensaje")
val (autor, contenido) = msg // Destructuring
println(autor) // "Luis"
println(contenido) // "Texto del mensaje"
```

## Comparación: Data Class vs Clase Normal

### Con data class (1 línea):

```kotlin
data class Message(val author: String, val body: String)
```


## Reglas y limitaciones de Data Classes

1. **Al menos un parámetro** en el constructor primario
2. **Todos los parámetros deben ser `val` o `var`**
3. **No pueden ser abstractas, abiertas, selladas o internas**
4. **Solo las propiedades del constructor primario** se usan en `equals()`, `hashCode()`, etc.

## Ejemplo de uso en la aplicación

```kotlin
// Crear instancias
val mensaje1 = Message("Android", "Jetpack Compose")
val mensaje2 = Message("Kotlin", "Es genial")

// Acceder a las propiedades
println(mensaje1.author) // "Android"
println(mensaje1.body)   // "Jetpack Compose"

// Crear una copia modificada
val mensajeEditado = mensaje1.copy(body = "Compose es increíble")
```

## ¿Por qué usar Data Class aquí?

1. **Simplicidad**: Una línea vs muchas líneas de código
2. **Inmutabilidad**: `val` hace que los datos no cambien accidentalmente
3. **Comparación**: Puedes comparar mensajes por contenido
4. **Debugging**: `toString()` automático facilita el debugging
5. **Performance**: `hashCode()` optimizado para uso en colecciones

## Casos de uso comunes

Las data classes son perfectas para representar:

- **Modelos de datos**: Usuario, Producto, Mensaje, etc.
- **Respuestas de API**: Datos que recibes de servicios web
- **Configuraciones**: Settings, preferencias, etc.
- **Estados**: Estados de UI, estados de aplicación
- **DTOs**: Data Transfer Objects entre capas

## Ejemplos adicionales

```kotlin
// Usuario de una aplicación
data class User(val id: Int, val name: String, val email: String)

// Producto de e-commerce
data class Product(val id: String, val name: String, val price: Double)

// Coordenadas geográficas
data class Location(val latitude: Double, val longitude: Double)

// Estado de loading
data class LoadingState(val isLoading: Boolean, val error: String? = null)
```

## Conclusión

La data class `Message(val author: String, val body: String)` es una forma extremadamente eficiente de crear una estructura de datos que:

- Almacena información de un mensaje (autor y contenido)
- Proporciona métodos útiles automáticamente
- Mantiene el código limpio y conciso
- Facilita el trabajo con los datos en toda la aplicación

Es la elección perfecta para representar datos estructurados en Kotlin.