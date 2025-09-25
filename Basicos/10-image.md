# Componente Text en Jetpack Compose - Guía Completa

El componente `Text` es uno de los elementos más fundamentales en Jetpack Compose. Es responsable de mostrar texto en la interfaz de usuario y ofrece una gran cantidad de opciones de personalización.

## ¿Qué es el componente Text?

`Text` es un Composable que renderiza texto estático en la pantalla. Es el equivalente a `TextView` en el sistema de vistas tradicional de Android, pero optimizado para Compose.

### Características principales:
- **Renderizado eficiente** de texto
- **Soporte completo de tipografía** Material Design
- **Personalización avanzada** de estilos, colores y layout
- **Accesibilidad integrada**
- **Soporte para texto multi-idioma**
- **Animaciones de texto** fluidas

## Sintaxis básica

```kotlin
Text(text = "Hola Mundo")
```

## Parámetros principales

### Estructura completa del componente

```kotlin
Text(
    text = "Mi texto",                           // Contenido del texto
    modifier = Modifier,                         // Modificadores de layout y estilo
    color = Color.Unspecified,                   // Color del texto
    fontSize = TextUnit.Unspecified,             // Tamaño de la fuente
    fontStyle = null,                           // Estilo: normal, italic
    fontWeight = null,                          // Peso: normal, bold, etc.
    fontFamily = null,                          // Familia de fuente
    letterSpacing = TextUnit.Unspecified,       // Espaciado entre caracteres
    textDecoration = null,                      // Decoración: underline, strikethrough
    textAlign = null,                           // Alineación del texto
    lineHeight = TextUnit.Unspecified,          // Altura de línea
    overflow = TextOverflow.Clip,               // Comportamiento de desbordamiento
    softWrap = true,                            // Salto de línea automático
    maxLines = Int.MAX_VALUE,                   // Número máximo de líneas
    minLines = 1,                               // Número mínimo de líneas
    onTextLayout = null,                        // Callback de layout
    style = LocalTextStyle.current              // Estilo base
)
```

## Ejemplos básicos

### Texto simple
```kotlin
@Composable
fun SimpleText() {
    Text(text = "Este es un texto básico")
}
```

### Texto con estilo personalizado
```kotlin
@Composable
fun StyledText() {
    Text(
        text = "Texto con estilo",
        fontSize = 24.sp,
        color = Color.Blue,
        fontWeight = FontWeight.Bold
    )
}
```

### Texto con múltiples líneas
```kotlin
@Composable
fun MultilineText() {
    Text(
        text = "Este es un texto muy largo que se dividirá automáticamente en múltiples líneas para adaptarse al ancho disponible del contenedor.",
        maxLines = 3,
        overflow = TextOverflow.Ellipsis
    )
}
```

## Tipografía y estilos predefinidos

### Usando Material Theme Typography
```kotlin
@Composable
fun TypographyExamples() {
    Column(
        verticalArrangement = Arrangement.spacedBy(8.dp),
        modifier = Modifier.padding(16.dp)
    ) {
        Text(
            text = "Display Large",
            style = MaterialTheme.typography.displayLarge
        )
        Text(
            text = "Headline Medium",
            style = MaterialTheme.typography.headlineMedium
        )
        Text(
            text = "Title Large",
            style = MaterialTheme.typography.titleLarge
        )
        Text(
            text = "Body Large",
            style = MaterialTheme.typography.bodyLarge
        )
        Text(
            text = "Body Medium",
            style = MaterialTheme.typography.bodyMedium
        )
        Text(
            text = "Body Small",
            style = MaterialTheme.typography.bodySmall
        )
        Text(
            text = "Label Large",
            style = MaterialTheme.typography.labelLarge
        )
        Text(
            text = "Label Medium",
            style = MaterialTheme.typography.labelMedium
        )
        Text(
            text = "Label Small",
            style = MaterialTheme.typography.labelSmall
        )
    }
}
```

### Estilos de tipografía disponibles

| Estilo | Uso recomendado |
|--------|-----------------|
| `displayLarge` | Títulos muy grandes, splash screens |
| `displayMedium` | Títulos principales |
| `displaySmall` | Títulos secundarios |
| `headlineLarge` | Headers importantes |
| `headlineMedium` | Subtítulos principales |
| `headlineSmall` | Subtítulos secundarios |
| `titleLarge` | Títulos de secciones |
| `titleMedium` | Títulos de cards o items |
| `titleSmall` | Títulos pequeños |
| `bodyLarge` | Texto principal grande |
| `bodyMedium` | Texto principal estándar |
| `bodySmall` | Texto secundario |
| `labelLarge` | Labels de botones grandes |
| `labelMedium` | Labels estándar |
| `labelSmall` | Labels pequeños, captions |

## Personalización de colores

### Colores básicos
```kotlin
@Composable
fun ColorExamples() {
    Column(verticalArrangement = Arrangement.spacedBy(8.dp)) {
        Text(
            text = "Texto rojo",
            color = Color.Red
        )
        Text(
            text = "Texto verde",
            color = Color(0xFF4CAF50)
        )
        Text(
            text = "Color del tema",
            color = MaterialTheme.colorScheme.primary
        )
        Text(
            text = "Color con opacidad",
            color = Color.Black.copy(alpha = 0.6f)
        )
    }
}
```

### Colores del tema Material
```kotlin
@Composable
fun ThemeColorExamples() {
    val colorScheme = MaterialTheme.colorScheme
    
    Column(verticalArrangement = Arrangement.spacedBy(8.dp)) {
        Text("Primary", color = colorScheme.primary)
        Text("Secondary", color = colorScheme.secondary)
        Text("Tertiary", color = colorScheme.tertiary)
        Text("Error", color = colorScheme.error)
        Text("On Background", color = colorScheme.onBackground)
        Text("On Surface", color = colorScheme.onSurface)
        Text("Outline", color = colorScheme.outline)
    }
}
```

## Formateo de texto avanzado

### Peso y estilo de fuente
```kotlin
@Composable
fun FontStyleExamples() {
    Column(verticalArrangement = Arrangement.spacedBy(8.dp)) {
        Text("Peso Light", fontWeight = FontWeight.Light)
        Text("Peso Normal", fontWeight = FontWeight.Normal)
        Text("Peso Medium", fontWeight = FontWeight.Medium)
        Text("Peso SemiBold", fontWeight = FontWeight.SemiBold)
        Text("Peso Bold", fontWeight = FontWeight.Bold)
        Text("Peso ExtraBold", fontWeight = FontWeight.ExtraBold)
        Text("Estilo Italic", fontStyle = FontStyle.Italic)
        Text("Estilo Normal", fontStyle = FontStyle.Normal)
    }
}
```

### Decoraciones de texto
```kotlin
@Composable
fun TextDecorationExamples() {
    Column(verticalArrangement = Arrangement.spacedBy(8.dp)) {
        Text(
            text = "Texto subrayado",
            textDecoration = TextDecoration.Underline
        )
        Text(
            text = "Texto tachado",
            textDecoration = TextDecoration.LineThrough
        )
        Text(
            text = "Subrayado y tachado",
            textDecoration = TextDecoration.Underline + TextDecoration.LineThrough
        )
    }
}
```

### Espaciado de caracteres y líneas
```kotlin
@Composable
fun SpacingExamples() {
    Column(verticalArrangement = Arrangement.spacedBy(12.dp)) {
        Text(
            text = "Espaciado normal de caracteres",
            letterSpacing = 0.sp
        )
        Text(
            text = "E s p a c i a d o   a m p l i o",
            letterSpacing = 4.sp
        )
        Text(
            text = "Texto con altura de línea normal\nSegunda línea del texto\nTercera línea",
            lineHeight = 20.sp
        )
        Text(
            text = "Texto con altura de línea amplia\nSegunda línea del texto\nTercera línea",
            lineHeight = 32.sp
        )
    }
}
```

## Alineación del texto

### Alineaciones horizontales
```kotlin
@Composable
fun TextAlignmentExamples() {
    Column(
        modifier = Modifier
            .fillMaxWidth()
            .padding(16.dp),
        verticalArrangement = Arrangement.spacedBy(8.dp)
    ) {
        Text(
            text = "Texto alineado a la izquierda",
            textAlign = TextAlign.Start,
            modifier = Modifier
                .fillMaxWidth()
                .background(Color.LightGray.copy(alpha = 0.3f))
                .padding(8.dp)
        )
        Text(
            text = "Texto centrado",
            textAlign = TextAlign.Center,
            modifier = Modifier
                .fillMaxWidth()
                .background(Color.LightGray.copy(alpha = 0.3f))
                .padding(8.dp)
        )
        Text(
            text = "Texto alineado a la derecha",
            textAlign = TextAlign.End,
            modifier = Modifier
                .fillMaxWidth()
                .background(Color.LightGray.copy(alpha = 0.3f))
                .padding(8.dp)
        )
        Text(
            text = "Este texto está justificado y se distribuye uniformemente a lo ancho del contenedor cuando es lo suficientemente largo",
            textAlign = TextAlign.Justify,
            modifier = Modifier
                .fillMaxWidth()
                .background(Color.LightGray.copy(alpha = 0.3f))
                .padding(8.dp)
        )
    }
}
```

## Manejo del desbordamiento (Overflow)

### Opciones de overflow
```kotlin
@Composable
fun OverflowExamples() {
    val longText = "Este es un texto muy largo que definitivamente no cabrá en una sola línea y causará desbordamiento"
    
    Column(
        modifier = Modifier.width(200.dp),
        verticalArrangement = Arrangement.spacedBy(16.dp)
    ) {
        // Clip - Corta el texto
        Text(
            text = "Clip: $longText",
            maxLines = 1,
            overflow = TextOverflow.Clip,
            modifier = Modifier
                .background(Color.Yellow.copy(alpha = 0.3f))
                .padding(4.dp)
        )
        
        // Ellipsis - Agrega puntos suspensivos
        Text(
            text = "Ellipsis: $longText",
            maxLines = 1,
            overflow = TextOverflow.Ellipsis,
            modifier = Modifier
                .background(Color.Green.copy(alpha = 0.3f))
                .padding(4.dp)
        )
        
        // Visible - Permite que se desborde
        Text(
            text = "Visible: $longText",
            maxLines = 1,
            overflow = TextOverflow.Visible,
            modifier = Modifier
                .background(Color.Blue.copy(alpha = 0.3f))
                .padding(4.dp)
        )
    }
}
```

### Control de líneas
```kotlin
@Composable
fun LineControlExamples() {
    val mediumText = "Este es un texto de longitud media que puede ocupar varias líneas dependiendo del ancho del contenedor."
    
    Column(
        modifier = Modifier.width(250.dp),
        verticalArrangement = Arrangement.spacedBy(16.dp)
    ) {
        Text(
            text = "Máximo 2 líneas:\n$mediumText",
            maxLines = 2,
            overflow = TextOverflow.Ellipsis
        )
        
        Text(
            text = "Mínimo 3 líneas:\n$mediumText",
            minLines = 3
        )
        
        Text(
            text = "Sin salto de línea automático: $mediumText",
            softWrap = false,
            overflow = TextOverflow.Ellipsis
        )
    }
}
```

## Texto seleccionable

### Habilitando selección
```kotlin
@Composable
fun SelectableTextExamples() {
    Column(verticalArrangement = Arrangement.spacedBy(16.dp)) {
        Text(
            text = "Este texto NO es seleccionable"
        )
        
        SelectionContainer {
            Text(
                text = "Este texto SÍ es seleccionable. Mantén presionado para seleccionar."
            )
        }
        
        SelectionContainer {
            Column {
                Text("Primer párrafo seleccionable")
                Text("Segundo párrafo también seleccionable")
            }
        }
        
        // Deshabilitar selección para parte del contenido
        SelectionContainer {
            Column {
                Text("Texto seleccionable")
                DisableSelection {
                    Text("Este texto NO es seleccionable dentro del contenedor")
                }
                Text("Más texto seleccionable")
            }
        }
    }
}
```

## Texto clickeable

### ClickableText básico
```kotlin
@Composable
fun ClickableTextExample() {
    val annotatedText = buildAnnotatedString {
        append("Este es un texto normal con un ")
        
        // Parte clickeable
        pushStringAnnotation(
            tag = "clickable",
            annotation = "Este es el texto clickeable"
        )
        withStyle(
            style = SpanStyle(
                color = Color.Blue,
                textDecoration = TextDecoration.Underline
            )
        ) {
            append("enlace clickeable")
        }
        pop()
        
        append(" en el medio.")
    }
    
    ClickableText(
        text = annotatedText,
        onClick = { offset ->
            annotatedText.getStringAnnotations(
                tag = "clickable",
                start = offset,
                end = offset
            ).firstOrNull()?.let {
                // Manejar el clic en el texto
                println("Clicked on: ${it.item}")
            }
        }
    )
}
```

### Múltiples enlaces en un texto
```kotlin
@Composable
fun MultipleLinksExample() {
    val annotatedText = buildAnnotatedString {
        append("Visita nuestro ")
        
        // Primer enlace
        pushStringAnnotation(tag = "website", annotation = "https://example.com")
        withStyle(
            style = SpanStyle(
                color = Color.Blue,
                textDecoration = TextDecoration.Underline
            )
        ) {
            append("sitio web")
        }
        pop()
        
        append(" o síguenos en ")
        
        // Segundo enlace
        pushStringAnnotation(tag = "twitter", annotation = "https://twitter.com/example")
        withStyle(
            style = SpanStyle(
                color = Color.Blue,
                textDecoration = TextDecoration.Underline
            )
        ) {
            append("Twitter")
        }
        pop()
        
        append(" para más información.")
    }
    
    ClickableText(
        text = annotatedText,
        onClick = { offset ->
            // Verificar enlace de sitio web
            annotatedText.getStringAnnotations(
                tag = "website",
                start = offset,
                end = offset
            ).firstOrNull()?.let { annotation ->
                // Abrir navegador
                println("Opening website: ${annotation.item}")
            }
            
            // Verificar enlace de Twitter
            annotatedText.getStringAnnotations(
                tag = "twitter",
                start = offset,
                end = offset
            ).firstOrNull()?.let { annotation ->
                // Abrir Twitter
                println("Opening Twitter: ${annotation.item}")
            }
        }
    )
}
```

## Texto con formato rich (AnnotatedString)

### Estilos múltiples en un solo texto
```kotlin
@Composable
fun RichTextExample() {
    val styledText = buildAnnotatedString {
        withStyle(style = SpanStyle(fontSize = 24.sp, fontWeight = FontWeight.Bold)) {
            append("Título Principal\n")
        }
        
        withStyle(style = SpanStyle(fontSize = 16.sp, color = Color.Gray)) {
            append("Subtítulo en gris\n\n")
        }
        
        append("Este es texto normal con ")
        
        withStyle(style = SpanStyle(fontWeight = FontWeight.Bold)) {
            append("texto en negrita")
        }
        
        append(" y ")
        
        withStyle(
            style = SpanStyle(
                fontStyle = FontStyle.Italic,
                color = Color.Red
            )
        ) {
            append("texto en cursiva roja")
        }
        
        append(".\n\nTambién podemos tener ")
        
        withStyle(
            style = SpanStyle(
                background = Color.Yellow,
                color = Color.Black
            )
        ) {
            append("texto resaltado")
        }
        
        append(" como si fuera un marcador.")
    }
    
    Text(text = styledText)
}
```

### Párrafos con estilos diferentes
```kotlin
@Composable
fun ParagraphStyledText() {
    val styledText = buildAnnotatedString {
        withStyle(
            style = ParagraphStyle(
                textAlign = TextAlign.Center,
                lineHeight = 30.sp
            )
        ) {
            withStyle(
                style = SpanStyle(
                    fontSize = 20.sp,
                    fontWeight = FontWeight.Bold
                )
            ) {
                append("Párrafo centrado\n")
            }
            append("Este párrafo está centrado y tiene un espaciado de línea mayor.\n\n")
        }
        
        withStyle(
            style = ParagraphStyle(
                textAlign = TextAlign.Justify,
                textIndent = TextIndent(firstLine = 16.sp)
            )
        ) {
            append("Este párrafo está justificado y tiene una sangría en la primera línea. " +
                   "Este tipo de formato es útil para crear texto que parece más formal o similar a un documento.\n\n")
        }
        
        withStyle(
            style = ParagraphStyle(
                textAlign = TextAlign.End
            )
        ) {
            append("Este párrafo está alineado a la derecha.")
        }
    }
    
    Text(
        text = styledText,
        modifier = Modifier
            .fillMaxWidth()
            .padding(16.dp)
    )
}
```

## Familias de fuentes personalizadas

### Usando fuentes del sistema
```kotlin
@Composable
fun SystemFontExamples() {
    Column(verticalArrangement = Arrangement.spacedBy(8.dp)) {
        Text(
            text = "Fuente Default",
            fontFamily = FontFamily.Default
        )
        Text(
            text = "Fuente Serif",
            fontFamily = FontFamily.Serif
        )
        Text(
            text = "Fuente Sans Serif",
            fontFamily = FontFamily.SansSerif
        )
        Text(
            text = "Fuente Monospace",
            fontFamily = FontFamily.Monospace
        )
        Text(
            text = "Fuente Cursive",
            fontFamily = FontFamily.Cursive
        )
    }
}
```

### Fuentes personalizadas (ejemplo conceptual)
```kotlin
// Definir la familia de fuentes personalizada
val customFontFamily = FontFamily(
    Font(R.font.my_regular_font, FontWeight.Normal),
    Font(R.font.my_bold_font, FontWeight.Bold),
    Font(R.font.my_italic_font, FontWeight.Normal, FontStyle.Italic)
)

@Composable
fun CustomFontExample() {
    Column(verticalArrangement = Arrangement.spacedBy(8.dp)) {
        Text(
            text = "Texto con fuente personalizada normal",
            fontFamily = customFontFamily,
            fontWeight = FontWeight.Normal
        )
        Text(
            text = "Texto con fuente personalizada en negrita",
            fontFamily = customFontFamily,
            fontWeight = FontWeight.Bold
        )
        Text(
            text = "Texto con fuente personalizada en cursiva",
            fontFamily = customFontFamily,
            fontStyle = FontStyle.Italic
        )
    }
}
```

## Casos de uso prácticos

### Lista de elementos con texto estructurado
```kotlin
data class NewsItem(
    val title: String,
    val author: String,
    val time: String,
    val content: String
)

@Composable
fun NewsItemCard(item: NewsItem) {
    Card(
        modifier = Modifier
            .fillMaxWidth()
            .padding(8.dp)
    ) {
        Column(modifier = Modifier.padding(16.dp)) {
            // Título
            Text(
                text = item.title,
                style = MaterialTheme.typography.headlineSmall,
                maxLines = 2,
                overflow = TextOverflow.Ellipsis
            )
            
            Spacer(modifier = Modifier.height(8.dp))
            
            // Información del autor y tiempo
            Row(
                modifier = Modifier.fillMaxWidth(),
                horizontalArrangement = Arrangement.SpaceBetween
            ) {
                Text(
                    text = "Por ${item.author}",
                    style = MaterialTheme.typography.labelMedium,
                    color = MaterialTheme.colorScheme.primary
                )
                Text(
                    text = item.time,
                    style = MaterialTheme.typography.labelSmall,
                    color = MaterialTheme.colorScheme.onSurfaceVariant
                )
            }
            
            Spacer(modifier = Modifier.height(12.dp))
            
            // Contenido
            Text(
                text = item.content,
                style = MaterialTheme.typography.bodyMedium,
                maxLines = 3,
                overflow = TextOverflow.Ellipsis,
                lineHeight = 20.sp
            )
        }
    }
}
```

### Texto de estado con diferentes colores
```kotlin
enum class Status { SUCCESS, WARNING, ERROR, LOADING }

@Composable
fun StatusText(status: Status, message: String) {
    val (color, icon) = when (status) {
        Status.SUCCESS -> Color(0xFF4CAF50) to "✓"
        Status.WARNING -> Color(0xFFFF9800) to "⚠"
        Status.ERROR -> Color(0xFFF44336) to "✗"
        Status.LOADING -> Color(0xFF2196F3) to "⏳"
    }
    
    Text(
        text = "$icon $message",
        color = color,
        fontWeight = FontWeight.Medium,
        modifier = Modifier.padding(8.dp)
    )
}

@Composable
fun StatusExamples() {
    Column {
        StatusText(Status.SUCCESS, "Operación completada exitosamente")
        StatusText(Status.WARNING, "Advertencia: Revisa los datos")
        StatusText(Status.ERROR, "Error: No se pudo conectar")
        StatusText(Status.LOADING, "Cargando datos...")
    }
}
```

### Chat con texto formateado
```kotlin
@Composable
fun ChatMessage(
    message: String,
    sender: String,
    time: String,
    isCurrentUser: Boolean
) {
    val backgroundColor = if (isCurrentUser) {
        MaterialTheme.colorScheme.primary
    } else {
        MaterialTheme.colorScheme.surfaceVariant
    }
    
    val contentColor = if (isCurrentUser) {
        MaterialTheme.colorScheme.onPrimary
    } else {
        MaterialTheme.colorScheme.onSurfaceVariant
    }
    
    Card(
        modifier = Modifier
            .fillMaxWidth(0.8f)
            .padding(4.dp),
        colors = CardDefaults.cardColors(
            containerColor = backgroundColor
        )
    ) {
        Column(
            modifier = Modifier.padding(12.dp)
        ) {
            if (!isCurrentUser) {
                Text(
                    text = sender,
                    style = MaterialTheme.typography.labelSmall,
                    color = contentColor.copy(alpha = 0.7f),
                    fontWeight = FontWeight.Bold
                )
                Spacer(modifier = Modifier.height(4.dp))
            }
            
            Text(
                text = message,
                style = MaterialTheme.typography.bodyMedium,
                color = contentColor
            )
            
            Spacer(modifier = Modifier.height(4.dp))
            
            Text(
                text = time,
                style = MaterialTheme.typography.labelSmall,
                color = contentColor.copy(alpha = 0.6f),
                textAlign = if (isCurrentUser) TextAlign.End else TextAlign.Start,
                modifier = Modifier.fillMaxWidth()
            )
        }
    }
}
```

## Accesibilidad

### Mejores prácticas de accesibilidad
```kotlin
@Composable
fun AccessibleTextExamples() {
    Column(verticalArrangement = Arrangement.spacedBy(16.dp)) {
        // Texto con descripción semántica
        Text(
            text = "Título principal",
            style = MaterialTheme.typography.headlineMedium,
            modifier = Modifier.semantics {
                heading()  // Marca como encabezado para lectores de pantalla
            }
        )
        
        // Texto de estado con información adicional para accesibilidad
        Text(
            text = "Error: Campo obligatorio",
            color = MaterialTheme.colorScheme.error,
            modifier = Modifier.semantics {
                contentDescription = "Error: El campo de nombre es obligatorio y debe completarse"
                role = Role.Text
            }
        )
        
        // Texto con contraste adecuado
        Text(
            text = "Texto con contraste apropiado",
            color = MaterialTheme.colorScheme.onBackground,
            style = MaterialTheme.typography.bodyLarge
        )
        
        // Evitar texto demasiado pequeño
        Text(
            text = "Texto con tamaño mínimo recomendado",
            fontSize = 16.sp  // Tamaño mínimo recomendado para legibilidad
        )
    }
}
```

## Performance y optimizaciones

### Evitar recomposiciones innecesarias
```kotlin
@Composable
fun OptimizedTextDisplay(
    items: List<String>,
    selectedItem: String
) {
    LazyColumn {
        items(
            items = items,
            key = { item -> item }  // Key estable para evitar recomposiciones
        ) { item ->
            val isSelected = item == selectedItem
            val textStyle = if (isSelected) {
                MaterialTheme.typography.bodyLarge.copy(fontWeight = FontWeight.Bold)
            } else {
                MaterialTheme.typography.bodyMedium
            }
            
            Text(
                text = item,
                style = textStyle,
                color = if (isSelected) {
                    MaterialTheme.colorScheme.primary
                } else {
                    MaterialTheme.colorScheme.onSurface
                },
                modifier = Modifier
                    .fillMaxWidth()
                    .padding(16.dp)
            )
        }
    }
}
```

### Reutilización de estilos
```kotlin
// Definir estilos reutilizables
object AppTextStyles {
    val cardTitle = TextStyle(
        fontSize = 18.sp,
        fontWeight = FontWeight.SemiBold,
        lineHeight = 24.sp
    )
    
    val cardSubtitle = TextStyle(
        fontSize = 14.sp,
        fontWeight = FontWeight.Normal,
        lineHeight = 20.sp
    )
    
    val caption = TextStyle(
        fontSize = 12.sp,
        fontWeight = FontWeight.Normal,
        lineHeight = 16.sp
    )
}

@Composable
fun ReusableStylesExample() {
    Card {
        Column(modifier = Modifier.padding(16.dp)) {
            Text(
                text = "Título de la tarjeta",
                style = AppTextStyles.cardTitle,
                color = MaterialTheme.colorScheme.onSurface
            )
            Text(
                text = "Subtítulo explicativo",
                style = AppTextStyles.cardSubtitle,
                color = MaterialTheme.colorScheme.onSurfaceVariant
            )
            Text(
                text = "Información adicional",
                style = AppTextStyles.caption,
                color = MaterialTheme.colorScheme.outline
            )
        }
    }
}
```

## Mejores prácticas

### ✅ Hacer
1. **Usar estilos de tipografía** del MaterialTheme cuando sea posible
2. **Proporcionar contentDescription** para accesibilidad cuando sea necesario
3. **Limitar maxLines** para textos que pueden ser muy largos
4. **Usar overflow = TextOverflow.Ellipsis** para texto truncado
5. **Mantener contraste adecuado** entre texto y fondo
6. **Reutilizar estilos** para consistencia
7. **Considerar el tamaño mínimo** de 16.sp para legibilidad

### ❌ Evitar
1. **No usar tamaños de texto demasiado pequeños** (menor a 12.sp)
2. **No abusar del texto en cursiva** - reduce legibilidad
3. **No usar colores con contraste insuficiente**
4. **No crear demasiados estilos custom** sin necesidad
5. **No olvidar maxLines** en listas o cards
6. **No usar fontWeight extremos** sin razón de diseño
7. **No ignorar el espaciado** entre elementos de texto

## Resumen

El componente `Text` en Jetpack Compose es extremadamente versátil y potente:

- **Tipografía Material Design** integrada
- **Personalización completa** de estilos, colores y formateo
- **Soporte para texto rico** con múltiples estilos
- **Funcionalidad de selección y clic**
- **Optimizaciones de performance** incorporadas
- **Accesibilidad** de primera clase

Dominar el componente `Text` es esencial para crear interfaces de usuario atractivas y funcionales en Compose, ya que el texto es uno de los elementos más importantes para comunicar información a los usuarios.