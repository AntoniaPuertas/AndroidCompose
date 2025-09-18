# Tutorial Completo de Jetpack Compose 📱

Este repositorio contiene una guía completa y progresiva para aprender **Jetpack Compose**, el framework moderno de Android para crear interfaces de usuario nativas. Desde conceptos básicos hasta técnicas avanzadas de theming y componentes personalizados.

## 🎯 ¿Para quién es este tutorial?

- **Desarrolladores Android** que quieren migrar a Jetpack Compose
- **Principiantes** en desarrollo de interfaces móviles modernas
- **Desarrolladores experimentados** que buscan una referencia completa
- **Estudiantes** de programación móvil con Kotlin

## 📚 Contenido del Tutorial

### 🚀 **Fundamentos**

#### [01. Introducción a Jetpack Compose](./01-Introducción.md)
Aprende los conceptos básicos creando tu primera aplicación con Compose. Cubre `MainActivity`, `@Composable`, `Scaffold`, y `@Preview`.

**Conceptos clave:** ComponentActivity, setContent, enableEdgeToEdge, estructura básica

#### [02. Trabajando con Múltiples Textos](./02-variosTextos.md)
Evoluciona tu app agregando una data class `Message` y creando tarjetas de mensaje reutilizables.

**Conceptos clave:** Data classes, MessageCard, pasar objetos a Composables, layouts verticales

#### [03. Data Classes en Kotlin - Explicación Detallada](./03-data-class.md)
Profundiza en las data classes: qué son, por qué usarlas y cómo Kotlin genera automáticamente métodos útiles.

**Conceptos clave:** `equals()`, `hashCode()`, `toString()`, `copy()`, destructuring, inmutabilidad

---

### 🏗️ **Layouts y Contenedores**

#### [04. Contenedores de Layout](./04-contenedores.md)
Domina los 5 contenedores esenciales para organizar elementos en la UI: `Column`, `Row`, `Box`, `LazyColumn`, y `LazyRow`.

**Conceptos clave:** Layouts verticales/horizontales, superposición, listas eficientes, performance

#### [05. LazyColumn - Listas Verticales Eficientes](./05-lazy-column.md)
Comprende en profundidad cómo funcionan las listas virtualizadas, el bucle interno y las optimizaciones de memoria.

**Conceptos clave:** Virtualización, lazy loading, bucle mágico `items()`, rendimiento de memoria

#### [06. LazyRow - Listas Horizontales Eficientes](./06-lazy-row.md)
Crea carruseles, chips de categorías y navegación horizontal con scroll fluido y eficiente.

**Conceptos clave:** Scroll horizontal, carruseles, chips, navegación de tabs, control de estado

---

### 🎨 **Componentes y Personalización**

#### [07. Componentes Básicos - Referencia Rápida](./08-componentes-basicos.md)
Guía completa de los 96+ componentes más utilizados en Compose, organizados por categorías con ejemplos listos para usar.

**Conceptos clave:** Text, Image, Button, TextField, Card, Navigation, Material Design

#### [08. Componente Text - Guía Completa](./09-text.md)
Todo sobre el componente más fundamental: tipografía, colores, formateo, texto clickeable, AnnotatedString y accesibilidad.

**Conceptos clave:** Material Typography, overflow, texto seleccionable, enlaces, formato rich

---

### 📐 **Medidas y Dimensiones**

#### [09. Unidades de Medida en Compose](./11-unidades-medida.md)
Domina `dp`, `sp`, `TextUnit`, dimensiones flexibles y responsive design para crear interfaces que se vean perfectas en todos los dispositivos.

**Conceptos clave:** Dp vs Sp, densidad independiente, fillMax, weight, wrapContent, responsive design

---

### 🎨 **Temas y Diseño Visual**

#### [10. Temas en Jetpack Compose](./12-temas.md)
Crea sistemas de diseño completos con Color Schemes, tipografía personalizada, formas, Material You y CompositionLocal.

**Conceptos clave:** MaterialTheme, Color Scheme, tipografía custom, formas, tema claro/oscuro, Material You

---

## 🛠️ **Cómo usar este tutorial**

### 📖 **Lectura secuencial** (Recomendado para principiantes)
Sigue los documentos en orden numérico. Cada capítulo construye sobre conceptos del anterior.

### 🔍 **Consulta por temas** (Para desarrolladores con experiencia)
Usa la tabla de contenido para ir directamente al tema que necesitas.

### 🚀 **Práctica activa**
- Copia y ejecuta todos los ejemplos de código
- Modifica los parámetros para ver cómo cambia el comportamiento
- Crea tus propias variaciones de los componentes

## 🎓 **Progresión de aprendizaje**

```
Principiante                    Intermedio                     Avanzado
     ↓                              ↓                             ↓
01. Introducción            04. Contenedores            09. Unidades de Medida
02. Múltiples Textos        05. LazyColumn              10. Temas Personalizados
03. Data Classes            06. LazyRow                 
                            07. Componentes Básicos      
                            08. Componente Text          
```

## 💡 **Características destacadas**

- ✅ **+500 ejemplos de código** funcionales y reutilizables
- ✅ **Explicaciones paso a paso** de conceptos complejos
- ✅ **Mejores prácticas** y patrones recomendados
- ✅ **Casos de uso del mundo real** (chats, galerías, formularios)
- ✅ **Optimizaciones de performance** incluidas
- ✅ **Consideraciones de accesibilidad** en cada capítulo
- ✅ **Material Design 3** y Material You
- ✅ **Responsive design** para diferentes tamaños de pantalla

## 📱 **Compatibilidad**

- **Android API Level:** 21+ (Android 5.0)
- **Jetpack Compose:** 1.5.0+
- **Kotlin:** 1.8.0+
- **Material Design:** 3.0

## 🤝 **Contribuciones**

Este tutorial está en constante evolución. Si encuentras errores, tienes sugerencias de mejora o quieres contribuir con nuevos ejemplos, ¡tu aportación es bienvenida!

## 📈 **Próximos capítulos**

- **Animaciones en Compose**
- **Navegación con Navigation Compose**
- **Estado y arquitectura (ViewModel, State Hoisting)**
- **Testing de interfaces Compose**
- **Performance avanzada y optimizaciones**
- **Integración con Views tradicionales**

---

## 🏆 **Al completar este tutorial sabrás:**

- ✅ Crear interfaces modernas con Jetpack Compose
- ✅ Manejar estado y recomposición eficientemente  
- ✅ Implementar layouts complejos y responsivos
- ✅ Aplicar temas y sistemas de diseño consistentes
- ✅ Optimizar performance y accesibilidad
- ✅ Seguir las mejores prácticas de Material Design
- ✅ Crear componentes reutilizables y modulares

---

**¡Comienza tu viaje con Jetpack Compose!** 🚀

Empieza con [01. Introducción a Jetpack Compose](./01-Introducción.md) y descubre el futuro del desarrollo de interfaces en Android.