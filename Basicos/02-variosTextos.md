# Explicación del código MessageCard con Data Class

Este documento explica el código de una aplicación Android que utiliza **data class** y **Jetpack Compose** para mostrar tarjetas de mensaje.

## Código completo

```kotlin
data class Message(val author: String, val body: String)

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MessageCard(Message("Android", "Jetpack Compose"))
        }
    }
}

@Composable
fun MessageCard(msg: Message) {
    Text(text = msg.author)
    Text(text = msg.body)
}
```

## Data Class Message

```kotlin
data class Message(val author: String, val body: String)
```

### Características:

- **data class**: Tipo especial de clase en Kotlin optimizada para almacenar datos
- **val author**: Propiedad inmutable que almacena el nombre del autor del mensaje
- **val body**: Propiedad inmutable que contiene el contenido del mensaje
- **Beneficios**: Genera automáticamente métodos como `equals()`, `hashCode()`, `toString()` y `copy()`

## Clase MainActivity

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MessageCard(Message("Android", "Jetpack Compose"))
        }
    }
}
```

### Componentes principales:

- **MainActivity**: Actividad principal que hereda de `ComponentActivity`
- **onCreate()**: Método que se ejecuta al crear la actividad
- **setContent {}**: Define el contenido visual usando Compose
- **Message("Android", "Jetpack Compose")**: Crea una instancia del objeto Message con autor "Android" y cuerpo "Jetpack Compose"
- **MessageCard()**: Llama a la función composable pasando el objeto Message como parámetro

## Función MessageCard

```kotlin
@Composable
fun MessageCard(msg: Message) {
    Column {  // <-- Esto define el layout vertical
        Text(text = msg.author)
        Text(text = msg.body)
    }
}
```

### Características:

- **@Composable**: Indica que es una función que puede generar UI
- **msg: Message**: Parámetro que recibe un objeto de tipo Message
- **Text(text = msg.author)**: Muestra el nombre del autor en un componente Text
- **Text(text = msg.body)**: Muestra el contenido del mensaje en otro componente Text
- **Disposición**: Los elementos Text se apilan verticalmente (comportamiento por defecto)

## Resultado visual

La aplicación muestra en pantalla:
```
Android
Jetpack Compose
```

Donde "Android" es el autor y "Jetpack Compose" es el contenido del mensaje, cada uno en una línea separada.

## Conceptos clave

- **Data Class**: Estructura de datos inmutable perfecta para representar información
- **Composable Functions**: Funciones que crean componentes de UI reutilizables
- **Parameter Passing**: Pasar objetos de datos a funciones Composable
- **Text Component**: Elemento básico de Compose para mostrar texto
- **Vertical Layout**: Los componentes se apilan verticalmente por defecto en Compose

## Ventajas de este enfoque

1. **Separación de datos**: La data class separa la lógica de datos de la UI
2. **Reutilización**: MessageCard puede usar cualquier objeto Message
3. **Tipado fuerte**: Kotlin garantiza que los datos sean del tipo correcto
4. **Inmutabilidad**: Los valores no pueden cambiar después de crearse
5. **Legibilidad**: El código es más claro y fácil de mantener