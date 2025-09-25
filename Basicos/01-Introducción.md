# Explicación del código Android con Jetpack Compose

Este documento explica el código de una aplicación básica de Android desarrollada en **Kotlin con Jetpack Compose**.

## Código completo

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            HolaMundoTheme {
                Scaffold(modifier = Modifier.fillMaxSize()) { innerPadding ->
                    Greeting(
                        name = "Android",
                        modifier = Modifier.padding(innerPadding)
                    )
                }
            }
        }
    }
}

@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Text(
        text = "Hello $name!",
        modifier = modifier
    )
}

@Preview(showBackground = true)
@Composable
fun GreetingPreview() {
    HolaMundoTheme {
        Greeting("Android")
    }
}
```

## Clase MainActivity

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            // Contenido de la interfaz
        }
    }
}
```

### Componentes principales:

- **MainActivity**: Es la actividad principal de la app, hereda de `ComponentActivity`
- **onCreate()**: Método que se ejecuta cuando se crea la actividad
- **enableEdgeToEdge()**: Permite que la app use toda la pantalla, incluyendo las áreas del notch/barras de sistema
- **setContent {}**: Define el contenido visual usando Compose en lugar del tradicional XML

## Estructura del contenido

```kotlin
HolaMundoTheme {
    Scaffold(modifier = Modifier.fillMaxSize()) { innerPadding ->
        Greeting(
            name = "Android",
            modifier = Modifier.padding(innerPadding)
        )
    }
}
```

### Elementos de la estructura:

- **HolaMundoTheme**: Aplica el tema visual personalizado de la app
- **Scaffold**: Proporciona la estructura básica de la pantalla (como AppBar, FloatingActionButton, etc.)
- **fillMaxSize()**: Hace que ocupe toda la pantalla disponible
- **innerPadding**: Padding automático para evitar solapamientos con elementos del sistema

## Función Greeting

```kotlin
@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Text(
        text = "Hello $name!",
        modifier = modifier
    )
}
```

### Características:

- **@Composable**: Indica que es una función de Compose que puede generar UI
- Recibe un nombre como parámetro y muestra "Hello [nombre]!"
- **modifier**: Permite aplicar estilos y modificaciones desde el exterior

## Preview

```kotlin
@Preview(showBackground = true)
@Composable
fun GreetingPreview() {
    HolaMundoTheme {
        Greeting("Android")
    }
}
```

### Funcionalidad del Preview:

- **@Preview**: Permite ver cómo se ve el componente en Android Studio sin ejecutar la app
- **showBackground = true**: Muestra un fondo en la vista previa
- Útil para desarrollar y probar la UI rápidamente

## Resultado final

La aplicación muestra **"Hello Android!"** en pantalla con el tema y estructura básica de Material Design.

## Conceptos clave

- **Jetpack Compose**: Framework moderno de Android para crear interfaces de usuario
- **ComponentActivity**: Clase base para actividades que usan Compose
- **@Composable**: Anotación que marca funciones que pueden crear UI
- **Scaffold**: Estructura de layout que implementa Material Design
- **Modifier**: Sistema para aplicar estilos y comportamientos a los componentes