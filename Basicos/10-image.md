# Componente Image en Jetpack Compose - Guía Básica

## 🖼️ ¿Qué es el componente Image?

El componente `Image` en Jetpack Compose se usa para **mostrar imágenes** en tu aplicación. Es el equivalente al `ImageView` en el sistema tradicional de Android, pero optimizado para Compose.

### Usos comunes:
- Mostrar fotos de perfil
- Iconos grandes
- Imágenes de productos
- Fondos decorativos
- Logotipos

## 📝 Sintaxis básica

```kotlin
Image(
    painter = painterResource(R.drawable.mi_imagen),
    contentDescription = "Descripción de la imagen"
)
```

### Parámetros principales:
- **`painter`**: De dónde viene la imagen (recurso, URL, etc.)
- **`contentDescription`**: Descripción para accesibilidad
- **`modifier`**: Tamaño, padding y otros estilos
- **`contentScale`**: Cómo se ajusta la imagen

## 🖼️ Cargar imágenes desde recursos

### Paso 1: Agregar imagen a res/drawable
Coloca tu imagen en la carpeta `app/src/main/res/drawable/`

### Paso 2: Usar la imagen
```kotlin
@Composable
fun ImagenBasica() {
    Image(
        painter = painterResource(R.drawable.mi_foto),
        contentDescription = "Mi foto de perfil",
        modifier = Modifier.size(100.dp)
    )
}
```

### Con tamaño específico
```kotlin
@Composable
fun ImagenConTamaño() {
    Image(
        painter = painterResource(R.drawable.logo),
        contentDescription = "Logo de la app",
        modifier = Modifier
            .width(200.dp)
            .height(100.dp)
    )
}
```

## 📐 ContentScale - Cómo se ajusta la imagen

### Crop - Recorta para llenar todo el espacio
```kotlin
Image(
    painter = painterResource(R.drawable.foto),
    contentDescription = "Foto",
    contentScale = ContentScale.Crop,
    modifier = Modifier.size(150.dp)
)
```

### Fit - Ajusta toda la imagen sin recortar
```kotlin
Image(
    painter = painterResource(R.drawable.foto),
    contentDescription = "Foto",
    contentScale = ContentScale.Fit,
    modifier = Modifier.size(150.dp)
)
```

### FillBounds - Estira la imagen para llenar el espacio
```kotlin
Image(
    painter = painterResource(R.drawable.foto),
    contentDescription = "Foto",
    contentScale = ContentScale.FillBounds,
    modifier = Modifier.size(150.dp)
)
```

## 🔵 Imágenes con formas

### Imagen circular (avatar)
```kotlin
@Composable
fun Avatar() {
    Image(
        painter = painterResource(R.drawable.perfil),
        contentDescription = "Avatar del usuario",
        contentScale = ContentScale.Crop,
        modifier = Modifier
            .size(80.dp)
            .clip(CircleShape)
    )
}
```

### Imagen con esquinas redondeadas
```kotlin
@Composable
fun ImagenRedondeada() {
    Image(
        painter = painterResource(R.drawable.producto),
        contentDescription = "Producto",
        contentScale = ContentScale.Crop,
        modifier = Modifier
            .size(120.dp)
            .clip(RoundedCornerShape(16.dp))
    )
}
```

### Imagen con borde
```kotlin
@Composable
fun ImagenConBorde() {
    Image(
        painter = painterResource(R.drawable.foto),
        contentDescription = "Foto con borde",
        contentScale = ContentScale.Crop,
        modifier = Modifier
            .size(100.dp)
            .clip(CircleShape)
            .border(3.dp, Color.Blue, CircleShape)
    )
}
```

## 🌐 AsyncImage - Cargar imágenes desde internet

Para cargar imágenes desde URLs, necesitas la librería Coil:

### Agregar dependencia
```kotlin
// En build.gradle.kts (Module: app)
implementation("io.coil-kt:coil-compose:2.5.0")
```

### Usar GlideImage
```kotlin
Añadir en build.gradle.kts (APP)
implementation("com.github.bumptech.glide:compose:1.0.0-beta01")

Añadir permisos en el Manifest
<uses-permission android:name="android.permission.INTERNET" />

@Composable
fun ImagenDeInternet() {
    GlideImage(
        model = "https://upload.wikimedia.org/wikipedia/en/3/35/Supermanflying.png",
        contentDescription = "Superman",
        modifier = Modifier.size(150.dp)
    )
}
```

### Con placeholder y error
```kotlin
@Composable
fun ImagenConPlaceholder() {
    GlideImage(
        model = "https://upload.wikimedia.org/wikipedia/en/3/35/Supermanflying.png",
        contentDescription = "Superman",
        modifier = Modifier.size(150.dp),
        loading = placeholder(R.drawable.baseline_cloud_download_24),
        failure = placeholder(R.drawable.outline_account_circle_off_24)
    )
}
```

## 🎨 Casos de uso comunes

### 1. Card con imagen
```kotlin
@Composable
fun TarjetaConImagen() {
    Card(
        modifier = Modifier
            .fillMaxWidth()
            .padding(8.dp)
    ) {
        Column {
            Image(
                painter = painterResource(R.drawable.producto),
                contentDescription = "Producto",
                contentScale = ContentScale.Crop,
                modifier = Modifier
                    .fillMaxWidth()
                    .height(200.dp)
            )
            Text(
                text = "Nombre del producto",
                modifier = Modifier.padding(16.dp)
            )
        }
    }
}
```

### 2. Lista con avatares
```kotlin
@Composable
fun ContactoConAvatar() {
    Row(
        modifier = Modifier
            .fillMaxWidth()
            .padding(16.dp),
        verticalAlignment = Alignment.CenterVertically
    ) {
        Image(
            painter = painterResource(R.drawable.avatar),
            contentDescription = "Avatar",
            contentScale = ContentScale.Crop,
            modifier = Modifier
                .size(50.dp)
                .clip(CircleShape)
        )
        
        Spacer(modifier = Modifier.width(16.dp))
        
        Column {
            Text("Juan Pérez")
            Text("juan@email.com", color = Color.Gray)
        }
    }
}
```

### 3. Galería simple
```kotlin
@Composable
fun GaleriaSimple() {
    LazyRow(
        horizontalArrangement = Arrangement.spacedBy(8.dp),
        contentPadding = PaddingValues(16.dp)
    ) {
        items(5) { index ->
            Image(
                painter = painterResource(R.drawable.foto),
                contentDescription = "Foto $index",
                contentScale = ContentScale.Crop,
                modifier = Modifier
                    .size(100.dp)
                    .clip(RoundedCornerShape(8.dp))
            )
        }
    }
}
```

## ⚠️ Errores comunes

### Error 1: Olvidar contentDescription
```kotlin
// ❌ MAL - Sin descripción para accesibilidad
Image(
    painter = painterResource(R.drawable.foto),
    contentDescription = null  // Malo para accesibilidad
)

// ✅ BIEN - Con descripción
Image(
    painter = painterResource(R.drawable.foto),
    contentDescription = "Foto de perfil del usuario"
)
```

### Error 2: No controlar el tamaño
```kotlin
// ❌ MAL - Imagen muy grande
Image(
    painter = painterResource(R.drawable.foto_gigante),
    contentDescription = "Foto"
    // Sin modifier - puede ocupar toda la pantalla
)

// ✅ BIEN - Con tamaño controlado
Image(
    painter = painterResource(R.drawable.foto_gigante),
    contentDescription = "Foto",
    modifier = Modifier.size(200.dp)
)
```

### Error 3: ContentScale incorrecto
```kotlin
// ❌ MAL - Imagen distorsionada
Image(
    painter = painterResource(R.drawable.foto),
    contentDescription = "Foto",
    contentScale = ContentScale.FillBounds,  // Puede distorsionar
    modifier = Modifier.size(100.dp)
)

// ✅ BIEN - Mantiene proporción
Image(
    painter = painterResource(R.drawable.foto),
    contentDescription = "Foto",
    contentScale = ContentScale.Crop,  // O ContentScale.Fit
    modifier = Modifier.size(100.dp)
)
```

## 📚 ContentScale - Guía rápida

| ContentScale | ¿Qué hace? | ¿Cuándo usar? |
|--------------|------------|---------------|
| `Crop` | Recorta para llenar el espacio | Avatares, thumbnails |
| `Fit` | Muestra toda la imagen | Logos, iconos importantes |
| `FillBounds` | Estira para llenar | Raramente (distorsiona) |
| `FillWidth` | Llena el ancho | Banners horizontales |
| `FillHeight` | Llena la altura | Imágenes verticales |

## 🎯 Mejores prácticas

### ✅ SÍ hacer:
- Usar `contentDescription` siempre
- Controlar el tamaño con `modifier`
- Usar `ContentScale.Crop` para avatares
- Usar `ContentScale.Fit` para logos
- Optimizar imágenes antes de agregarlas a la app

### ❌ NO hacer:
- Omitir `contentDescription`
- Usar imágenes muy pesadas sin redimensionar
- Usar `FillBounds` si no es necesario
- Cargar muchas imágenes grandes sin lazy loading

## 🔧 Formatos soportados

### ✅ Formatos compatibles:
- **PNG** - Mejor para imágenes con transparencia
- **JPEG** - Mejor para fotos (menor tamaño)
- **WebP** - Buena compresión y calidad
- **GIF** - Animaciones simples
- **SVG** - Gráficos vectoriales (con librerías adicionales)

### 📁 Organización recomendada:
```
res/drawable/
├── ic_launcher.png          // Iconos de la app
├── avatar_placeholder.png   // Placeholder para avatares
├── logo.png                // Logo de la aplicación
└── photo_sample.jpg        // Fotos de ejemplo
```

## 🎉 Resumen

- **`Image`** muestra imágenes en Compose
- **`painterResource()`** para imágenes locales
- **`AsyncImage`** para imágenes de internet
- **`contentScale`** controla cómo se ajusta la imagen
- **`modifier`** controla tamaño y forma
- **`contentDescription`** es obligatorio para accesibilidad

¡Con estos conceptos básicos ya puedes mostrar imágenes en tus aplicaciones Compose! 🚀