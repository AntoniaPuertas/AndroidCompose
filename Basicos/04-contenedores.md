# Contenedores de Layout en Jetpack Compose

Este documento explica los principales contenedores de layout disponibles en Jetpack Compose para organizar elementos en la interfaz de usuario.

## 1. Column - Layout Vertical

### Descripción
`Column` organiza sus elementos hijos **verticalmente**, uno debajo del otro.

### Sintaxis básica
```kotlin
@Composable
fun VerticalLayout() {
    Column {
        Text("Primer elemento")
        Text("Segundo elemento")
        Button(onClick = {}) {
            Text("Botón")
        }
    }
}
```

### Parámetros importantes
```kotlin
Column(
    modifier = Modifier.fillMaxSize(),
    verticalArrangement = Arrangement.Center,  // Cómo distribuir verticalmente
    horizontalAlignment = Alignment.CenterHorizontally  // Alineación horizontal
) {
    // Elementos hijos
}
```

### Opciones de `verticalArrangement`
- `Arrangement.Top`: Elementos al principio
- `Arrangement.Center`: Elementos centrados
- `Arrangement.Bottom`: Elementos al final
- `Arrangement.SpaceBetween`: Espacio entre elementos
- `Arrangement.SpaceEvenly`: Espacio uniforme
- `Arrangement.SpaceAround`: Espacio alrededor de cada elemento

### Opciones de `horizontalAlignment`
- `Alignment.Start`: Alineación a la izquierda
- `Alignment.CenterHorizontally`: Centrado horizontal
- `Alignment.End`: Alineación a la derecha

### Casos de uso
- Formularios con campos uno debajo del otro
- Listas de elementos simples
- Menús verticales
- Layouts principales de pantalla

---

## 2. Row - Layout Horizontal

### Descripción
`Row` organiza sus elementos hijos **horizontalmente**, uno al lado del otro.

### Sintaxis básica
```kotlin
@Composable
fun HorizontalLayout() {
    Row {
        Text("Izquierda")
        Spacer(modifier = Modifier.width(16.dp))
        Text("Centro")
        Spacer(modifier = Modifier.width(16.dp))
        Text("Derecha")
    }
}
```

### Parámetros importantes
```kotlin
Row(
    modifier = Modifier.fillMaxWidth(),
    horizontalArrangement = Arrangement.SpaceBetween,  // Distribución horizontal
    verticalAlignment = Alignment.CenterVertically  // Alineación vertical
) {
    // Elementos hijos
}
```

### Opciones de `horizontalArrangement`
- `Arrangement.Start`: Elementos al inicio
- `Arrangement.Center`: Elementos centrados
- `Arrangement.End`: Elementos al final
- `Arrangement.SpaceBetween`: Espacio entre elementos
- `Arrangement.SpaceEvenly`: Espacio uniforme

### Opciones de `verticalAlignment`
- `Alignment.Top`: Alineación superior
- `Alignment.CenterVertically`: Centrado vertical
- `Alignment.Bottom`: Alineación inferior

### Casos de uso
- Barras de herramientas
- Botones de acción en línea
- Información con iconos al lado
- Headers con múltiples elementos

---

## 3. Box - Superposición de Elementos

### Descripción
`Box` permite **superponer** elementos unos encima de otros, como capas.

### Sintaxis básica
```kotlin
@Composable
fun OverlayLayout() {
    Box {
        Image(
            painter = painterResource(R.drawable.background),
            contentDescription = null
        )
        Text(
            text = "Texto superpuesto",
            color = Color.White,
            modifier = Modifier.align(Alignment.Center)
        )
    }
}
```

### Alineaciones disponibles
```kotlin
Box {
    Text("Fondo", modifier = Modifier.align(Alignment.Center))
    Text("Esquina superior izquierda", modifier = Modifier.align(Alignment.TopStart))
    Text("Esquina superior derecha", modifier = Modifier.align(Alignment.TopEnd))
    Text("Esquina inferior izquierda", modifier = Modifier.align(Alignment.BottomStart))
    Text("Esquina inferior derecha", modifier = Modifier.align(Alignment.BottomEnd))
}
```

### Casos de uso
- Texto sobre imágenes
- Badges sobre iconos
- Loading overlays
- Floating Action Buttons
- Elementos de decoración superpuestos

---

## 4. LazyColumn - Lista Vertical con Scroll

### Descripción
`LazyColumn` crea **listas verticales eficientes** que solo renderizan los elementos visibles en pantalla.

### Sintaxis básica
```kotlin
@Composable
fun VerticalList() {
    val items = (1..1000).map { "Item #$it" }
    
    LazyColumn {
        items(items) { item ->
            Text(
                text = item,
                modifier = Modifier.padding(16.dp)
            )
        }
    }
}
```

### Diferentes tipos de items
```kotlin
LazyColumn {
    // Item único
    item {
        Text("Header")
    }
    
    // Lista de items
    items(itemList) { item ->
        ItemCard(item)
    }
    
    // Items con índice
    itemsIndexed(itemList) { index, item ->
        Text("$index: $item")
    }
    
    // Item único al final
    item {
        Text("Footer")
    }
}
```

### Parámetros importantes
```kotlin
LazyColumn(
    modifier = Modifier.fillMaxSize(),
    contentPadding = PaddingValues(16.dp),  // Padding interno
    verticalArrangement = Arrangement.spacedBy(8.dp),  // Espacio entre items
    state = rememberLazyListState()  // Control del estado de scroll
) {
    // Items
}
```

### Casos de uso
- Listas de contactos
- Feeds de noticias
- Catálogos de productos
- Historial de conversaciones
- Cualquier lista larga de datos

---

## 5. LazyRow - Lista Horizontal con Scroll

### Descripción
`LazyRow` crea **listas horizontales eficientes** con scroll horizontal.

### Sintaxis básica
```kotlin
@Composable
fun HorizontalList() {
    val categories = listOf("Tecnología", "Deportes", "Música", "Arte", "Ciencia")
    
    LazyRow {
        items(categories) { category ->
            CategoryChip(
                text = category,
                modifier = Modifier.padding(horizontal = 4.dp)
            )
        }
    }
}

@Composable
fun CategoryChip(text: String, modifier: Modifier = Modifier) {
    Surface(
        modifier = modifier,
        shape = RoundedCornerShape(16.dp),
        color = MaterialTheme.colors.primary
    ) {
        Text(
            text = text,
            modifier = Modifier.padding(horizontal = 16.dp, vertical = 8.dp),
            color = Color.White
        )
    }
}
```

### Casos de uso
- Chips de categorías
- Carrusel de imágenes
- Lista de filtros
- Navegación de tabs
- Galería horizontal

---

## Ejemplo Combinado

```kotlin
@Composable
fun CompleteLayout() {
    Column {
        // Header con elementos horizontales
        Row(
            modifier = Modifier
                .fillMaxWidth()
                .padding(16.dp),
            horizontalArrangement = Arrangement.SpaceBetween
        ) {
            Text("Mi App")
            Button(onClick = {}) {
                Text("Configuración")
            }
        }
        
        // Lista de categorías horizontal
        LazyRow(
            contentPadding = PaddingValues(horizontal = 16.dp),
            horizontalArrangement = Arrangement.spacedBy(8.dp)
        ) {
            items(listOf("Todos", "Favoritos", "Recientes")) { category ->
                CategoryChip(category)
            }
        }
        
        // Lista principal vertical
        LazyColumn(
            modifier = Modifier.weight(1f),
            contentPadding = PaddingValues(16.dp),
            verticalArrangement = Arrangement.spacedBy(8.dp)
        ) {
            items(20) { index ->
                ItemCard("Item #${index + 1}")
            }
        }
    }
}
```

## Consejos de Performance

### Para LazyColumn/LazyRow:
- Usa `key` parameter para items únicos
- Evita operaciones pesadas en el contenido de los items
- Usa `rememberLazyListState()` para controlar el scroll
- Implementa `contentType` para diferentes tipos de items

```kotlin
LazyColumn {
    items(
        items = itemList,
        key = { item -> item.id },  // Key único para cada item
        contentType = { item -> item.type }  // Tipo de contenido
    ) { item ->
        ItemComposable(item)
    }
}
```

## Resumen de Cuándo Usar Cada Uno

| Layout | Cuándo usar |
|--------|-------------|
| **Column** | Elementos apilados verticalmente, formularios |
| **Row** | Elementos en línea horizontal, toolbars |
| **Box** | Superposición de elementos, overlays |
| **LazyColumn** | Listas verticales largas, feeds |
| **LazyRow** | Listas horizontales, carruseles, chips |

Cada contenedor tiene su propósito específico y elegir el correcto mejora tanto la experiencia de usuario como el rendimiento de la aplicación.