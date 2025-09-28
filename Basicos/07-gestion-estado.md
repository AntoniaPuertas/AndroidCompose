# Gestión de Estado en Jetpack Compose - Nivel Básico

## 🎯 ¿Qué es el Estado?

El **estado** es información que puede cambiar en tu aplicación:
- Un contador que sube y baja
- El texto que escribes en un campo
- Si un botón está presionado o no

Cuando el estado cambia, la interfaz se **actualiza automáticamente**.

## 🔄 ¿Por qué necesitamos gestionar el estado?

```kotlin
// ❌ Esto NO funciona
@Composable
fun ContadorQueNoFunciona() {
    var numero = 0  // Se resetea a 0 en cada cambio
    
    Button(onClick = { numero++ }) {  // No se actualiza la UI
        Text("Número: $numero")
    }
}
```

**Problema**: Cada vez que algo cambia, el código se ejecuta de nuevo y `numero` vuelve a ser 0.

## ✅ La solución: `remember` y `mutableStateOf`

```kotlin
@Composable
fun ContadorQueSiFunciona() {
    var numero by remember { mutableStateOf(0) }  // ¡Ahora sí funciona!
    
    Button(onClick = { numero++ }) {  // La UI se actualiza
        Text("Número: $numero")
    }
}
```

### 🧠 Explicación:
- **`mutableStateOf(0)`**: Crea un "estado" que puede cambiar, empezando en 0
- **`remember`**: Le dice a Compose "¡recuerda este valor!" entre actualizaciones
- **`by`**: Nos permite usar `numero` directamente sin escribir `.value`

## 📝 Sintaxis básica

### Crear estado
```kotlin
var contador by remember { mutableStateOf(0) }
var texto by remember { mutableStateOf("") }
var activo by remember { mutableStateOf(false) }
```

### Usar el estado
```kotlin
// Leer el valor
Text("Contador: $contador")

// Cambiar el valor
Button(onClick = { contador++ }) { 
    Text("Incrementar") 
}

// Con condicionales
if (activo) {
    Text("Está activo")
}
```

## 🔄 Formas de escribir el estado

### Forma 1: Con `by` (recomendada)
```kotlin
var contador by remember { mutableStateOf(0) }
contador = 5  // Usar directamente
```

### Forma 2: Con `.value`
```kotlin
val contador = remember { mutableStateOf(0) }
contador.value = 5  // Necesitas .value
```

### Forma 3: Con destructuring
```kotlin
val (contador, setContador) = remember { mutableStateOf(0) }
setContador(5)  // Usar función
```

**Recomendación**: Usa la **Forma 1** con `by` porque es más simple.

## 📋 Tipos de estado comunes

### Estado simple
```kotlin
var numero by remember { mutableStateOf(0) }
var texto by remember { mutableStateOf("") }
var visible by remember { mutableStateOf(true) }
```

### Estado con listas
```kotlin
var elementos by remember { mutableStateOf(listOf("Item 1", "Item 2")) }

// Para agregar elementos
elementos = elementos + "Nuevo item"

// Para eliminar elementos
elementos = elementos.filter { it != "Item 1" }
```

### Estado con objetos
```kotlin
data class Usuario(val nombre: String, val edad: Int)

var usuario by remember { mutableStateOf(Usuario("Ana", 25)) }

// Para cambiar propiedades
usuario = usuario.copy(edad = 26)
```

## ⚠️ Errores comunes

### Error 1: Olvidar `remember`
```kotlin
// ❌ MAL - Se resetea siempre
var contador = mutableStateOf(0)

// ✅ BIEN - Se mantiene
var contador by remember { mutableStateOf(0) }
```

### Error 2: Modificar listas directamente
```kotlin
// ❌ MAL - No funciona
elementos.add("nuevo")

// ✅ BIEN - Crear nueva lista
elementos = elementos + "nuevo"
```

### Error 3: Estado que no cambia
```kotlin
// ❌ MAL - Si nunca va a cambiar
val textoFijo by remember { mutableStateOf("Hola") }

// ✅ BIEN - Variable simple
val textoFijo = "Hola"
```

## 📚 Reglas simples

1. **Si algo cambia** → Usa `mutableStateOf`
2. **Si quieres que se mantenga** → Envuélvelo con `remember`
3. **Para listas** → Crea una nueva lista en lugar de modificar
4. **Usa `by`** → Es más fácil de leer y escribir

## 🎯 Cuándo usar estado

### ✅ SÍ usar estado para:
- Valores que cambian con la interacción del usuario
- Contadores, texto de campos, switches
- Listas que se modifican
- Estados de loading o errores

### ❌ NO usar estado para:
- Valores que nunca cambian
- Constantes de la aplicación
- Colores, tamaños fijos
- Configuraciones que no dependen del usuario

## 🎉 Resumen

- **Estado = información que cambia**
- **`remember { mutableStateOf() }`** para crear estado
- **`by`** para usar el estado fácilmente
- **Cuando el estado cambia, la UI se actualiza automáticamente**
- **Para listas: crear nueva lista en lugar de modificar**

¡Con estos conceptos básicos ya puedes crear aplicaciones interactivas! 🚀