# LazyRow en Jetpack Compose - Explicación Detallada

Este documento explica en profundidad `LazyRow`, el componente de Jetpack Compose para crear listas horizontales eficientes con scroll.

## ¿Qué es LazyRow?

`LazyRow` es un componente que crea **listas horizontales eficientes** donde los elementos se disponen uno al lado del otro horizontalmente. Al igual que `LazyColumn`, utiliza **virtualización** para renderizar solo los elementos visibles en pantalla.

### Características principales:
- **Scroll horizontal**: Los elementos se desplazan de izquierda a derecha
- **Lazy loading**: Solo renderiza elementos visibles
- **Memoria eficiente**: Mantiene pocos elementos en memoria
- **Performance**: Puede manejar miles de elementos sin problemas

## Sintaxis básica

```kotlin
@Composable
fun BasicHorizontalList() {
    val items = (1..100).map { "Item #$it" }
    
    LazyRow {
        items(items) { item ->
            Text(
                text = item,
                modifier = Modifier.padding(16.dp)
            )
        }
    }
}
```

## Visualización del comportamiento

```
┌─────────────────────────────────────────────────────────────┐
│ LazyRow - Vista horizontal con scroll                       │
├─────────────────────────────────────────────────────────────┤
│ ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐ ───────────→      │
│ │Item │ │Item │ │Item │ │Item │ │Item │                    │
│ │  #1 │ │  #2 │ │  #3 │ │  #4 │ │  #5 │                    │
│ └─────┘ └─────┘ └─────┘ └─────┘ └─────┘                    │
│                                                             │
│ Items #6-100 (no renderizados, fuera de vista)             │
└─────────────────────────────────────────────────────────────┘
```

## Parámetros principales de LazyRow

```kotlin
LazyRow(
    modifier = Modifier.fillMaxWidth(),
    contentPadding = PaddingValues(horizontal = 16.dp),
    horizontalArrangement = Arrangement.spacedBy(8.dp),
    verticalAlignment = Alignment.CenterVertically,
    state = rememberLazyListState(),
    reverseLayout = false,
    userScrollEnabled = true
) {
    // Contenido de la lista
}
```

### Explicación de parámetros:

#### `contentPadding`
Padding interno de toda la lista:
```kotlin
LazyRow(
    contentPadding = PaddingValues(
        start = 16.dp,    // Espacio al inicio
        end = 16.dp,      // Espacio al final
        top = 8.dp,       // Espacio arriba
        bottom = 8.dp     // Espacio abajo
    )
) { /* items */ }
```

#### `horizontalArrangement`
Cómo distribuir los elementos horizontalmente:
```kotlin
// Ejemplos de distribución horizontal
LazyRow(horizontalArrangement = Arrangement.Start) { /* items */ }        // Al inicio
LazyRow(horizontalArrangement = Arrangement.Center) { /* items */ }       // Centrados
LazyRow(horizontalArrangement = Arrangement.End) { /* items */ }          // Al final
LazyRow(horizontalArrangement = Arrangement.SpaceBetween) { /* items */ } // Espacio entre
LazyRow(horizontalArrangement = Arrangement.SpaceEvenly) { /* items */ }  // Espacio uniforme
LazyRow(horizontalArrangement = Arrangement.spacedBy(12.dp)) { /* items */ } // Espacio fijo
```

#### `verticalAlignment`
Alineación vertical de los elementos:
```kotlin
LazyRow(verticalAlignment = Alignment.Top) { /* items */ }             // Arriba
LazyRow(verticalAlignment = Alignment.CenterVertically) { /* items */ } // Centro
LazyRow(verticalAlignment = Alignment.Bottom) { /* items */ }           // Abajo
```

## Casos de uso comunes

### 1. Chips de categorías

```kotlin
@Composable
fun CategoryChips() {
    val categories = listOf("Todos", "Deportes", "Música", "Arte", "Ciencia", "Tecnología")
    var selectedCategory by remember { mutableStateOf("Todos") }
    
    LazyRow(
        contentPadding = PaddingValues(horizontal = 16.dp),
        horizontalArrangement = Arrangement.spacedBy(8.dp)
    ) {
        items(categories) { category ->
            FilterChip(
                selected = category == selectedCategory,
                onClick = { selectedCategory = category },
                label = { Text(category) }
            )
        }
    }
}
```

### 2. Carrusel de imágenes

```kotlin
@Composable
fun ImageCarousel() {
    val images = listOf(
        R.drawable.image1,
        R.drawable.image2,
        R.drawable.image3,
        R.drawable.image4
    )
    
    LazyRow(
        contentPadding = PaddingValues(16.dp),
        horizontalArrangement = Arrangement.spacedBy(12.dp)
    ) {
        items(images) { imageRes ->
            Card(
                modifier = Modifier.size(200.dp),
                shape = RoundedCornerShape(12.dp)
            ) {
                Image(
                    painter = painterResource(imageRes),
                    contentDescription = null,
                    contentScale = ContentScale.Crop,
                    modifier = Modifier.fillMaxSize()
                )
            }
        }
    }
}
```

### 3. Lista de contactos horizontal

```kotlin
data class Contact(val name: String, val avatar: Int)

@Composable
fun HorizontalContactList() {
    val contacts = listOf(
        Contact("Ana", R.drawable.avatar1),
        Contact("Carlos", R.drawable.avatar2),
        Contact("María", R.drawable.avatar3),
        Contact("José", R.drawable.avatar4)
    )
    
    LazyRow(
        contentPadding = PaddingValues(16.dp),
        horizontalArrangement = Arrangement.spacedBy(16.dp)
    ) {
        items(contacts) { contact ->
            Column(
                horizontalAlignment = Alignment.CenterHorizontally,
                modifier = Modifier.width(80.dp)
            ) {
                Image(
                    painter = painterResource(contact.avatar),
                    contentDescription = contact.name,
                    modifier = Modifier
                        .size(56.dp)
                        .clip(CircleShape)
                )
                Spacer(modifier = Modifier.height(8.dp))
                Text(
                    text = contact.name,
                    textAlign = TextAlign.Center,
                    maxLines = 1,
                    overflow = TextOverflow.Ellipsis
                )
            }
        }
    }
}
```

### 4. Navegación de tabs horizontal

```kotlin
@Composable
fun HorizontalTabs() {
    val tabs = listOf("Recientes", "Favoritos", "Archivados", "Papelera", "Configuración")
    var selectedTab by remember { mutableStateOf(0) }
    
    LazyRow(
        modifier = Modifier.fillMaxWidth(),
        contentPadding = PaddingValues(horizontal = 8.dp)
    ) {
        itemsIndexed(tabs) { index, tab ->
            Tab(
                selected = selectedTab == index,
                onClick = { selectedTab = index },
                text = { Text(tab) },
                modifier = Modifier.padding(horizontal = 4.dp)
            )
        }
    }
}
```

## Comparación: LazyRow vs Row normal

### Con Row normal (INEFICIENTE para muchos elementos):

```kotlin
@Composable
fun InefficiencyHorizontalList() {
    val items = (1..1000).map { "Item #$it" }
    
    ScrollableRow {  // ❌ Renderiza TODOS los elementos
        items.forEach { item ->
            Text(
                text = item,
                modifier = Modifier.padding(16.dp)
            )
        }
    }
}
```

**Problemas:**
- Renderiza todos los elementos inmediatamente
- Consume mucha memoria
- Puede causar ANR (Application Not Responding)

### Con LazyRow (EFICIENTE):

```kotlin
@Composable
fun EfficientHorizontalList() {
    val items = (1..1000).map { "Item #$it" }
    
    LazyRow {  // ✅ Solo renderiza elementos visibles
        items(items) { item ->
            Text(
                text = item,
                modifier = Modifier.padding(16.dp)
            )
        }
    }
}
```

## Control avanzado del estado

### Estado de scroll personalizado

```kotlin
@Composable
fun ControlledScrollRow() {
    val items = (1..50).map { "Item #$it" }
    val listState = rememberLazyListState()
    val coroutineScope = rememberCoroutineScope()
    
    Column {
        // Botones de control
        Row(
            modifier = Modifier
                .fillMaxWidth()
                .padding(16.dp),
            horizontalArrangement = Arrangement.SpaceEvenly
        ) {
            Button(
                onClick = {
                    coroutineScope.launch {
                        listState.animateScrollToItem(0)
                    }
                }
            ) {
                Text("Inicio")
            }
            
            Button(
                onClick = {
                    coroutineScope.launch {
                        listState.animateScrollToItem(items.size - 1)
                    }
                }
            ) {
                Text("Final")
            }
        }
        
        // Lista horizontal
        LazyRow(
            state = listState,
            contentPadding = PaddingValues(horizontal = 16.dp),
            horizontalArrangement = Arrangement.spacedBy(8.dp)
        ) {
            items(items) { item ->
                Card(
                    modifier = Modifier.size(100.dp)
                ) {
                    Box(
                        modifier = Modifier.fillMaxSize(),
                        contentAlignment = Alignment.Center
                    ) {
                        Text(item)
                    }
                }
            }
        }
    }
}
```

### Detección de scroll

```kotlin
@Composable
fun ScrollDetectionRow() {
    val items = (1..30).map { "Item #$it" }
    val listState = rememberLazyListState()
    
    // Detectar cuando el usuario está haciendo scroll
    val isScrolling by remember {
        derivedStateOf {
            listState.isScrollInProgress
        }
    }
    
    // Obtener el primer elemento visible
    val firstVisibleIndex by remember {
        derivedStateOf {
            listState.firstVisibleItemIndex
        }
    }
    
    Column {
        // Información de estado
        Card(
            modifier = Modifier
                .fillMaxWidth()
                .padding(16.dp)
        ) {
            Column(modifier = Modifier.padding(16.dp)) {
                Text("¿Scrolleando?: ${if (isScrolling) "Sí" else "No"}")
                Text("Primer elemento visible: $firstVisibleIndex")
            }
        }
        
        // Lista horizontal
        LazyRow(
            state = listState,
            contentPadding = PaddingValues(horizontal = 16.dp),
            horizontalArrangement = Arrangement.spacedBy(8.dp)
        ) {
            items(items) { item ->
                Card(
                    modifier = Modifier.size(80.dp),
                    colors = CardDefaults.cardColors(
                        containerColor = if (isScrolling) 
                            MaterialTheme.colorScheme.secondary 
                        else 
                            MaterialTheme.colorScheme.surface
                    )
                ) {
                    Box(
                        modifier = Modifier.fillMaxSize(),
                        contentAlignment = Alignment.Center
                    ) {
                        Text(item)
                    }
                }
            }
        }
    }
}
```

## Diferentes tipos de elementos

### Lista mixta con diferentes contenidos

```kotlin
sealed class HorizontalItem {
    data class TextItem(val text: String) : HorizontalItem()
    data class ImageItem(val imageRes: Int, val title: String) : HorizontalItem()
    data class ButtonItem(val text: String, val action: () -> Unit) : HorizontalItem()
}

@Composable
fun MixedHorizontalContent() {
    val items = listOf(
        HorizontalItem.TextItem("Primer texto"),
        HorizontalItem.ImageItem(R.drawable.sample1, "Imagen 1"),
        HorizontalItem.TextItem("Segundo texto"),
        HorizontalItem.ButtonItem("Acción") { /* hacer algo */ },
        HorizontalItem.ImageItem(R.drawable.sample2, "Imagen 2")
    )
    
    LazyRow(
        contentPadding = PaddingValues(16.dp),
        horizontalArrangement = Arrangement.spacedBy(12.dp),
        verticalAlignment = Alignment.CenterVertically
    ) {
        items(
            items = items,
            contentType = { item ->
                when (item) {
                    is HorizontalItem.TextItem -> "text"
                    is HorizontalItem.ImageItem -> "image"
                    is HorizontalItem.ButtonItem -> "button"
                }
            }
        ) { item ->
            when (item) {
                is HorizontalItem.TextItem -> {
                    Card(
                        modifier = Modifier.widthIn(min = 100.dp)
                    ) {
                        Text(
                            text = item.text,
                            modifier = Modifier.padding(16.dp)
                        )
                    }
                }
                is HorizontalItem.ImageItem -> {
                    Column(
                        horizontalAlignment = Alignment.CenterHorizontally,
                        modifier = Modifier.width(120.dp)
                    ) {
                        Image(
                            painter = painterResource(item.imageRes),
                            contentDescription = item.title,
                            modifier = Modifier
                                .size(80.dp)
                                .clip(RoundedCornerShape(8.dp)),
                            contentScale = ContentScale.Crop
                        )
                        Spacer(modifier = Modifier.height(4.dp))
                        Text(item.title, textAlign = TextAlign.Center)
                    }
                }
                is HorizontalItem.ButtonItem -> {
                    Button(
                        onClick = item.action,
                        modifier = Modifier.height(40.dp)
                    ) {
                        Text(item.text)
                    }
                }
            }
        }
    }
}
```

## Optimizaciones de performance

### 1. Usar keys únicas

```kotlin
data class Product(val id: String, val name: String, val price: Double)

@Composable
fun ProductCarousel(products: List<Product>) {
    LazyRow {
        items(
            items = products,
            key = { product -> product.id }  // ✅ Key única
        ) { product ->
            ProductCard(product)
        }
    }
}
```

### 2. contentType para diferentes tipos

```kotlin
LazyRow {
    items(
        items = mixedItems,
        contentType = { item ->
            when (item) {
                is HorizontalItem.TextItem -> "text"
                is HorizontalItem.ImageItem -> "image"
                is HorizontalItem.ButtonItem -> "button"
            }
        }
    ) { item ->
        // Renderizado según el tipo
    }
}
```

### 3. Limitar el tamaño de elementos

```kotlin
LazyRow {
    items(items) { item ->
        Card(
            modifier = Modifier
                .widthIn(min = 120.dp, max = 200.dp)  // ✅ Tamaños consistentes
                .height(100.dp)
        ) {
            // Contenido
        }
    }
}
```

## Ejemplo completo: Pantalla de inicio con múltiples secciones

```kotlin
@Composable
fun HomeScreen() {
    LazyColumn {
        item {
            Text(
                text = "Categorías",
                style = MaterialTheme.typography.headlineMedium,
                modifier = Modifier.padding(16.dp)
            )
        }
        
        item {
            CategoryChips()
        }
        
        item {
            Text(
                text = "Destacados",
                style = MaterialTheme.typography.headlineMedium,
                modifier = Modifier.padding(16.dp)
            )
        }
        
        item {
            FeaturedCarousel()
        }
        
        item {
            Text(
                text = "Contactos frecuentes",
                style = MaterialTheme.typography.headlineMedium,
                modifier = Modifier.padding(16.dp)
            )
        }
        
        item {
            HorizontalContactList()
        }
    }
}

@Composable
fun FeaturedCarousel() {
    val featuredItems = listOf("Destacado 1", "Destacado 2", "Destacado 3")
    
    LazyRow(
        contentPadding = PaddingValues(horizontal = 16.dp),
        horizontalArrangement = Arrangement.spacedBy(12.dp)
    ) {
        items(featuredItems) { item ->
            Card(
                modifier = Modifier.size(width = 160.dp, height = 120.dp)
            ) {
                Box(
                    modifier = Modifier.fillMaxSize(),
                    contentAlignment = Alignment.Center
                ) {
                    Text(item)
                }
            }
        }
    }
}
```

## Cuándo usar LazyRow

**✅ Usar LazyRow cuando:**
- Tienes listas horizontales con muchos elementos
- Los elementos no caben todos en pantalla
- Quieres scroll horizontal fluido
- Necesitas performance optimizada

**❌ No usar LazyRow cuando:**
- Solo tienes pocos elementos (2-5)
- Todos los elementos caben en pantalla
- No necesitas scroll (usar `Row` normal)

## Resumen de mejores prácticas

1. **Usa `contentPadding`** para espaciado externo
2. **Usa `horizontalArrangement = Arrangement.spacedBy()`** para espaciado entre elementos
3. **Define keys únicas** para elementos que pueden cambiar
4. **Especifica `contentType`** para listas mixtas
5. **Controla el estado** cuando necesites navegación programática
6. **Limita los tamaños** para mantener consistencia visual
7. **Usa `verticalAlignment`** para alinear elementos de diferentes alturas

LazyRow es perfecto para crear interfaces horizontales fluidas y eficientes en Jetpack Compose.