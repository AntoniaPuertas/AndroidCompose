# Componentes Comunes de Jetpack Compose - Referencia Rápida

Esta es una guía de referencia rápida de los componentes más utilizados en Jetpack Compose, organizados por categorías.

## 📝 Componentes de Texto e Imágenes

### `Text`
Muestra texto en la interfaz.
```kotlin
Text(
    text = "Hola Mundo",
    style = MaterialTheme.typography.headlineMedium,
    color = Color.Blue
)
```
**Cuándo usar:** Para mostrar cualquier texto - títulos, párrafos, etiquetas, etc.

### `Image`
Muestra imágenes desde recursos o URLs.
```kotlin
Image(
    painter = painterResource(R.drawable.mi_imagen),
    contentDescription = "Descripción",
    modifier = Modifier.size(100.dp)
)
```
**Cuándo usar:** Para mostrar imágenes estáticas, iconos grandes, fotos.

### `Icon`
Muestra iconos pequeños, optimizado para iconografía.
```kotlin
Icon(
    imageVector = Icons.Default.Favorite,
    contentDescription = "Favorito",
    tint = Color.Red
)
```
**Cuándo usar:** Iconos en botones, navegación, estados, acciones.

## 🔘 Botones e Interacciones

### `Button`
Botón principal de Material Design.
```kotlin
Button(onClick = { /* acción */ }) {
    Text("Presionar")
}
```
**Cuándo usar:** Acciones principales, envío de formularios, navegación importante.

### `OutlinedButton`
Botón con borde, menos prominente que Button.
```kotlin
OutlinedButton(onClick = { /* acción */ }) {
    Text("Cancelar")
}
```
**Cuándo usar:** Acciones secundarias, cancelar, opciones alternativas.

### `TextButton`
Botón de solo texto, mínima prominencia.
```kotlin
TextButton(onClick = { /* acción */ }) {
    Text("Más información")
}
```
**Cuándo usar:** Enlaces, acciones terciarias, navegación sutil.

### `IconButton`
Botón circular para iconos.
```kotlin
IconButton(onClick = { /* acción */ }) {
    Icon(Icons.Default.Settings, contentDescription = "Configuración")
}
```
**Cuándo usar:** Acciones rápidas con iconos, toolbars, navegación.

### `FloatingActionButton`
Botón flotante para la acción principal de la pantalla.
```kotlin
FloatingActionButton(onClick = { /* acción */ }) {
    Icon(Icons.Default.Add, contentDescription = "Agregar")
}
```
**Cuándo usar:** Acción principal y más común de la pantalla (agregar, crear, etc.).

### `Switch`
Interruptor para estados on/off.
```kotlin
var checked by remember { mutableStateOf(false) }
Switch(
    checked = checked,
    onCheckedChange = { checked = it }
)
```
**Cuándo usar:** Configuraciones booleanas, activar/desactivar funciones.

### `Checkbox`
Casilla de verificación para selecciones múltiples.
```kotlin
var checked by remember { mutableStateOf(false) }
Checkbox(
    checked = checked,
    onCheckedChange = { checked = it }
)
```
**Cuándo usar:** Listas donde puedes seleccionar múltiples elementos.

### `RadioButton`
Botón de radio para selecciones exclusivas.
```kotlin
var selected by remember { mutableStateOf("opcion1") }
RadioButton(
    selected = selected == "opcion1",
    onClick = { selected = "opcion1" }
)
```
**Cuándo usar:** Grupos donde solo puedes seleccionar una opción.

## 📋 Campos de Input y Formularios

### `TextField`
Campo de texto básico para entrada de usuario.
```kotlin
var text by remember { mutableStateOf("") }
TextField(
    value = text,
    onValueChange = { text = it },
    label = { Text("Nombre") }
)
```
**Cuándo usar:** Formularios, búsquedas, entrada de datos.

### `OutlinedTextField`
Campo de texto con borde, estilo más limpio.
```kotlin
var text by remember { mutableStateOf("") }
OutlinedTextField(
    value = text,
    onValueChange = { text = it },
    label = { Text("Email") }
)
```
**Cuándo usar:** Formularios formales, cuando prefieres el diseño con borde.

### `Slider`
Control deslizante para seleccionar valores en un rango.
```kotlin
var sliderValue by remember { mutableStateOf(0.5f) }
Slider(
    value = sliderValue,
    onValueChange = { sliderValue = it },
    valueRange = 0f..1f
)
```
**Cuándo usar:** Volumen, brillo, progreso, cualquier valor en rango continuo.

## 📐 Layouts y Contenedores

### `Column`
Organiza elementos verticalmente.
```kotlin
Column {
    Text("Elemento 1")
    Text("Elemento 2")
    Text("Elemento 3")
}
```
**Cuándo usar:** Formularios, listas simples, elementos apilados verticalmente.

### `Row`
Organiza elementos horizontalmente.
```kotlin
Row {
    Text("Izquierda")
    Spacer(modifier = Modifier.weight(1f))
    Text("Derecha")
}
```
**Cuándo usar:** Barras de herramientas, elementos en línea, headers.

### `Box`
Superpone elementos unos encima de otros.
```kotlin
Box {
    Image(painter = painterResource(R.drawable.fondo), contentDescription = null)
    Text("Texto superpuesto", modifier = Modifier.align(Alignment.Center))
}
```
**Cuándo usar:** Overlays, badges, texto sobre imágenes.

### `LazyColumn`
Lista vertical eficiente para muchos elementos.
```kotlin
LazyColumn {
    items(listaElementos) { elemento ->
        Text(elemento)
    }
}
```
**Cuándo usar:** Listas largas, feeds, cualquier lista con scroll vertical.

### `LazyRow`
Lista horizontal eficiente para muchos elementos.
```kotlin
LazyRow {
    items(listaElementos) { elemento ->
        Card { Text(elemento) }
    }
}
```
**Cuándo usar:** Carruseles, chips de categorías, navegación horizontal.

### `Scaffold`
Estructura básica de pantalla con Material Design.
```kotlin
Scaffold(
    topBar = { TopAppBar(title = { Text("Mi App") }) },
    floatingActionButton = { FloatingActionButton(onClick = {}) { Icon(Icons.Default.Add, null) } }
) { paddingValues ->
    // Contenido principal
}
```
**Cuándo usar:** Como contenedor principal de la mayoría de pantallas.

### `Card`
Contenedor elevado siguiendo Material Design.
```kotlin
Card(
    modifier = Modifier.padding(8.dp),
    elevation = CardDefaults.cardElevation(defaultElevation = 4.dp)
) {
    Text("Contenido de la tarjeta", modifier = Modifier.padding(16.dp))
}
```
**Cuándo usar:** Agrupar información relacionada, elementos de lista, contenido destacado.

### `Surface`
Contenedor base con color de fondo y elevación.
```kotlin
Surface(
    color = MaterialTheme.colorScheme.primary,
    contentColor = MaterialTheme.colorScheme.onPrimary
) {
    Text("Texto en superficie", modifier = Modifier.padding(16.dp))
}
```
**Cuándo usar:** Fondos personalizados, crear componentes custom, contenedores temáticos.

## 🎨 Componentes de Material Design

### `TopAppBar`
Barra superior de la aplicación.
```kotlin
TopAppBar(
    title = { Text("Mi Aplicación") },
    navigationIcon = {
        IconButton(onClick = {}) {
            Icon(Icons.Default.Menu, contentDescription = "Menú")
        }
    },
    actions = {
        IconButton(onClick = {}) {
            Icon(Icons.Default.Search, contentDescription = "Buscar")
        }
    }
)
```
**Cuándo usar:** Como header de pantallas, navegación principal, acciones globales.

### `BottomAppBar`
Barra inferior de la aplicación.
```kotlin
BottomAppBar {
    IconButton(onClick = {}) {
        Icon(Icons.Default.Home, contentDescription = "Inicio")
    }
    // Más iconos...
}
```
**Cuándo usar:** Navegación principal, acciones frecuentes desde cualquier pantalla.

### `NavigationBar`
Barra de navegación inferior con tabs.
```kotlin
NavigationBar {
    NavigationBarItem(
        selected = selectedTab == 0,
        onClick = { selectedTab = 0 },
        icon = { Icon(Icons.Default.Home, contentDescription = "Inicio") },
        label = { Text("Inicio") }
    )
    // Más items...
}
```
**Cuándo usar:** Navegación principal entre 3-5 secciones de la app.

### `TabRow`
Fila de pestañas para navegación horizontal.
```kotlin
TabRow(selectedTabIndex = selectedTab) {
    Tab(
        selected = selectedTab == 0,
        onClick = { selectedTab = 0 },
        text = { Text("Tab 1") }
    )
    // Más tabs...
}
```
**Cuándo usar:** Navegación entre secciones relacionadas, filtros, categorías.

### `Chip`
Elemento compacto para filtros o selecciones.
```kotlin
FilterChip(
    selected = isSelected,
    onClick = { isSelected = !isSelected },
    label = { Text("Filtro") }
)
```
**Cuándo usar:** Filtros, tags, selecciones múltiples, categorías.

### `Badge`
Indicador pequeño de notificaciones o estado.
```kotlin
BadgedBox(
    badge = { Badge { Text("3") } }
) {
    Icon(Icons.Default.Notifications, contentDescription = "Notificaciones")
}
```
**Cuándo usar:** Contar notificaciones, indicar estados, elementos nuevos.

## 🎛️ Controles de Navegación y Interacción

### `Pager`
Navegación por páginas con deslizamiento.
```kotlin
val pagerState = rememberPagerState(pageCount = { 3 })
HorizontalPager(state = pagerState) { page ->
    Text("Página $page")
}
```
**Cuándo usar:** Onboarding, galerías de imágenes, navegación por pasos.

### `PullToRefresh`
Control de "tirar para refrescar".
```kotlin
PullToRefreshBox(
    isRefreshing = isRefreshing,
    onRefresh = { /* actualizar datos */ }
) {
    // Contenido que se puede refrescar
}
```
**Cuándo usar:** Listas de contenido que se pueden actualizar, feeds, datos dinámicos.

### `SwipeToDismiss`
Permite deslizar para descartar elementos.
```kotlin
SwipeToDismissBox(
    state = dismissState,
    backgroundContent = { /* contenido de fondo al deslizar */ }
) {
    // Elemento que se puede descartar
}
```
**Cuándo usar:** Eliminar elementos de listas, acciones deslizables.

## 🔧 Componentes Auxiliares

### `Spacer`
Espacio vacío entre elementos.
```kotlin
Column {
    Text("Elemento 1")
    Spacer(modifier = Modifier.height(16.dp))
    Text("Elemento 2")
}
```
**Cuándo usar:** Crear espacios específicos entre elementos.

### `Divider`
Línea divisoria entre contenido.
```kotlin
Column {
    Text("Sección 1")
    Divider(modifier = Modifier.padding(vertical = 8.dp))
    Text("Sección 2")
}
```
**Cuándo usar:** Separar secciones visualmente, listas, grupos de contenido.

### `CircularProgressIndicator`
Indicador de carga circular.
```kotlin
CircularProgressIndicator(
    progress = { 0.75f }, // Progreso específico o sin parámetro para infinito
    modifier = Modifier.size(50.dp)
)
```
**Cuándo usar:** Operaciones de carga, progreso de tareas.

### `LinearProgressIndicator`
Indicador de carga lineal.
```kotlin
LinearProgressIndicator(
    progress = { 0.6f },
    modifier = Modifier.fillMaxWidth()
)
```
**Cuándo usar:** Barras de progreso, descarga de archivos, instalaciones.

## 🎨 Componentes Visuales Avanzados

### `Canvas`
Área de dibujo personalizada.
```kotlin
Canvas(modifier = Modifier.size(100.dp)) { drawScope ->
    drawCircle(Color.Blue, radius = 50.dp.toPx())
}
```
**Cuándo usar:** Gráficos custom, dibujos, visualizaciones de datos.

### `AnimatedVisibility`
Controla la visibilidad con animaciones.
```kotlin
AnimatedVisibility(visible = isVisible) {
    Text("Este texto aparece/desaparece con animación")
}
```
**Cuándo usar:** Mostrar/ocultar elementos suavemente, transiciones.

### `Crossfade`
Transición suave entre diferentes contenidos.
```kotlin
Crossfade(targetState = currentScreen) { screen ->
    when (screen) {
        "home" -> HomeContent()
        "profile" -> ProfileContent()
    }
}
```
**Cuándo usar:** Cambiar entre diferentes pantallas o estados con transición suave.

## 📱 Componentes Específicos de Plataforma

### `BackHandler`
Maneja el botón de "atrás" del sistema.
```kotlin
BackHandler(enabled = canGoBack) {
    // Lógica personalizada para el botón atrás
}
```
**Cuándo usar:** Navegación custom, confirmaciones antes de salir, estados específicos.

### `LaunchedEffect`
Ejecuta código de efecto lateral durante la composición.
```kotlin
LaunchedEffect(key1 = userId) {
    // Cargar datos del usuario
    userData = loadUserData(userId)
}
```
**Cuándo usar:** Llamadas a API, operaciones asíncronas, efectos que dependen de cambios.

### `DisposableEffect`
Efecto que se limpia cuando el Composable se destruye.
```kotlin
DisposableEffect(Unit) {
    // Configurar algo (ej: listener)
    onDispose {
        // Limpiar (ej: remover listener)
    }
}
```
**Cuándo usar:** Registrar/desregistrar listeners, recursos que necesitan limpieza.

## 🛠️ Consejos de Uso

### Componentes más utilizados en orden de frecuencia:
1. **Text** - En prácticamente todas las pantallas
2. **Column/Row** - Layouts básicos fundamentales
3. **Button** - Interacciones principales
4. **LazyColumn** - Listas de contenido
5. **Scaffold** - Estructura de pantallas
6. **Card** - Agrupación de contenido
7. **TextField** - Formularios e inputs
8. **Icon** - Iconografía general
9. **Image** - Contenido visual
10. **TopAppBar** - Navegación y títulos

### Principios para elegir componentes:

- **Funcionalidad primero**: ¿Qué debe hacer el componente?
- **Material Design**: Prefiere componentes que siguen las guías de Material
- **Performance**: Usa Lazy* para listas grandes
- **Accesibilidad**: Siempre incluye `contentDescription` donde corresponda
- **Consistencia**: Mantén patrones similares en toda la app

Esta referencia cubre los componentes esenciales para construir aplicaciones completas en Jetpack Compose.