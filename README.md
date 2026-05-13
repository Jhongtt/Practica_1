# Practica_1
# Práctica 1 — Jetpack Compose Básico

> Construye una pantalla de perfil usando **únicamente** composables básicos:  
> `Surface` · `Box` · `Column` · `Row` · `Text` · `Button` · `Spacer`

---

##  Estructura del proyecto

```
app/src/main/java/com/example/practica1/
│
├── MainActivity.kt                  ← Entry point de la app
│
├── screens/
│   └── ProfileScreen.kt             ← Pantalla principal (arma todo junto)
│
└── components/
    ├── ProfileHeader.kt             ← Título "Mi Perfil" y subtítulo
    ├── ProfileAvatar.kt             ← Círculo con ícono de usuario
    ├── ProfileInfoCard.kt           ← Tarjeta con Nombre, Correo, Curso, Estado
    ├── ProfileActions.kt            ← Botones Editar y Guardar (Row)
    └── ProfileBanner.kt             ← Caja inferior con texto centrado
```

---

##  Cómo crear el proyecto desde cero

### Paso 1 — Crear proyecto en Android Studio

1. Abre **Android Studio**
2. Click en **New Project**
3. Selecciona **Empty Activity** (la de Compose)
4. Configura:
   - **Name:** `Practica1`
   - **Package name:** `com.example.practica1`
   - **Language:** Kotlin
   - **Minimum SDK:** API 24
5. Click **Finish** y espera que gradle sincronice

---

### Paso 2 — Verificar dependencias en `build.gradle` (módulo app)

Asegúrate de tener esto en `app/build.gradle`:

```kotlin
dependencies {
    implementation("androidx.core:core-ktx:1.12.0")
    implementation("androidx.activity:activity-compose:1.8.2")
    implementation(platform("androidx.compose:compose-bom:2024.02.00"))
    implementation("androidx.compose.ui:ui")
    implementation("androidx.compose.material3:material3")
    implementation("androidx.compose.material:material-icons-extended") // ← para los íconos
    implementation("androidx.compose.ui:ui-tooling-preview")
    debugImplementation("androidx.compose.ui:ui-tooling")
}
```

> Si no tienes `material-icons-extended`, agrégala y haz click en **Sync Now**.

---

### Paso 3 — Crear las carpetas

Dentro de `app/src/main/java/com/example/practica1/`:

1. Click derecho → **New → Package** → escribe `screens`
2. Click derecho → **New → Package** → escribe `components`

---

### Paso 4 — Crear los archivos

Click derecho sobre la carpeta → **New → Kotlin Class/File** → elige **File** → pega el código.

####  `MainActivity.kt` (reemplaza el que ya existe)

```kotlin
package com.example.practica1

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.material3.MaterialTheme
import com.example.practica1.screens.ProfileScreen

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MaterialTheme {
                ProfileScreen()
            }
        }
    }
}
```

---

####  `screens/ProfileScreen.kt`

```kotlin
package com.example.practica1.screens

import androidx.compose.foundation.layout.*
import androidx.compose.material3.Surface
import androidx.compose.runtime.Composable
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import com.example.practica1.components.*

@Composable
fun ProfileScreen() {
    Surface(
        modifier = Modifier.fillMaxSize(),
        color = Color(0xFFF5F6FA)
    ) {
        Column(
            modifier = Modifier
                .fillMaxSize()
                .padding(24.dp),
            horizontalAlignment = Alignment.CenterHorizontally
        ) {
            ProfileHeader()

            Spacer(modifier = Modifier.height(24.dp))

            ProfileAvatar()

            Spacer(modifier = Modifier.height(24.dp))

            ProfileInfoCard()

            Spacer(modifier = Modifier.height(20.dp))

            ProfileActions()

            Spacer(modifier = Modifier.height(20.dp))

            ProfileBanner()
        }
    }
}

@Preview(showBackground = true, showSystemUi = true)
@Composable
fun ProfileScreenPreview() {
    ProfileScreen()
}
```

---

####  `components/ProfileHeader.kt`

```kotlin
package com.example.practica1.components

import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.unit.sp

@Composable
fun ProfileHeader() {
    Column(
        horizontalAlignment = Alignment.CenterHorizontally,
        modifier = Modifier.fillMaxWidth()
    ) {
        Text(
            text = "Mi Perfil",
            fontSize = 28.sp,
            fontWeight = FontWeight.Bold,
            color = Color(0xFF1A1A2E)
        )
        Text(
            text = "Jetpack Compose Básico",
            fontSize = 14.sp,
            color = Color(0xFF6B7280)
        )
    }
}
```

---

####  `components/ProfileAvatar.kt`

```kotlin
package com.example.practica1.components

import androidx.compose.foundation.background
import androidx.compose.foundation.border
import androidx.compose.foundation.layout.Box
import androidx.compose.foundation.layout.size
import androidx.compose.foundation.shape.CircleShape
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.Person
import androidx.compose.material3.Icon
import androidx.compose.runtime.Composable
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.draw.clip
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.unit.dp

@Composable
fun ProfileAvatar() {
    Box(
        contentAlignment = Alignment.Center,
        modifier = Modifier
            .size(120.dp)
            .clip(CircleShape)
            .background(Color(0xFFE0E7FF))
            .border(3.dp, Color(0xFF6366F1), CircleShape)
    ) {
        Icon(
            imageVector = Icons.Default.Person,
            contentDescription = "Avatar del usuario",
            tint = Color(0xFF6366F1),
            modifier = Modifier.size(72.dp)
        )
    }
}
```

---

####  `components/ProfileInfoCard.kt`

```kotlin
package com.example.practica1.components

import androidx.compose.foundation.border
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp

@Composable
fun ProfileInfoCard() {
    Column(
        modifier = Modifier
            .fillMaxWidth()
            .border(1.dp, Color(0xFFE5E7EB), RoundedCornerShape(12.dp))
            .padding(16.dp),
        verticalArrangement = Arrangement.spacedBy(14.dp)
    ) {
        InfoItem(label = "Nombre:", value = "Ana López")
        InfoItem(label = "Correo:", value = "ana.lopez@estudiante.com")
        InfoItem(label = "Curso:", value = "Desarrollo Android")
        InfoItem(label = "Estado:", value = "Activo", valueColor = Color(0xFF16A34A))
    }
}

@Composable
fun InfoItem(
    label: String,
    value: String,
    valueColor: Color = Color(0xFF1A1A2E)
) {
    Column {
        Text(
            text = label,
            fontSize = 12.sp,
            color = Color(0xFF6B7280)
        )
        Text(
            text = value,
            fontSize = 16.sp,
            fontWeight = FontWeight.SemiBold,
            color = valueColor
        )
    }
}
```

---

####  `components/ProfileActions.kt`

```kotlin
package com.example.practica1.components

import androidx.compose.foundation.layout.*
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.material3.Button
import androidx.compose.material3.ButtonDefaults
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.unit.dp

@Composable
fun ProfileActions() {
    Row(
        modifier = Modifier.fillMaxWidth(),
        horizontalArrangement = Arrangement.spacedBy(12.dp)
    ) {
        Button(
            onClick = { },
            modifier = Modifier.weight(1f),
            colors = ButtonDefaults.buttonColors(
                containerColor = Color(0xFF7C3AED)
            ),
            shape = RoundedCornerShape(8.dp)
        ) {
            Text(
                text = "Editar",
                color = Color.White,
                fontWeight = FontWeight.SemiBold
            )
        }

        Button(
            onClick = { },
            modifier = Modifier.weight(1f),
            colors = ButtonDefaults.buttonColors(
                containerColor = Color(0xFF16A34A)
            ),
            shape = RoundedCornerShape(8.dp)
        ) {
            Text(
                text = "Guardar",
                color = Color.White,
                fontWeight = FontWeight.SemiBold
            )
        }
    }
}
```

---

####  `components/ProfileBanner.kt`

```kotlin
package com.example.practica1.components

import androidx.compose.foundation.background
import androidx.compose.foundation.border
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.Info
import androidx.compose.material3.Icon
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp

@Composable
fun ProfileBanner() {
    Box(
        contentAlignment = Alignment.Center,
        modifier = Modifier
            .fillMaxWidth()
            .background(Color(0xFFEEF2FF), RoundedCornerShape(12.dp))
            .border(1.dp, Color(0xFFC7D2FE), RoundedCornerShape(12.dp))
            .padding(20.dp)
    ) {
        Column(horizontalAlignment = Alignment.CenterHorizontally) {
            Icon(
                imageVector = Icons.Default.Info,
                contentDescription = "Información",
                tint = Color(0xFF6366F1),
                modifier = Modifier.size(28.dp)
            )
            Spacer(modifier = Modifier.height(8.dp))
            Text(
                text = "Práctica de layouts en Compose",
                fontSize = 14.sp,
                fontWeight = FontWeight.Medium,
                color = Color(0xFF4338CA)
            )
        }
    }
}
```

---

### Paso 5 — Ejecutar

1. Conecta un emulador o dispositivo físico
2. Click en  **Run** (o `Shift + F10`)
3. ¡Listo!

---

## Qué hace cada composable

| Composable | Archivo | Para qué |
|---|---|---|
| `Surface` | `ProfileScreen` | Fondo general de la pantalla |
| `Column` | `ProfileScreen`, `ProfileHeader`, `ProfileInfoCard`, `ProfileBanner` | Apila elementos verticalmente |
| `Row` | `ProfileActions` | Pone los botones uno al lado del otro |
| `Box` | `ProfileAvatar`, `ProfileBanner` | Centra el contenido dentro |
| `Text` | Todos | Muestra textos y etiquetas |
| `Button` | `ProfileActions` | Botones Editar y Guardar |
| `Spacer` | `ProfileScreen`, `ProfileBanner` | Espacio entre elementos |

---

##  Restricciones cumplidas

-  `Surface`  contenedor principal
-  `Box`  centra avatar y banner
-  `Column`  organiza todo verticalmente
- `Row` — organiza botones horizontalmente
-  `Text`  todos los textos
-  `Button` — Editar y Guardar
-  `Spacer` — espacios verticales y horizontales
-  Sin `LazyColumn`, `Cards`, `Scaffold`, `Navigation` ni componentes avanzados
