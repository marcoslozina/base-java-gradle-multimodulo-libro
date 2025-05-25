# 3. 🏗 Proyecto profesional Gradle

En esta sección comenzamos la construcción progresiva de un proyecto multimódulo profesional con Gradle, aplicando buenas prácticas de organización y separación de responsabilidades.

---

## 📁 Carpeta `03-estructura-base`

Esta estructura es el punto de partida para cualquier proyecto profesional con arquitectura en capas o hexagonal. Usaremos Kotlin DSL (`.kts`) para la configuración del build, incluso cuando el código de producción esté en Java.

---

## 🧱 Estructura inicial del proyecto

```
gradle-profesional-ejemplo/
├── build.gradle.kts
├── settings.gradle.kts
├── gradle.properties
├── buildSrc/
│   ├── build.gradle.kts
│   └── src/main/kotlin/
│       ├── Dependencies.kt
│       ├── Plugins.kt
│       └── ProjectConventions.kt
├── application/
│   ├── build.gradle.kts
│   ├── src/main/java/
│   └── src/test/java/
├── domain/
│   ├── build.gradle.kts
│   ├── src/main/java/
│   └── src/test/java/
├── infrastructure/
│   ├── build.gradle.kts
│   ├── src/main/java/
│   └── src/test/java/
├── config/
│   ├── build.gradle.kts
│   ├── src/main/java/
│   └── src/test/java/
```

---

## 📄 Propósito de cada módulo

| Módulo          | Propósito                                                                 |
|------------------|---------------------------------------------------------------------------|
| `application`    | Lógica de orquestación, servicios, y casos de uso                         |
| `domain`         | Entidades, interfaces, lógica de negocio puro                             |
| `infrastructure` | Implementaciones técnicas (bases de datos, APIs, etc.)                    |
| `config`         | Configuración de beans, inyección de dependencias, seguridad, etc.        |
| `buildSrc`       | Configuración y reutilización de versiones, dependencias, plugins         |

> Este tipo de estructura promueve un diseño desacoplado y facilita los tests y mantenibilidad a largo plazo.

---

## 📌 Archivos clave a crear

### 🔹 `settings.gradle.kts`

```kotlin
rootProject.name = "gradle-profesional-ejemplo"

include("application", "domain", "infrastructure", "config")
```

### 🔹 `gradle.properties`

```properties
javaVersion=21
group=com.ejemplo
version=1.0.0
```

### 🔹 `build.gradle.kts` (raíz)

```kotlin
plugins {
    kotlin("jvm") version "1.9.0" apply false
}

allprojects {
    repositories {
        mavenCentral()
    }
}
```

---

## ✅ Buenas prácticas

- Crear módulos vacíos para planificar el diseño antes de escribir código.
- Definir nombres coherentes de carpetas y paquetes desde el inicio.
- Mantener el `settings.gradle.kts` siempre actualizado al agregar submódulos.
- Usar `buildSrc` para evitar duplicación y facilitar upgrades centralizados.
- Incluir README por módulo si cada uno tiene responsabilidades claras.

---

## 🧠 Ejercicio propuesto

**Objetivo**: Preparar la estructura base del proyecto.

> 🔧 Inicializá un proyecto vacío en IntelliJ IDEA o desde consola con Gradle y creá los siguientes subproyectos vacíos:  
> `application`, `domain`, `infrastructure`, `config`.

> 📝 Completá los archivos `settings.gradle.kts` y `build.gradle.kts` raíz. Verificá con `./gradlew build` que todo compile sin errores.

---

## ✅ Checklist de la sección

- ✅ 📁 Creé el módulo raíz del proyecto
- ✅ 🧱 Agregué los submódulos `application`, `domain`, `infrastructure` y `config`
- ✅ ⚙️ Definí el archivo `settings.gradle.kts` con los módulos incluidos
- ✅ 🪪 Configuré `gradle.properties` con `group`, `version` y `javaVersion`
- ✅ 📦 Agregué el archivo `build.gradle.kts` con repositorios comunes
- ✅ 🧪 Verifiqué que `./gradlew build` se ejecuta correctamente
- ✅ 🧭 Comprendí el propósito de cada módulo en la arquitectura 