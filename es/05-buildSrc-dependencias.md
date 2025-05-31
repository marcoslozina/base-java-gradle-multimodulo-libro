
# 5. `buildSrc` y su rol en la arquitectura del build

El directorio `buildSrc/` en Gradle es una herramienta estratégica para organizar la lógica de construcción de forma escalable, modular y centralizada. Al estar diseñado como un subproyecto especial, cualquier clase o constante que se declare en él estará disponible globalmente en todos los `build.gradle.kts`.

En proyectos Java multimódulo —especialmente aquellos que usan Spring Boot—, `buildSrc` permite mantener un **build limpio, consistente y fácil de evolucionar**.

---

## 📁 Carpeta `04-buildsrc-dependencias`

Estructura mínima recomendada:

```
04-buildsrc-dependencias/
└── buildSrc/
    ├── build.gradle.kts
    └── src/main/kotlin/
        ├── Dependencies.kt
        └── Plugins.kt       # Opcional, si centralizas IDs de plugin
```

---

## 🧠 ¿Por qué usar `buildSrc`?

- ✅ Centraliza convenciones, dependencias y versiones.
- ✅ Elimina duplicación de lógica entre módulos.
- ✅ Mejora la experiencia de desarrollo con autocompletado y validación estática en el IDE.
- ✅ Escala mejor que copiar/pegar bloques de configuración.

> 💡 Gradle recomienda comenzar con `buildSrc` antes de migrar a estructuras más avanzadas como `build-logic`.  
> Fuente: [Gradle Docs – Build Logic](https://docs.gradle.org/current/userguide/organizing_gradle_projects.html#sec:build_sources)

---

## 📄 Ejemplo de `gradle.properties`

Centraliza versiones de librerías en el archivo `gradle.properties`:

```properties
# gradle.properties
springBootVersion=3.2.5
junitVersion=5.9.2
```

---

## 📄 Ejemplo de `Dependencies.kt`

```kotlin
object Versions {
    const val springBoot = project.property("springBootVersion") as String
    const val junit = project.property("junitVersion") as String
}

object Dependencies {
    const val springBootStarterWeb = "org.springframework.boot:spring-boot-starter-web:${Versions.springBoot}"
    const val springBootStarterTest = "org.springframework.boot:spring-boot-starter-test:${Versions.springBoot}"
    const val junitJupiterApi       = "org.junit.jupiter:junit-jupiter-api:${Versions.junit}"
    const val junitJupiterEngine    = "org.junit.jupiter:junit-jupiter-engine:${Versions.junit}"
}
```

---

## 📄 Ejemplo de `Plugins.kt` (opcional)

```kotlin
import org.gradle.plugin.use.PluginDependenciesSpec

object PluginIds {
    const val springBoot   = "org.springframework.boot"
    const val dependencyManagement = "io.spring.dependency-management"
}

object PluginVersions {
    const val springBoot = project.property("springBootVersion") as String
}
```

---

## 🔄 Orden de compilación y evaluación en Gradle

Comprender el orden en que Gradle evalúa y compila los distintos archivos es clave para evitar errores comunes y estructurar correctamente los proyectos:

1. **`settings.gradle.kts`**  
   Se ejecuta primero. Aquí aún no están disponibles `gradle.properties` ni `buildSrc`.

2. **`gradle.properties`**  
   Se carga antes de compilar los scripts de construcción. Contiene valores globales reutilizables.

3. **`buildSrc`**  
   Se trata como un subproyecto especial que se compila antes que cualquier módulo.  
   ❗ El contenido de `buildSrc` **no se puede usar en el `build.gradle.kts` raíz**, solo en submódulos.

4. **`build.gradle.kts` (raíz)**  
   Se ejecuta después de compilar `buildSrc`, pero sin acceso directo a sus clases.

5. **`build.gradle.kts` de submódulos**  
   Aquí es donde se debe utilizar lo definido en `buildSrc`.

---

## ✅ Buenas prácticas

- Definir todas las versiones en `gradle.properties` y referenciarlas desde `buildSrc`.
- Utilizar constantes claras y autocontenidas en `Dependencies.kt`.
- Evitar lógica compleja en los `build.gradle.kts` de cada módulo; delegarla a `buildSrc`.
- Versionar `buildSrc` con el mismo criterio que el código de producción, ya que afecta todo el build.
- No usar `Dependencies.kt` en el módulo raíz, ya que puede generar errores de referencia.

---

## 🧠 Ejercicio propuesto

**Objetivo**: Implementar `buildSrc` en tu proyecto.

> 🔨 Crea la carpeta `buildSrc` dentro de `04-buildsrc-dependencias`.  
> 📝 Agrega `gradle.properties` con al menos dos versiones.  
> 💡 Define en `Dependencies.kt` cuatro dependencias usando esas versiones.  
> 🚀 Verifica con `./gradlew build` que todas las referencias funcionan correctamente.

---

## ✅ Checklist de la sección

- ✅ 🏗️ Creé la carpeta `04-buildsrc-dependencias` con el subdirectorio `buildSrc`
- ✅ 📋 Definí versiones en `gradle.properties` (`springBootVersion`, `junitVersion`)
- ✅ 📦 Implementé el archivo `Dependencies.kt` usando versiones desde `gradle.properties`
- ✅ 🔌 (Opcional) Añadí `Plugins.kt` para centralizar IDs y versiones de plugins
- ✅ 🧪 Verifiqué con `./gradlew build` que no hay errores de compilación
- ✅ 🔍 Confirmé que el IDE autocompleta las constantes definidas en `buildSrc`
- ✅ ⚠️ Comprendí que `buildSrc` no se puede usar en `build.gradle.kts` raíz
- ✅ 🔄 Entendí el orden de evaluación: settings → properties → buildSrc → build.gradle.kts