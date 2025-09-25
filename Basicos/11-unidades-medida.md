# Unidades de Medida en Jetpack Compose - Guía Completa

Este documento explica en detalle todas las unidades de medida disponibles en Jetpack Compose, cuándo usarlas y cómo aplicarlas correctamente para crear interfaces responsivas y bien dimensionadas.

## ¿Por qué son importantes las unidades de medida?

En Compose, elegir la unidad de medida correcta es crucial para:
- **Consistency visual** en diferentes dispositivos
- **Accesibilidad** apropiada
- **Responsive design** que se adapta a diversas pantallas
- **Performance** óptimo del layout
- **Experiencia de usuario** coherente

## Tipos de unidades de medida

### 1. Dp (Density-independent pixels)

**Definición:** Píxeles independientes de densidad. Una unidad abstracta basada en la densidad física de la pantalla.

#### ¿Cómo funciona?
- **1 dp = 1 pixel** en una pantalla de 160 DPI (densidad media)
- En pantallas de mayor densidad, 1 dp equivale a más píxeles físicos
- **Escala automáticamente** según la densidad del dispositivo

#### Sintaxis y ejemplos
```kotlin
@Composable
fun DpExamples() {
    Column(
        modifier = Modifier.padding(16.dp),
        verticalArrangement = Arrangement.spacedBy(8.dp)
    ) {
        Text("Unidades Dp - Density Independent Pixels")
        
        // Tamaños fijos en dp
        Box(
            modifier = Modifier
                .size(48.dp) // 48x48 dp
                .background(Color.Blue)
        )
        
        // Dimensiones específicas
        Box(
            modifier = Modifier
                .width(120.dp)
                .height(60.dp)
                .background(Color.Green)
        )
        
        // Padding y margins
        Text(
            text = "Texto con padding",
            modifier = Modifier
                .background(Color.Yellow)
                .padding(horizontal = 16.dp, vertical = 8.dp)
        )
        
        // Bordes
        Box(
            modifier = Modifier
                .size(80.dp)
                .border(2.dp, Color.Red, RoundedCornerShape(8.dp))
        )
    }
}
```

#### Casos de uso típicos
```kotlin
@Composable
fun CommonDpUseCases() {
    Column {
        // Tamaños de elementos UI estándar
        IconButton(
            onClick = {},
            modifier = Modifier.size(48.dp) // Tamaño táctil mínimo recomendado
        ) {
            Icon(Icons.Default.Favorite, contentDescription = null)
        }
        
        // Espaciado consistente
        Spacer(modifier = Modifier.height(16.dp)) // Espaciado estándar
        
        // Elevación de cards
        Card(
            elevation = CardDefaults.cardElevation(defaultElevation = 4.dp),
            modifier = Modifier.padding(8.dp)
        ) {
            Text("Card con elevación", modifier = Modifier.padding(16.dp))
        }
        
        // Esquinas redondeadas
        Button(
            onClick = {},
            shape = RoundedCornerShape(24.dp)
        ) {
            Text("Botón redondeado")
        }
    }
}
```

#### Valores recomendados Material Design
```kotlin
// Espaciado estándar en dp
object MaterialSpacing {
    val xs = 4.dp      // Espaciado extra pequeño
    val small = 8.dp   // Espaciado pequeño
    val medium = 16.dp // Espaciado estándar
    val large = 24.dp  // Espaciado grande
    val xl = 32.dp     // Espaciado extra grande
    val xxl = 48.dp    // Espaciado muy grande
}

// Tamaños de iconos estándar
object IconSizes {
    val small = 16.dp
    val medium = 24.dp
    val large = 32.dp
    val extraLarge = 48.dp
}

// Tamaños táctiles mínimos
object TouchTargets {
    val minimum = 48.dp    // Tamaño mínimo recomendado
    val comfortable = 56.dp // Tamaño cómodo
}

@Composable
fun MaterialDesignStandards() {
    Column(
        modifier = Modifier.padding(MaterialSpacing.medium),
        verticalArrangement = Arrangement.spacedBy(MaterialSpacing.small)
    ) {
        // Usando los estándares definidos
        IconButton(
            onClick = {},
            modifier = Modifier.size(TouchTargets.minimum)
        ) {
            Icon(
                Icons.Default.Settings, 
                contentDescription = null,
                modifier = Modifier.size(IconSizes.medium)
            )
        }
        
        Card(
            modifier = Modifier.padding(MaterialSpacing.small)
        ) {
            Text(
                "Contenido de la card",
                modifier = Modifier.padding(MaterialSpacing.medium)
            )
        }
    }
}
```

---

### 2. Sp (Scale-independent pixels)

**Definición:** Píxeles independientes de escala. Similar a dp pero también considera las preferencias de tamaño de fuente del usuario.

#### ¿Cómo funciona?
- **Escala con la densidad** como dp
- **ADEMÁS escala con las preferencias de fuente** del usuario
- Si el usuario aumenta el tamaño de fuente del sistema, los sp se escalan proporcionalmente

#### Sintaxis y ejemplos
```kotlin
@Composable
fun SpExamples() {
    Column(
        modifier = Modifier.padding(16.dp),
        verticalArrangement = Arrangement.spacedBy(12.dp)
    ) {
        Text("Unidades Sp - Scale Independent Pixels")
        
        // Diferentes tamaños de texto
        Text(
            text = "Texto pequeño",
            fontSize = 12.sp
        )
        
        Text(
            text = "Texto normal",
            fontSize = 16.sp
        )
        
        Text(
            text = "Texto grande",
            fontSize = 20.sp
        )
        
        Text(
            text = "Título",
            fontSize = 24.sp,
            fontWeight = FontWeight.Bold
        )
        
        // Espaciado de líneas también en sp
        Text(
            text = "Texto con espaciado de línea personalizado.\nEsta es la segunda línea para mostrar el efecto.",
            fontSize = 16.sp,
            lineHeight = 24.sp
        )
    }
}
```

#### Comparación Dp vs Sp
```kotlin
@Composable
fun DpVsSpComparison() {
    Column(
        modifier = Modifier.padding(16.dp),
        verticalArrangement = Arrangement.spacedBy(16.dp)
    ) {
        Text(
            "Comparación Dp vs Sp",
            style = MaterialTheme.typography.headlineMedium
        )
        
        // Elemento con dp - NO escala con preferencias del usuario
        Box(
            modifier = Modifier
                .size(100.dp) // Siempre será 100dp
                .background(Color.Blue),
            contentAlignment = Alignment.Center
        ) {
            Text(
                text = "100dp",
                color = Color.White,
                fontSize = 16.sp // El texto SÍ escalará
            )
        }
        
        // Texto en sp - SÍ escala con preferencias del usuario
        Text(
            text = "Este texto cambia de tamaño según las preferencias del usuario",
            fontSize = 18.sp // Escalará con configuración del sistema
        )
        
        // Mal uso: letra spacing en dp
        Text(
            text = "Espaciado incorrecto",
            fontSize = 16.sp,
            letterSpacing = 2.dp // ❌ MAL: no escalará con el texto
        )
        
        // Buen uso: letter spacing en sp o em
        Text(
            text = "Espaciado correcto",
            fontSize = 16.sp,
            letterSpacing = 0.1.sp // ✅ BIEN: escalará proporcionalmente
        )
    }
}
```

#### Tamaños de fuente recomendados
```kotlin
object TextSizes {
    val caption = 12.sp      // Texto muy pequeño, captions
    val body2 = 14.sp        // Texto secundario
    val body1 = 16.sp        // Texto principal
    val subtitle2 = 14.sp    // Subtítulos pequeños
    val subtitle1 = 16.sp    // Subtítulos normales
    val headline6 = 20.sp    // Títulos pequeños
    val headline5 = 24.sp    // Títulos medianos
    val headline4 = 34.sp    // Títulos grandes
    val headline3 = 48.sp    // Títulos muy grandes
    val headline2 = 60.sp    // Títulos de pantalla
    val headline1 = 96.sp    // Display text
}

@Composable
fun TypographyScale() {
    LazyColumn(
        contentPadding = PaddingValues(16.dp),
        verticalArrangement = Arrangement.spacedBy(8.dp)
    ) {
        item {
            Text("H1 - Display", fontSize = TextSizes.headline1)
        }
        item {
            Text("H2 - Headline", fontSize = TextSizes.headline2)
        }
        item {
            Text("H3 - Title", fontSize = TextSizes.headline3)
        }
        item {
            Text("H4 - Subtitle", fontSize = TextSizes.headline4)
        }
        item {
            Text("Body 1 - Texto principal", fontSize = TextSizes.body1)
        }
        item {
            Text("Body 2 - Texto secundario", fontSize = TextSizes.body2)
        }
        item {
            Text("Caption - Texto pequeño", fontSize = TextSizes.caption)
        }
    }
}
```

---

### 3. TextUnit - Unidad flexible para texto

**Definición:** Unidad especializada que puede representar Sp, Em o valores no especificados.

#### Tipos de TextUnit
```kotlin
@Composable
fun TextUnitExamples() {
    Column(
        modifier = Modifier.padding(16.dp),
        verticalArrangement = Arrangement.spacedBy(12.dp)
    ) {
        Text("TextUnit Examples")
        
        // TextUnit.Sp - equivalente a usar .sp directamente
        Text(
            text = "Usando TextUnit.Sp",
            fontSize = TextUnit(16f, TextUnitType.Sp)
        )
        
        // TextUnit.Em - relativo al tamaño de fuente padre
        Text(
            text = "Texto base con em",
            fontSize = 20.sp,
            modifier = Modifier.background(Color.LightGray.copy(alpha = 0.3f))
        ) {
            // Este texto interno será relativo al padre
            Text(
                text = "1.5em del padre",
                fontSize = TextUnit(1.5f, TextUnitType.Em)
            )
        }
        
        // TextUnit.Unspecified - usa el valor por defecto
        Text(
            text = "Sin especificar (usa tema)",
            fontSize = TextUnit.Unspecified
        )
    }
}
```

#### Uso práctico de Em
```kotlin
@Composable
fun EmUnitsExample() {
    Column(
        modifier = Modifier.padding(16.dp),
        verticalArrangement = Arrangement.spacedBy(16.dp)
    ) {
        // Base font size
        val baseFontSize = 18.sp
        
        Text(
            text = "Jerarquía con Em",
            fontSize = baseFontSize,
            fontWeight = FontWeight.Bold
        )
        
        Column(
            modifier = Modifier.padding(start = 16.dp),
            verticalArrangement = Arrangement.spacedBy(4.dp)
        ) {
            // Estos tamaños son relativos al tamaño base
            Text(
                text = "Subtítulo (0.9em)",
                fontSize = (baseFontSize.value * 0.9f).sp
            )
            
            Text(
                text = "Texto normal (1em)",
                fontSize = baseFontSize
            )
            
            Text(
                text = "Texto destacado (1.2em)",
                fontSize = (baseFontSize.value * 1.2f).sp,
                fontWeight = FontWeight.Medium
            )
        }
    }
}
```

---

### 4. Px (Píxeles absolutos)

**Definición:** Píxeles físicos reales de la pantalla. **Raramente recomendado** en Compose.

#### Cuándo NO usar px
```kotlin
@Composable
fun WhyNotPixels() {
    Column(modifier = Modifier.padding(16.dp)) {
        Text("Problemas con píxeles absolutos")
        
        // ❌ MAL: Estos elementos se verán diferentes en cada dispositivo
        Box(
            modifier = Modifier
                .size(100.px) // ❌ Se ve pequeño en pantallas de alta densidad
                .background(Color.Red)
        )
        
        Text(
            "Este texto puede ser ilegible",
            fontSize = TextUnit(12f, TextUnitType.Px) // ❌ Muy pequeño en hdpi
        )
    }
}
```

#### Casos raros donde px puede ser útil
```kotlin
@Composable
fun RarePixelUseCases() {
    // Líneas muy finas (1 pixel físico)
    Divider(
        thickness = 1.px, // Exactamente 1 pixel físico
        color = Color.Gray
    )
    
    // Para efectos específicos o debugging
    Canvas(modifier = Modifier.size(100.dp)) { drawScope ->
        drawLine(
            color = Color.Black,
            start = Offset(0f, 0f),
            end = Offset(100f, 100f),
            strokeWidth = 1.px.toPx() // Línea de exactamente 1px
        )
    }
}
```

---

### 5. Dimensiones intrínsecas y flexibles

#### Modifier.fillMax* - Llenar el espacio disponible
```kotlin
@Composable
fun FillExamples() {
    Column(
        modifier = Modifier
            .fillMaxSize() // Llena toda la pantalla disponible
            .background(Color.LightGray.copy(alpha = 0.3f))
            .padding(16.dp)
    ) {
        // Elemento que llena el ancho completo
        Box(
            modifier = Modifier
                .fillMaxWidth() // Ancho completo disponible
                .height(60.dp)
                .background(Color.Blue)
        ) {
            Text(
                "Ancho completo",
                color = Color.White,
                modifier = Modifier.align(Alignment.Center)
            )
        }
        
        Spacer(modifier = Modifier.height(16.dp))
        
        // Elemento que llena una fracción del ancho
        Box(
            modifier = Modifier
                .fillMaxWidth(0.7f) // 70% del ancho disponible
                .height(60.dp)
                .background(Color.Green)
        ) {
            Text(
                "70% del ancho",
                color = Color.White,
                modifier = Modifier.align(Alignment.Center)
            )
        }
        
        Spacer(modifier = Modifier.height(16.dp))
        
        // Elemento que llena el resto de la altura
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .fillMaxHeight() // Resto de la altura disponible
                .background(Color.Red)
        ) {
            Text(
                "Resto de altura",
                color = Color.White,
                modifier = Modifier.align(Alignment.Center)
            )
        }
    }
}
```

#### wrapContent - Ajustar al contenido
```kotlin
@Composable
fun WrapContentExamples() {
    Column(
        modifier = Modifier.padding(16.dp),
        verticalArrangement = Arrangement.spacedBy(16.dp)
    ) {
        Text("Ejemplos de wrapContent")
        
        // Se ajusta exactamente al texto
        Text(
            text = "Texto corto",
            modifier = Modifier
                .wrapContentSize() // Se ajusta al contenido
                .background(Color.Yellow)
                .padding(8.dp)
        )
        
        // Se ajusta solo en altura
        Text(
            text = "Este texto es más largo y se ajustará en altura pero llenará el ancho",
            modifier = Modifier
                .fillMaxWidth()
                .wrapContentHeight() // Solo altura ajustada
                .background(Color.Cyan)
                .padding(8.dp)
        )
        
        // Útil para centrar contenido
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .height(100.dp)
                .background(Color.LightGray)
        ) {
            Text(
                text = "Centrado",
                modifier = Modifier
                    .wrapContentSize() // Se ajusta al contenido
                    .align(Alignment.Center)
                    .background(Color.White)
                    .padding(16.dp)
            )
        }
    }
}
```

#### weight - Distribución proporcional
```kotlin
@Composable
fun WeightExamples() {
    Column(
        modifier = Modifier.padding(16.dp),
        verticalArrangement = Arrangement.spacedBy(16.dp)
    ) {
        Text("Distribución con weight")
        
        // Distribución horizontal
        Row(
            modifier = Modifier
                .fillMaxWidth()
                .height(60.dp)
        ) {
            Box(
                modifier = Modifier
                    .weight(1f) // Toma 1 parte del espacio
                    .fillMaxHeight()
                    .background(Color.Red),
                contentAlignment = Alignment.Center
            ) {
                Text("1", color = Color.White)
            }
            
            Box(
                modifier = Modifier
                    .weight(2f) // Toma 2 partes del espacio (doble)
                    .fillMaxHeight()
                    .background(Color.Green),
                contentAlignment = Alignment.Center
            ) {
                Text("2", color = Color.White)
            }
            
            Box(
                modifier = Modifier
                    .weight(1f) // Toma 1 parte del espacio
                    .fillMaxHeight()
                    .background(Color.Blue),
                contentAlignment = Alignment.Center
            ) {
                Text("1", color = Color.White)
            }
        }
        
        // Distribución vertical
        Column(
            modifier = Modifier
                .fillMaxWidth()
                .height(200.dp)
        ) {
            Box(
                modifier = Modifier
                    .weight(1f)
                    .fillMaxWidth()
                    .background(Color.Orange),
                contentAlignment = Alignment.Center
            ) {
                Text("Header")
            }
            
            Box(
                modifier = Modifier
                    .weight(3f) // 3 veces más espacio
                    .fillMaxWidth()
                    .background(Color.Purple),
                contentAlignment = Alignment.Center
            ) {
                Text("Content", color = Color.White)
            }
            
            Box(
                modifier = Modifier
                    .weight(1f)
                    .fillMaxWidth()
                    .background(Color.Brown),
                contentAlignment = Alignment.Center
            ) {
                Text("Footer", color = Color.White)
            }
        }
    }
}
```

---

### 6. Infinity - Dimensiones infinitas

```kotlin
@Composable
fun InfinityExamples() {
    Column(modifier = Modifier.padding(16.dp)) {
        Text("Dimensiones infinitas (cuidado)")
        
        // LazyColumn maneja internamente dimensiones infinitas
        LazyColumn(
            modifier = Modifier
                .fillMaxWidth()
                .height(200.dp), // Altura limitada para el ejemplo
            verticalArrangement = Arrangement.spacedBy(8.dp)
        ) {
            items(50) { index ->
                Text(
                    text = "Item $index",
                    modifier = Modifier
                        .fillMaxWidth()
                        .background(Color.LightGray)
                        .padding(16.dp)
                )
            }
        }
        
        // ❌ EVITAR: Dimensiones infinitas sin restricción
        // ScrollableColumn { // Esto causaría problemas
        //     repeat(1000) {
        //         Text("Item $it")
        //     }
        // }
    }
}
```

---

## Conversión entre unidades

### Funciones de conversión útiles
```kotlin
@Composable
fun UnitConversions() {
    val density = LocalDensity.current
    
    Column(modifier = Modifier.padding(16.dp)) {
        Text("Conversiones de unidades")
        
        with(density) {
            val dpValue = 48.dp
            val pxValue = dpValue.toPx() // Convertir dp a píxeles
            val spValue = 16.sp
            val spToPx = spValue.toPx() // Convertir sp a píxeles
            
            Text("48dp = ${pxValue}px en esta pantalla")
            Text("16sp = ${spToPx}px con la configuración actual")
            
            // Conversión inversa
            val pxToDp = 96.toDp() // Convertir píxeles a dp
            val pxToSp = 64.toSp() // Convertir píxeles a sp
            
            Text("96px = ${pxToDp} en esta pantalla")
            Text("64px = ${pxToSp} con la configuración actual")
        }
    }
}
```

### Utilidades para responsive design
```kotlin
@Composable
fun ResponsiveDesignUtils() {
    val configuration = LocalConfiguration.current
    val screenWidth = configuration.screenWidthDp.dp
    val screenHeight = configuration.screenHeightDp.dp
    
    // Tamaños adaptativos basados en el ancho de pantalla
    val cardPadding = when {
        screenWidth < 600.dp -> 8.dp    // Móvil
        screenWidth < 840.dp -> 16.dp   // Tablet pequeño
        else -> 24.dp                   // Tablet grande / Desktop
    }
    
    val textSize = when {
        screenWidth < 600.dp -> 14.sp   // Móvil
        else -> 16.sp                   // Tablet+
    }
    
    Column(
        modifier = Modifier.padding(cardPadding),
        verticalArrangement = Arrangement.spacedBy(8.dp)
    ) {
        Text(
            text = "Diseño responsivo",
            fontSize = textSize
        )
        
        Text(
            text = "Ancho de pantalla: $screenWidth",
            fontSize = (textSize.value - 2).sp
        )
        
        Text(
            text = "Altura de pantalla: $screenHeight",
            fontSize = (textSize.value - 2).sp
        )
        
        Card(
            modifier = Modifier
                .fillMaxWidth()
                .padding(cardPadding)
        ) {
            Text(
                "Card con padding adaptativo",
                modifier = Modifier.padding(cardPadding)
            )
        }
    }
}
```

---

## Mejores prácticas

### ✅ Hacer

#### 1. Usar dp para dimensiones físicas
```kotlin
@Composable
fun GoodDpUsage() {
    Column {
        // ✅ BIEN: Tamaños de elementos UI
        IconButton(
            onClick = {},
            modifier = Modifier.size(48.dp) // Área táctil mínima
        ) {
            Icon(Icons.Default.Menu, contentDescription = "Menu")
        }
        
        // ✅ BIEN: Espaciado consistente
        Spacer(modifier = Modifier.height(16.dp))
        
        // ✅ BIEN: Bordes y elevación
        Card(
            elevation = CardDefaults.cardElevation(defaultElevation = 4.dp),
            modifier = Modifier.padding(8.dp)
        ) {
            Text("Contenido", modifier = Modifier.padding(16.dp))
        }
    }
}
```

#### 2. Usar sp para texto
```kotlin
@Composable
fun GoodSpUsage() {
    Column {
        // ✅ BIEN: Tamaños de fuente
        Text("Título", fontSize = 24.sp)
        Text("Subtítulo", fontSize = 16.sp)
        Text("Cuerpo", fontSize = 14.sp)
        
        // ✅ BIEN: Espaciado relacionado con texto
        Text(
            text = "Líneas múltiples\ncon espaciado apropiado",
            fontSize = 16.sp,
            lineHeight = 24.sp // Proporcional al texto
        )
    }
}
```

#### 3. Definir constantes reutilizables
```kotlin
object AppDimensions {
    // Espaciado
    val spacingXs = 4.dp
    val spacingS = 8.dp
    val spacingM = 16.dp
    val spacingL = 24.dp
    val spacingXl = 32.dp
    
    // Tamaños de elementos
    val buttonHeight = 48.dp
    val iconSize = 24.dp
    val avatarSize = 40.dp
    
    // Esquinas y bordes
    val cornerRadius = 8.dp
    val borderWidth = 1.dp
    
    // Elevación
    val elevationCard = 4.dp
    val elevationFab = 8.dp
}

object AppTextSizes {
    val caption = 12.sp
    val body = 14.sp
    val subtitle = 16.sp
    val title = 20.sp
    val headline = 24.sp
}

@Composable
fun UsingConstants() {
    Card(
        elevation = CardDefaults.cardElevation(
            defaultElevation = AppDimensions.elevationCard
        ),
        shape = RoundedCornerShape(AppDimensions.cornerRadius),
        modifier = Modifier.padding(AppDimensions.spacingM)
    ) {
        Column(
            modifier = Modifier.padding(AppDimensions.spacingM),
            verticalArrangement = Arrangement.spacedBy(AppDimensions.spacingS)
        ) {
            Text("Título", fontSize = AppTextSizes.title)
            Text("Contenido", fontSize = AppTextSizes.body)
        }
    }
}
```

### ❌ Evitar

#### 1. Mezclar unidades incorrectamente
```kotlin
@Composable
fun BadUnitMixing() {
    Column {
        // ❌ MAL: Usar dp para texto
        Text(
            text = "Texto mal dimensionado",
            fontSize = TextUnit(16f, TextUnitType.Dp) // No escalará con preferencias
        )
        
        // ❌ MAL: Usar sp para elementos UI
        Box(
            modifier = Modifier
                .size(48.sp) // Se distorsiona con configuración de fuente
                .background(Color.Blue)
        )
        
        // ❌ MAL: Usar px sin razón específica
        Divider(thickness = 2.px) // Inconsistente entre dispositivos
    }
}
```

#### 2. Valores hardcodeados sin consistencia
```kotlin
@Composable
fun InconsistentSizing() {
    Column {
        // ❌ MAL: Valores random sin consistencia
        Text("Texto 1", modifier = Modifier.padding(13.dp))
        Text("Texto 2", modifier = Modifier.padding(17.dp))
        Text("Texto 3", modifier = Modifier.padding(11.dp))
        
        // ❌ MAL: No seguir múltiplos estándar
        Spacer(modifier = Modifier.height(13.dp))
        Spacer(modifier = Modifier.height(19.dp))
    }
}
```

#### 3. Ignorar densidad y accesibilidad
```kotlin
@Composable
fun AccessibilityIgnored() {
    // ❌ MAL: Elementos demasiado pequeños para tocar
    IconButton(
        onClick = {},
        modifier = Modifier.size(32.dp) // Menor al mínimo recomendado (48dp)
    ) {
        Icon(Icons.Default.Add, contentDescription = null)
    }
    
    // ❌ MAL: Texto demasiado pequeño
    Text(
        text = "Texto ilegible",
        fontSize = 8.sp // Demasiado pequeño para leer
    )
}
```

---

## Guía de referencia rápida

### Tabla de conversión aproximada

| Densidad | dp a px | Descripción |
|----------|---------|-------------|
| ldpi | 1 dp = 0.75 px | 120 DPI |
| mdpi | 1 dp = 1 px | 160 DPI (referencia) |
| hdpi | 1 dp = 1.5 px | 240 DPI |
| xhdpi | 1 dp = 2 px | 320 DPI |
| xxhdpi | 1 dp = 3 px | 480 DPI |
| xxxhdpi | 1 dp = 4 px | 640 DPI |

### Valores recomendados

#### Espaciado (dp)
```kotlin
val spacing = mapOf(
    "xs" to 4.dp,     // Espaciado mínimo
    "s" to 8.dp,      // Espaciado pequeño
    "m" to 16.dp,     // Espaciado estándar
    "l" to 24.dp,     // Espaciado grande
    "xl" to 32.dp,    // Espaciado extra grande
    "xxl" to 48.dp    // Espaciado máximo
)
```

#### Tamaños de fuente (sp)
```kotlin
val textSizes = mapOf(
    "caption" to 12.sp,    // Texto secundario pequeño
    "body2" to 14.sp,      // Texto secundario
    "body1" to 16.sp,      // Texto principal
    "subtitle2" to 14.sp,  // Subtítulo pequeño
    "subtitle1" to 16.sp,  // Subtítulo
    "h6" to 20.sp,         // Encabezado pequeño
    "h5" to 24.sp,         // Encabezado mediano
    "h4" to 34.sp,         // Encabezado grande
    "h3" to 48.sp,         // Título de pantalla
    "h2" to 60.sp,         // Título destacado
    "h1" to 96.sp          // Display text
)
```

#### Tamaños de elementos (dp)
```kotlin
val elementSizes = mapOf(
    "iconSmall" to 16.dp,      // Iconos pequeños
    "iconMedium" to 24.dp,     // Iconos estándar
    "iconLarge" to 32.dp,      // Iconos grandes
    "buttonHeight" to 48.dp,   // Altura de botones
    "touchTarget" to 48.dp,    // Área táctil mínima
    "avatarSmall" to 32.dp,    // Avatar pequeño
    "avatarMedium" to 48.dp,   // Avatar estándar
    "avatarLarge" to 64.dp     // Avatar grande
)
```

## Resumen

### Cuándo usar cada unidad:

- **Dp**: Dimensiones físicas, espaciado, tamaños de elementos UI, bordes, elevación
- **Sp**: Tamaños de fuente, espaciado de líneas, espaciado de letras
- **TextUnit**: Cuando necesites flexibilidad entre sp y em
- **Fill/Weight**: Layouts flexibles y responsivos
- **WrapContent**: Cuando el tamaño debe ajustarse al contenido
- **Px**: Solo en casos muy específicos (líneas de 1px, efectos especiales)

### Principios clave:

1. **Consistencia**: Usa múltiplos de 4dp o 8dp para espaciado
2. **Accesibilidad**: Respeta tamaños mínimos táctiles (48dp) y de fuente (12sp)
3. **Responsividad**: Combina unidades fijas con flexibles según el contexto
4. **Legibilidad**: Usa sp para todo lo relacionado con texto
5. **Performance**: Evita cálculos complejos de unidades en cada recomposición

Elegir las unidades correctas es fundamental para crear aplicaciones que se vean y funcionen bien en todos los dispositivos Android.