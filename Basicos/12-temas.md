# Temas en Jetpack Compose - Guía Completa

Los temas en Jetpack Compose proporcionan una forma consistente de aplicar colores, tipografía y formas a través de toda la aplicación. Esta guía explica cómo crear, personalizar y usar temas efectivamente.

## ¿Qué es un tema en Compose?

Un tema en Compose define la apariencia visual global de tu aplicación mediante tres pilares principales:
- **Color Scheme** - Paleta de colores
- **Typography** - Estilos de texto
- **Shapes** - Formas de componentes

## Estructura básica de MaterialTheme

```kotlin
@Composable
fun MyApp() {
    MaterialTheme(
        colorScheme = lightColorScheme(), // Esquema de colores
        typography = Typography(),        // Estilos de tipografía
        shapes = Shapes(),               // Formas de componentes
        content = {
            // Tu contenido aquí
            MyAppContent()
        }
    )
}
```

## 1. Color Schemes (Esquemas de Color)

### Color Scheme básico de Material 3

```kotlin
@Composable
fun BasicColorSchemeExample() {
    // Esquema de colores claro predeterminado
    val lightColors = lightColorScheme(
        primary = Color(0xFF6750A4),
        onPrimary = Color(0xFFFFFFFF),
        primaryContainer = Color(0xFFEADDFF),
        onPrimaryContainer = Color(0xFF21005D),
        secondary = Color(0xFF625B71),
        onSecondary = Color(0xFFFFFFFF),
        secondaryContainer = Color(0xFFE8DEF8),
        onSecondaryContainer = Color(0xFF1D192B),
        tertiary = Color(0xFF7D5260),
        onTertiary = Color(0xFFFFFFFF),
        tertiaryContainer = Color(0xFFFFD8E4),
        onTertiaryContainer = Color(0xFF31111D),
        error = Color(0xFFBA1A1A),
        errorContainer = Color(0xFFFFDAD6),
        onError = Color(0xFFFFFFFF),
        onErrorContainer = Color(0xFF410002),
        background = Color(0xFFFFFBFE),
        onBackground = Color(0xFF1C1B1F),
        surface = Color(0xFFFFFBFE),
        onSurface = Color(0xFF1C1B1F),
        surfaceVariant = Color(0xFFE7E0EC),
        onSurfaceVariant = Color(0xFF49454F),
        outline = Color(0xFF79747E),
        inverseOnSurface = Color(0xFFF4EFF4),
        inverseSurface = Color(0xFF313033),
        inversePrimary = Color(0xFFD0BCFF),
        surfaceTint = Color(0xFF6750A4),
        outlineVariant = Color(0xFFCAC4D0),
        scrim = Color(0xFF000000)
    )
    
    MaterialTheme(colorScheme = lightColors) {
        ColorShowcaseScreen()
    }
}

@Composable
fun ColorShowcaseScreen() {
    LazyColumn(
        contentPadding = PaddingValues(16.dp),
        verticalArrangement = Arrangement.spacedBy(12.dp)
    ) {
        item {
            Text(
                "Colores del Theme",
                style = MaterialTheme.typography.headlineMedium
            )
        }
        
        // Primary colors
        item {
            ColorCard(
                title = "Primary",
                backgroundColor = MaterialTheme.colorScheme.primary,
                contentColor = MaterialTheme.colorScheme.onPrimary
            )
        }
        
        item {
            ColorCard(
                title = "Primary Container",
                backgroundColor = MaterialTheme.colorScheme.primaryContainer,
                contentColor = MaterialTheme.colorScheme.onPrimaryContainer
            )
        }
        
        // Secondary colors
        item {
            ColorCard(
                title = "Secondary",
                backgroundColor = MaterialTheme.colorScheme.secondary,
                contentColor = MaterialTheme.colorScheme.onSecondary
            )
        }
        
        // Surface colors
        item {
            ColorCard(
                title = "Surface",
                backgroundColor = MaterialTheme.colorScheme.surface,
                contentColor = MaterialTheme.colorScheme.onSurface,
                showBorder = true
            )
        }
        
        // Error colors
        item {
            ColorCard(
                title = "Error",
                backgroundColor = MaterialTheme.colorScheme.error,
                contentColor = MaterialTheme.colorScheme.onError
            )
        }
    }
}

@Composable
fun ColorCard(
    title: String,
    backgroundColor: Color,
    contentColor: Color,
    showBorder: Boolean = false
) {
    Card(
        modifier = Modifier.fillMaxWidth(),
        colors = CardDefaults.cardColors(containerColor = backgroundColor),
        border = if (showBorder) BorderStroke(1.dp, MaterialTheme.colorScheme.outline) else null
    ) {
        Column(
            modifier = Modifier.padding(16.dp)
        ) {
            Text(
                text = title,
                color = contentColor,
                style = MaterialTheme.typography.titleMedium,
                fontWeight = FontWeight.Bold
            )
            Text(
                text = "Color: ${backgroundColor.toArgb().toString(16)}",
                color = contentColor.copy(alpha = 0.7f),
                style = MaterialTheme.typography.bodySmall
            )
        }
    }
}
```

### Tema oscuro y cambio dinámico

```kotlin
@Composable
fun DynamicThemeApp() {
    var isDarkTheme by remember { mutableStateOf(false) }
    
    val lightColors = lightColorScheme(
        primary = Color(0xFF6750A4),
        onPrimary = Color(0xFFFFFFFF),
        primaryContainer = Color(0xFFEADDFF),
        onPrimaryContainer = Color(0xFF21005D),
        background = Color(0xFFFFFBFE),
        onBackground = Color(0xFF1C1B1F),
        surface = Color(0xFFFFFBFE),
        onSurface = Color(0xFF1C1B1F)
    )
    
    val darkColors = darkColorScheme(
        primary = Color(0xFFD0BCFF),
        onPrimary = Color(0xFF381E72),
        primaryContainer = Color(0xFF4F378B),
        onPrimaryContainer = Color(0xFFEADDFF),
        background = Color(0xFF1C1B1F),
        onBackground = Color(0xFFE6E1E5),
        surface = Color(0xFF1C1B1F),
        onSurface = Color(0xFFE6E1E5)
    )
    
    MaterialTheme(
        colorScheme = if (isDarkTheme) darkColors else lightColors
    ) {
        Column(
            modifier = Modifier
                .fillMaxSize()
                .background(MaterialTheme.colorScheme.background)
                .padding(16.dp)
        ) {
            // Toggle switch para cambiar tema
            Row(
                modifier = Modifier.fillMaxWidth(),
                horizontalArrangement = Arrangement.SpaceBetween,
                verticalAlignment = Alignment.CenterVertically
            ) {
                Text(
                    "Tema oscuro",
                    color = MaterialTheme.colorScheme.onBackground
                )
                Switch(
                    checked = isDarkTheme,
                    onCheckedChange = { isDarkTheme = it }
                )
            }
            
            Spacer(modifier = Modifier.height(24.dp))
            
            // Contenido que responde al tema
            ThemeResponsiveContent()
        }
    }
}

@Composable
fun ThemeResponsiveContent() {
    LazyColumn(
        verticalArrangement = Arrangement.spacedBy(16.dp)
    ) {
        item {
            Card(
                modifier = Modifier.fillMaxWidth(),
                colors = CardDefaults.cardColors(
                    containerColor = MaterialTheme.colorScheme.primaryContainer,
                    contentColor = MaterialTheme.colorScheme.onPrimaryContainer
                )
            ) {
                Column(modifier = Modifier.padding(16.dp)) {
                    Text(
                        "Tarjeta Principal",
                        style = MaterialTheme.typography.titleLarge
                    )
                    Text(
                        "Esta tarjeta usa colores del contenedor principal",
                        style = MaterialTheme.typography.bodyMedium
                    )
                }
            }
        }
        
        item {
            Button(
                onClick = { },
                modifier = Modifier.fillMaxWidth()
            ) {
                Text("Botón con colores del tema")
            }
        }
        
        item {
            OutlinedButton(
                onClick = { },
                modifier = Modifier.fillMaxWidth()
            ) {
                Text("Botón outlined")
            }
        }
        
        item {
            Card(
                modifier = Modifier.fillMaxWidth()
            ) {
                Column(modifier = Modifier.padding(16.dp)) {
                    Text(
                        "Tarjeta de Surface",
                        style = MaterialTheme.typography.titleMedium,
                        color = MaterialTheme.colorScheme.onSurface
                    )
                    Text(
                        "Usa los colores de surface del tema actual",
                        style = MaterialTheme.typography.bodyMedium,
                        color = MaterialTheme.colorScheme.onSurfaceVariant
                    )
                }
            }
        }
    }
}
```

## 2. Tipografía personalizada

```kotlin
// Definir familia de fuentes personalizada
val robotoFontFamily = FontFamily(
    Font(R.font.roboto_light, FontWeight.Light),
    Font(R.font.roboto_regular, FontWeight.Normal),
    Font(R.font.roboto_medium, FontWeight.Medium),
    Font(R.font.roboto_bold, FontWeight.Bold)
)

// Crear tipografía personalizada
val CustomTypography = Typography(
    displayLarge = TextStyle(
        fontFamily = robotoFontFamily,
        fontWeight = FontWeight.Normal,
        fontSize = 57.sp,
        lineHeight = 64.sp,
        letterSpacing = (-0.25).sp
    ),
    displayMedium = TextStyle(
        fontFamily = robotoFontFamily,
        fontWeight = FontWeight.Normal,
        fontSize = 45.sp,
        lineHeight = 52.sp,
        letterSpacing = 0.sp
    ),
    displaySmall = TextStyle(
        fontFamily = robotoFontFamily,
        fontWeight = FontWeight.Normal,
        fontSize = 36.sp,
        lineHeight = 44.sp,
        letterSpacing = 0.sp
    ),
    headlineLarge = TextStyle(
        fontFamily = robotoFontFamily,
        fontWeight = FontWeight.Normal,
        fontSize = 32.sp,
        lineHeight = 40.sp,
        letterSpacing = 0.sp
    ),
    headlineMedium = TextStyle(
        fontFamily = robotoFontFamily,
        fontWeight = FontWeight.Normal,
        fontSize = 28.sp,
        lineHeight = 36.sp,
        letterSpacing = 0.sp
    ),
    headlineSmall = TextStyle(
        fontFamily = robotoFontFamily,
        fontWeight = FontWeight.Normal,
        fontSize = 24.sp,
        lineHeight = 32.sp,
        letterSpacing = 0.sp
    ),
    titleLarge = TextStyle(
        fontFamily = robotoFontFamily,
        fontWeight = FontWeight.Medium,
        fontSize = 22.sp,
        lineHeight = 28.sp,
        letterSpacing = 0.sp
    ),
    titleMedium = TextStyle(
        fontFamily = robotoFontFamily,
        fontWeight = FontWeight.Medium,
        fontSize = 16.sp,
        lineHeight = 24.sp,
        letterSpacing = 0.1.sp
    ),
    titleSmall = TextStyle(
        fontFamily = robotoFontFamily,
        fontWeight = FontWeight.Medium,
        fontSize = 14.sp,
        lineHeight = 20.sp,
        letterSpacing = 0.1.sp
    ),
    bodyLarge = TextStyle(
        fontFamily = robotoFontFamily,
        fontWeight = FontWeight.Normal,
        fontSize = 16.sp,
        lineHeight = 24.sp,
        letterSpacing = 0.5.sp
    ),
    bodyMedium = TextStyle(
        fontFamily = robotoFontFamily,
        fontWeight = FontWeight.Normal,
        fontSize = 14.sp,
        lineHeight = 20.sp,
        letterSpacing = 0.25.sp
    ),
    bodySmall = TextStyle(
        fontFamily = robotoFontFamily,
        fontWeight = FontWeight.Normal,
        fontSize = 12.sp,
        lineHeight = 16.sp,
        letterSpacing = 0.4.sp
    ),
    labelLarge = TextStyle(
        fontFamily = robotoFontFamily,
        fontWeight = FontWeight.Medium,
        fontSize = 14.sp,
        lineHeight = 20.sp,
        letterSpacing = 0.1.sp
    ),
    labelMedium = TextStyle(
        fontFamily = robotoFontFamily,
        fontWeight = FontWeight.Medium,
        fontSize = 12.sp,
        lineHeight = 16.sp,
        letterSpacing = 0.5.sp
    ),
    labelSmall = TextStyle(
        fontFamily = robotoFontFamily,
        fontWeight = FontWeight.Medium,
        fontSize = 11.sp,
        lineHeight = 16.sp,
        letterSpacing = 0.5.sp
    )
)

@Composable
fun CustomTypographyExample() {
    MaterialTheme(
        typography = CustomTypography
    ) {
        TypographyShowcase()
    }
}

@Composable
fun TypographyShowcase() {
    LazyColumn(
        modifier = Modifier
            .fillMaxSize()
            .background(MaterialTheme.colorScheme.background)
            .padding(16.dp),
        verticalArrangement = Arrangement.spacedBy(16.dp)
    ) {
        item {
            Text(
                "Display Large",
                style = MaterialTheme.typography.displayLarge,
                color = MaterialTheme.colorScheme.onBackground
            )
        }
        
        item {
            Text(
                "Headline Medium",
                style = MaterialTheme.typography.headlineMedium,
                color = MaterialTheme.colorScheme.onBackground
            )
        }
        
        item {
            Text(
                "Title Large",
                style = MaterialTheme.typography.titleLarge,
                color = MaterialTheme.colorScheme.onBackground
            )
        }
        
        item {
            Text(
                "Body Large - Este es el texto principal de la aplicación. Se usa para párrafos largos y contenido principal.",
                style = MaterialTheme.typography.bodyLarge,
                color = MaterialTheme.colorScheme.onBackground
            )
        }
        
        item {
            Text(
                "Body Medium - Texto secundario utilizado para descripciones y contenido de apoyo.",
                style = MaterialTheme.typography.bodyMedium,
                color = MaterialTheme.colorScheme.onSurfaceVariant
            )
        }
        
        item {
            Text(
                "Label Small",
                style = MaterialTheme.typography.labelSmall,
                color = MaterialTheme.colorScheme.onSurfaceVariant
            )
        }
    }
}
```

## 3. Formas personalizadas (Shapes)

```kotlin
val CustomShapes = Shapes(
    extraSmall = RoundedCornerShape(4.dp),
    small = RoundedCornerShape(8.dp),
    medium = RoundedCornerShape(12.dp),
    large = RoundedCornerShape(16.dp),
    extraLarge = RoundedCornerShape(24.dp)
)

// Formas más creativas
val CreativeShapes = Shapes(
    extraSmall = CutCornerShape(4.dp),
    small = RoundedCornerShape(topStart = 8.dp, bottomEnd = 8.dp),
    medium = RoundedCornerShape(
        topStart = 16.dp,
        topEnd = 16.dp,
        bottomStart = 4.dp,
        bottomEnd = 4.dp
    ),
    large = RoundedCornerShape(24.dp),
    extraLarge = CircleShape
)

@Composable
fun CustomShapesExample() {
    var useCreativeShapes by remember { mutableStateOf(false) }
    
    MaterialTheme(
        shapes = if (useCreativeShapes) CreativeShapes else CustomShapes
    ) {
        Column(
            modifier = Modifier
                .fillMaxSize()
                .background(MaterialTheme.colorScheme.background)
                .padding(16.dp),
            verticalArrangement = Arrangement.spacedBy(16.dp)
        ) {
            Row(
                modifier = Modifier.fillMaxWidth(),
                horizontalArrangement = Arrangement.SpaceBetween,
                verticalAlignment = Alignment.CenterVertically
            ) {
                Text(
                    "Formas creativas",
                    color = MaterialTheme.colorScheme.onBackground
                )
                Switch(
                    checked = useCreativeShapes,
                    onCheckedChange = { useCreativeShapes = it }
                )
            }
            
            ShapeShowcase()
        }
    }
}

@Composable
fun ShapeShowcase() {
    LazyColumn(
        verticalArrangement = Arrangement.spacedBy(12.dp)
    ) {
        item {
            Text(
                "Formas del tema",
                style = MaterialTheme.typography.headlineSmall,
                color = MaterialTheme.colorScheme.onBackground
            )
        }
        
        // Extra Small Shape
        item {
            Surface(
                modifier = Modifier
                    .fillMaxWidth()
                    .height(60.dp),
                shape = MaterialTheme.shapes.extraSmall,
                color = MaterialTheme.colorScheme.primaryContainer,
                contentColor = MaterialTheme.colorScheme.onPrimaryContainer
            ) {
                Box(
                    modifier = Modifier.fillMaxSize(),
                    contentAlignment = Alignment.Center
                ) {
                    Text("Extra Small Shape")
                }
            }
        }
        
        // Small Shape
        item {
            Surface(
                modifier = Modifier
                    .fillMaxWidth()
                    .height(60.dp),
                shape = MaterialTheme.shapes.small,
                color = MaterialTheme.colorScheme.secondaryContainer,
                contentColor = MaterialTheme.colorScheme.onSecondaryContainer
            ) {
                Box(
                    modifier = Modifier.fillMaxSize(),
                    contentAlignment = Alignment.Center
                ) {
                    Text("Small Shape")
                }
            }
        }
        
        // Medium Shape
        item {
            Surface(
                modifier = Modifier
                    .fillMaxWidth()
                    .height(60.dp),
                shape = MaterialTheme.shapes.medium,
                color = MaterialTheme.colorScheme.tertiaryContainer,
                contentColor = MaterialTheme.colorScheme.onTertiaryContainer
            ) {
                Box(
                    modifier = Modifier.fillMaxSize(),
                    contentAlignment = Alignment.Center
                ) {
                    Text("Medium Shape")
                }
            }
        }
        
        // Large Shape
        item {
            Surface(
                modifier = Modifier
                    .fillMaxWidth()
                    .height(60.dp),
                shape = MaterialTheme.shapes.large,
                color = MaterialTheme.colorScheme.surface,
                contentColor = MaterialTheme.colorScheme.onSurface,
                shadowElevation = 4.dp
            ) {
                Box(
                    modifier = Modifier.fillMaxSize(),
                    contentAlignment = Alignment.Center
                ) {
                    Text("Large Shape")
                }
            }
        }
        
        // Extra Large Shape
        item {
            Surface(
                modifier = Modifier
                    .size(100.dp)
                    .align(Alignment.CenterHorizontally),
                shape = MaterialTheme.shapes.extraLarge,
                color = MaterialTheme.colorScheme.primary,
                contentColor = MaterialTheme.colorScheme.onPrimary
            ) {
                Box(
                    modifier = Modifier.fillMaxSize(),
                    contentAlignment = Alignment.Center
                ) {
                    Text("XL")
                }
            }
        }
    }
}
```

## 4. Tema completo personalizado

```kotlin
// Colores de la marca
object BrandColors {
    val Purple = Color(0xFF7B2CBF)
    val PurpleLight = Color(0xFF9D4EDD)
    val PurpleDark = Color(0xFF5A189A)
    val Orange = Color(0xFFFF6B35)
    val OrangeLight = Color(0xFFFF8E53)
    val Gray = Color(0xFF6C757D)
    val GrayLight = Color(0xFFF8F9FA)
    val GrayDark = Color(0xFF343A40)
    val White = Color(0xFFFFFFFF)
    val Black = Color(0xFF000000)
}

// Esquemas de color personalizados
val CustomLightColorScheme = lightColorScheme(
    primary = BrandColors.Purple,
    onPrimary = BrandColors.White,
    primaryContainer = BrandColors.PurpleLight.copy(alpha = 0.3f),
    onPrimaryContainer = BrandColors.PurpleDark,
    secondary = BrandColors.Orange,
    onSecondary = BrandColors.White,
    secondaryContainer = BrandColors.OrangeLight.copy(alpha = 0.3f),
    onSecondaryContainer = BrandColors.Orange.copy(alpha = 0.8f),
    background = BrandColors.GrayLight,
    onBackground = BrandColors.GrayDark,
    surface = BrandColors.White,
    onSurface = BrandColors.GrayDark,
    surfaceVariant = BrandColors.Gray.copy(alpha = 0.1f),
    onSurfaceVariant = BrandColors.Gray,
    outline = BrandColors.Gray.copy(alpha = 0.5f),
    error = Color(0xFFDC3545),
    onError = BrandColors.White
)

val CustomDarkColorScheme = darkColorScheme(
    primary = BrandColors.PurpleLight,
    onPrimary = BrandColors.GrayDark,
    primaryContainer = BrandColors.PurpleDark,
    onPrimaryContainer = BrandColors.PurpleLight.copy(alpha = 0.8f),
    secondary = BrandColors.OrangeLight,
    onSecondary = BrandColors.GrayDark,
    secondaryContainer = BrandColors.Orange.copy(alpha = 0.3f),
    onSecondaryContainer = BrandColors.OrangeLight,
    background = BrandColors.GrayDark,
    onBackground = BrandColors.GrayLight,
    surface = BrandColors.Black.copy(alpha = 0.9f),
    onSurface = BrandColors.GrayLight,
    surfaceVariant = BrandColors.Gray.copy(alpha = 0.3f),
    onSurfaceVariant = BrandColors.GrayLight.copy(alpha = 0.7f),
    outline = BrandColors.Gray,
    error = Color(0xFFFF6B6B),
    onError = BrandColors.White
)

// Tema completo personalizado
@Composable
fun MyCustomTheme(
    useDarkTheme: Boolean = isSystemInDarkTheme(),
    content: @Composable () -> Unit
) {
    val colorScheme = if (useDarkTheme) {
        CustomDarkColorScheme
    } else {
        CustomLightColorScheme
    }
    
    MaterialTheme(
        colorScheme = colorScheme,
        typography = CustomTypography,
        shapes = CustomShapes,
        content = content
    )
}

// Aplicación usando el tema personalizado
@Composable
fun CustomThemeApp() {
    var useDarkTheme by remember { mutableStateOf(false) }
    
    MyCustomTheme(useDarkTheme = useDarkTheme) {
        Scaffold(
            topBar = {
                TopAppBar(
                    title = { Text("Mi App Personalizada") },
                    actions = {
                        IconButton(
                            onClick = { useDarkTheme = !useDarkTheme }
                        ) {
                            Icon(
                                imageVector = if (useDarkTheme) Icons.Default.LightMode else Icons.Default.DarkMode,
                                contentDescription = "Cambiar tema"
                            )
                        }
                    }
                )
            },
            floatingActionButton = {
                FloatingActionButton(
                    onClick = { }
                ) {
                    Icon(Icons.Default.Add, contentDescription = "Agregar")
                }
            }
        ) { paddingValues ->
            CustomThemeContent(
                modifier = Modifier.padding(paddingValues)
            )
        }
    }
}

@Composable
fun CustomThemeContent(modifier: Modifier = Modifier) {
    LazyColumn(
        modifier = modifier
            .fillMaxSize()
            .padding(16.dp),
        verticalArrangement = Arrangement.spacedBy(16.dp)
    ) {
        item {
            Text(
                "Bienvenido a mi app",
                style = MaterialTheme.typography.headlineMedium,
                color = MaterialTheme.colorScheme.onBackground
            )
        }
        
        item {
            Card(
                modifier = Modifier.fillMaxWidth(),
                colors = CardDefaults.cardColors(
                    containerColor = MaterialTheme.colorScheme.primaryContainer,
                    contentColor = MaterialTheme.colorScheme.onPrimaryContainer
                )
            ) {
                Column(
                    modifier = Modifier.padding(16.dp)
                ) {
                    Text(
                        "Tarjeta destacada",
                        style = MaterialTheme.typography.titleLarge
                    )
                    Spacer(modifier = Modifier.height(8.dp))
                    Text(
                        "Esta tarjeta usa los colores del contenedor principal del tema personalizado.",
                        style = MaterialTheme.typography.bodyMedium
                    )
                }
            }
        }
        
        item {
            Row(
                modifier = Modifier.fillMaxWidth(),
                horizontalArrangement = Arrangement.spacedBy(12.dp)
            ) {
                Button(
                    onClick = { },
                    modifier = Modifier.weight(1f)
                ) {
                    Text("Primario")
                }
                
                OutlinedButton(
                    onClick = { },
                    modifier = Modifier.weight(1f)
                ) {
                    Text("Secundario")
                }
            }
        }
        
        item {
            Card(
                modifier = Modifier.fillMaxWidth()
            ) {
                Column(
                    modifier = Modifier.padding(16.dp)
                ) {
                    Text(
                        "Información",
                        style = MaterialTheme.typography.titleMedium,
                        color = MaterialTheme.colorScheme.onSurface
                    )
                    Spacer(modifier = Modifier.height(8.dp))
                    Text(
                        "Esta es una tarjeta regular que usa los colores de surface del tema.",
                        style = MaterialTheme.typography.bodyMedium,
                        color = MaterialTheme.colorScheme.onSurfaceVariant
                    )
                }
            }
        }
    }
}
```

## 5. Material You y colores dinámicos

```kotlin
@Composable
fun DynamicColorTheme(
    useDarkTheme: Boolean = isSystemInDarkTheme(),
    content: @Composable () -> Unit
) {
    val context = LocalContext.current
    
    val dynamicColor = Build.VERSION.SDK_INT >= Build.VERSION_CODES.S
    
    val colorScheme = when {
        dynamicColor && useDarkTheme -> {
            dynamicDarkColorScheme(context)
        }
        dynamicColor && !useDarkTheme -> {
            dynamicLightColorScheme(context)
        }
        useDarkTheme -> CustomDarkColorScheme
        else -> CustomLightColorScheme
    }
    
    MaterialTheme(
        colorScheme = colorScheme,
        typography = CustomTypography,
        shapes = CustomShapes,
        content = content
    )
}

@Composable
fun MaterialYouExample() {
    var useDarkTheme by remember { mutableStateOf(false) }
    val context = LocalContext.current
    val supportsDynamicColor = Build.VERSION.SDK_INT >= Build.VERSION_CODES.S
    
    DynamicColorTheme(useDarkTheme = useDarkTheme) {
        Column(
            modifier = Modifier
                .fillMaxSize()
                .background(MaterialTheme.colorScheme.background)
                .padding(16.dp),
            verticalArrangement = Arrangement.spacedBy(16.dp)
        ) {
            Text(
                "Material You",
                style = MaterialTheme.typography.headlineMedium,
                color = MaterialTheme.colorScheme.onBackground
            )
            
            if (supportsDynamicColor) {
                Text(
                    "✅ Este dispositivo soporta colores dinámicos",
                    style = MaterialTheme.typography.bodyMedium,
                    color = MaterialTheme.colorScheme.primary
                )
            } else {
                Text(
                    "❌ Este dispositivo no soporta colores dinámicos (Android 12+)",
                    style = MaterialTheme.typography.bodyMedium,
                    color = MaterialTheme.colorScheme.error
                )
            }
            
            Row(
                modifier = Modifier.fillMaxWidth(),
                horizontalArrangement = Arrangement.SpaceBetween,
                verticalAlignment = Alignment.CenterVertically
            ) {
                Text("Tema oscuro")
                Switch(
                    checked = useDarkTheme,
                    onCheckedChange = { useDarkTheme = it }
                )
            }
            
            // Muestra de colores dinámicos
            DynamicColorShowcase()
        }
    }
}

@Composable
fun DynamicColorShowcase() {
    LazyColumn(
        verticalArrangement = Arrangement.spacedBy(8.dp)
    ) {
        val colors = listOf(
            "Primary" to MaterialTheme.colorScheme.primary,
            "Secondary" to MaterialTheme.colorScheme.secondary,
            "Tertiary" to MaterialTheme.colorScheme.tertiary,
            "Surface" to MaterialTheme.colorScheme.surface,
            "Primary Container" to MaterialTheme.colorScheme.primaryContainer,
            "Secondary Container" to MaterialTheme.colorScheme.secondaryContainer
        )
        
        items(colors) { (name, color) ->
            Row(
                modifier = Modifier.fillMaxWidth(),
                verticalAlignment = Alignment.CenterVertically
            ) {
                Box(
                    modifier = Modifier
                        .size(40.dp)
                        .background(color, CircleShape)
                        .border(1.dp, MaterialTheme.colorScheme.outline, CircleShape)
                )
                Spacer(modifier = Modifier.width(16.dp))
                Text(
                    name,
                    color = MaterialTheme.colorScheme.onBackground
                )
            }
        }
    }
}
```

## 6. Temas con CompositionLocal personalizado

```kotlin
// Datos adicionales del tema
data class AppThemeData(
    val gradients: AppGradients,
    val dimensions: AppDimensions,
    val animations: AppAnimations
)

data class AppGradients(
    val primary: Brush,
    val secondary: Brush,
    val background: Brush
)

data class AppDimensions(
    val cardElevation: Dp,
    val buttonHeight: Dp,
    val iconSize: Dp
)

data class AppAnimations(
    val short: Int,
    val medium: Int,
    val long: Int
)

// CompositionLocal personalizado
val LocalAppTheme = compositionLocalOf<AppThemeData> {
    error("No AppTheme provided")
}

// Crear datos del tema
val LightAppThemeData = AppThemeData(
    gradients = AppGradients(
        primary = Brush.linearGradient(
            colors = listOf(BrandColors.Purple, BrandColors.PurpleLight)
        ),
        secondary = Brush.linearGradient(
            colors = listOf(BrandColors.Orange, BrandColors.OrangeLight)
        ),
        background = Brush.linearGradient(
            colors = listOf(BrandColors.GrayLight, Color.White)
        )
    ),
    dimensions = AppDimensions(
        cardElevation = 4.dp,
        buttonHeight = 48.dp,
        iconSize = 24.dp
    ),
    animations = AppAnimations(
        short = 150,
        medium = 300,
        long = 500
    )
)

val DarkAppThemeData = AppThemeData(
    gradients = AppGradients(
        primary = Brush.linearGradient(
            colors = listOf(BrandColors.PurpleDark, BrandColors.Purple)
        ),
        secondary = Brush.linearGradient(
            colors = listOf(BrandColors.Orange.copy(alpha = 0.8f), BrandColors.OrangeLight)
        ),
        background = Brush.linearGradient(
            colors = listOf(BrandColors.GrayDark, BrandColors.Black)
        )
    ),
    dimensions = AppDimensions(
        cardElevation = 8.dp,
        buttonHeight = 48.dp,
        iconSize = 24.dp
    ),
    animations = AppAnimations(
        short = 150,
        medium = 300,
        long = 500
    )
)

@Composable
fun ExtendedTheme(
    useDarkTheme: Boolean = isSystemInDarkTheme(),
    content: @Composable () -> Unit
) {
    val colorScheme = if (useDarkTheme) CustomDarkColorScheme else CustomLightColorScheme
    val appThemeData = if (useDarkTheme) DarkAppThemeData else LightAppThemeData
    
    MaterialTheme(
        colorScheme = colorScheme,
        typography = CustomTypography,
        shapes = CustomShapes
    ) {
        CompositionLocalProvider(LocalAppTheme provides appThemeData) {
            content()
        }
    }
}

// Extensiones para fácil acceso
object AppTheme {
    val gradients: AppGradients
        @Composable
        get() = LocalAppTheme.current.gradients
    
    val dimensions: AppDimensions
        @Composable
        get() = LocalAppTheme.current.dimensions
    
    val animations: AppAnimations
        @Composable
        get() = LocalAppTheme.current.animations
}

@Composable
fun ExtendedThemeExample() {
    var useDarkTheme by remember { mutableStateOf(false) }
    
    ExtendedTheme(useDarkTheme = useDarkTheme) {
        Column(
            modifier = Modifier
                .fillMaxSize()
                .background(AppTheme.gradients.background)
                .padding(16.dp),
            verticalArrangement = Arrangement.spacedBy(16.dp)
        ) {
            Row(
                modifier = Modifier.fillMaxWidth(),
                horizontalArrangement = Arrangement.SpaceBetween,
                verticalAlignment = Alignment.CenterVertically
            ) {
                Text(
                    "Tema extendido",
                    color = MaterialTheme.colorScheme.onBackground
                )
                Switch(
                    checked = useDarkTheme,
                    onCheckedChange = { useDarkTheme = it }
                )
            }
            
            // Card con gradiente personalizado
            Card(
                modifier = Modifier.fillMaxWidth(),
                elevation = CardDefaults.cardElevation(
                    defaultElevation = AppTheme.dimensions.cardElevation
                )
            ) {
                Box(
                    modifier = Modifier
                        .fillMaxWidth()
                        .height(120.dp)
                        .background(AppTheme.gradients.primary),
                    contentAlignment = Alignment.Center
                ) {
                    Text(
                        "Gradiente primario",
                        color = Color.White,
                        style = MaterialTheme.typography.titleLarge
                    )
                }
            }
            
            // Botón con altura personalizada
            Button(
                onClick = { },
                modifier = Modifier
                    .fillMaxWidth()
                    .height(AppTheme.dimensions.buttonHeight)
            ) {
                Icon(
                    Icons.Default.Star,
                    contentDescription = null,
                    modifier = Modifier.size(AppTheme.dimensions.iconSize)
                )
                Spacer(modifier = Modifier.width(8.dp))
                Text("Botón personalizado")
            }
            
            // Card con gradiente secundario
            Card(
                modifier = Modifier.fillMaxWidth(),
                elevation = CardDefaults.cardElevation(
                    defaultElevation = AppTheme.dimensions.cardElevation
                )
            ) {
                Box(
                    modifier = Modifier
                        .fillMaxWidth()
                        .height(80.dp)
                        .background(AppTheme.gradients.secondary),
                    contentAlignment = Alignment.Center
                ) {
                    Text(
                        "Gradiente secundario",
                        color = Color.White,
                        style = MaterialTheme.typography.titleMedium
                    )
                }
            }
        }
    }
}
```

## 7. Mejores prácticas para temas

### Estructura de archivos recomendada

```kotlin
// ui/theme/Color.kt
object AppColors {
    // Colores base
    val Purple200 = Color(0xFFBB86FC)
    val Purple500 = Color(0xFF6200EE)
    // ... más colores
}

// ui/theme/Type.kt
val Typography = Typography(
    // Definiciones de tipografía
)

// ui/theme/Shape.kt
val Shapes = Shapes(
    // Definiciones de formas
)

// ui/theme/Theme.kt
@Composable
fun MyAppTheme(
    darkTheme: Boolean = isSystemInDarkTheme(),
    content: @Composable () -> Unit
) {
    // Implementación del tema
}
```

### Tema adaptativo para diferentes tamaños

```kotlin
@Composable
fun AdaptiveTheme(
    content: @Composable () -> Unit
) {
    val configuration = LocalConfiguration.current
    val isLargeScreen = configuration.screenWidthDp >= 600
    
    val adaptiveTypography = if (isLargeScreen) {
        Typography(
            headlineLarge = MaterialTheme.typography.headlineLarge.copy(fontSize = 40.sp),
            bodyLarge = MaterialTheme.typography.bodyLarge.copy(fontSize = 18.sp)
            // Texto más grande en pantallas grandes
        )
    } else {
        Typography() // Tipografía estándar para móviles
    }
    
    val adaptiveShapes = if (isLargeScreen) {
        Shapes(
            medium = RoundedCornerShape(16.dp), // Esquinas más redondeadas
            large = RoundedCornerShape(24.dp)
        )
    } else {
        Shapes(
            medium = RoundedCornerShape(8.dp),
            large = RoundedCornerShape(12.dp)
        )
    }
    
    MaterialTheme(
        colorScheme = if (isSystemInDarkTheme()) CustomDarkColorScheme else CustomLightColorScheme,
        typography = adaptiveTypography,
        shapes = adaptiveShapes,
        content = content
    )
}
```

### Sistema de tokens de diseño

```kotlin
// Design tokens
object DesignTokens {
    // Colores semánticos
    object Colors {
        val success = Color(0xFF4CAF50)
        val warning = Color(0xFFFF9800)
        val info = Color(0xFF2196F3)
        val danger = Color(0xFFf44336)
    }
    
    // Espaciado
    object Spacing {
        val none = 0.dp
        val xs = 4.dp
        val sm = 8.dp
        val md = 16.dp
        val lg = 24.dp
        val xl = 32.dp
        val xxl = 48.dp
    }
    
    // Elevaciones
    object Elevation {
        val none = 0.dp
        val sm = 2.dp
        val md = 4.dp
        val lg = 8.dp
        val xl = 12.dp
    }
}

// Componentes reutilizables usando tokens
@Composable
fun SuccessCard(
    title: String,
    description: String,
    modifier: Modifier = Modifier
) {
    Card(
        modifier = modifier,
        colors = CardDefaults.cardColors(
            containerColor = DesignTokens.Colors.success.copy(alpha = 0.1f),
            contentColor = DesignTokens.Colors.success
        ),
        elevation = CardDefaults.cardElevation(defaultElevation = DesignTokens.Elevation.sm),
        shape = MaterialTheme.shapes.medium
    ) {
        Column(
            modifier = Modifier.padding(DesignTokens.Spacing.md)
        ) {
            Row(
                verticalAlignment = Alignment.CenterVertically
            ) {
                Icon(
                    Icons.Default.CheckCircle,
                    contentDescription = null,
                    tint = DesignTokens.Colors.success
                )
                Spacer(modifier = Modifier.width(DesignTokens.Spacing.sm))
                Text(
                    title,
                    style = MaterialTheme.typography.titleMedium,
                    color = DesignTokens.Colors.success
                )
            }
            Spacer(modifier = Modifier.height(DesignTokens.Spacing.sm))
            Text(
                description,
                style = MaterialTheme.typography.bodyMedium,
                color = MaterialTheme.colorScheme.onSurface
            )
        }
    }
}
```

## Resumen de mejores prácticas

### ✅ Hacer

1. **Usar MaterialTheme** como base para consistencia
2. **Definir colores semánticos** (primary, secondary, error, etc.)
3. **Crear constantes reutilizables** para colores, espaciado y tipografía
4. **Soportar tema claro y oscuro** siempre
5. **Usar sp para texto** y dp para elementos UI
6. **Seguir las guías de Material Design** como punto de partida
7. **Probar en diferentes densidades** de pantalla
8. **Considerar accesibilidad** (contraste, tamaños mínimos)

### ❌ Evitar

1. **No hardcodear colores** directamente en componentes
2. **No ignorar el tema del sistema** (claro/oscuro)
3. **No crear demasiadas variaciones** sin propósito
4. **No mezclar diferentes sistemas** de diseño inconsistentemente
5. **No olvidar testear** en dispositivos reales
6. **No ignorar Material You** en Android 12+

### Checklist de implementación

- [ ] Colores definidos semánticamente
- [ ] Soporte para tema claro y oscuro
- [ ] Tipografía consistente en toda la app
- [ ] Formas coherentes con la identidad visual
- [ ] Tokens de diseño documentados
- [ ] CompositionLocal para extensiones si es necesario
- [ ] Testeo en diferentes dispositivos y densidades
- [ ] Consideraciones de accesibilidad aplicadas
- [ ] Soporte para Material You (Android 12+)

Los temas en Compose son poderosos y flexibles. Con una implementación cuidadosa, puedes crear una experiencia visual coherente y atractiva que se adapte a las preferencias del usuario y funcione bien en todos los dispositivos Android.