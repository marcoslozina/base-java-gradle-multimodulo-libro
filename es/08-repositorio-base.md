
# 8. 📦 Repositorio base del proyecto

El proyecto completo utilizado como referencia en este eBook se encuentra publicado en GitHub:

👉 **[github.com/marcoslozina/gradle-profesional-ejemplo](https://github.com/marcoslozina/base-java-gradle-multimodulo)**

Este repositorio constituye una base profesional para proyectos en Java con Spring Boot, incorporando una estructura moderna, tareas automatizadas y convenciones escalables, ideal para equipos que trabajan con microservicios o aplicaciones de mediana a gran escala.

---

## 🛠️ Componentes destacados del repositorio

### 🔧 Lenguaje y herramientas

- Java 21 como lenguaje principal
- Spring Boot 3.2.x
- Gradle con Kotlin DSL (`.kts`)
- Toolchain configurado desde `buildSrc` con `JavaLanguageVersion.of(...)`

### 🧱 Estructura del proyecto

Organizado como un proyecto **multimódulo** con arquitectura hexagonal:

- `application/`: lógica de aplicación y coordinación
- `domain/`: modelo de negocio y entidades puras
- `infrastructure/`: adaptadores externos (base de datos, APIs, etc.)
- `config/`: configuración técnica de Spring Boot

```kotlin
// settings.gradle.kts
include("application", "domain", "infrastructure", "config")
```

---

### ⚙️ Configuración centralizada

El proyecto aplica las siguientes convenciones:

- `gradle.properties`: define `springBootVersion`, `javaVersion`, `group`, entre otros
- `buildSrc/`: contiene clases como `Dependencies.kt`, `Versions.kt`, `Plugins.kt` y `CustomTasks.kt`  
  Se aplican automáticamente al resto del proyecto sin duplicación

```kotlin
val springBootVersion by extra("3.2.5")
```

```kotlin
// buildSrc/src/main/kotlin/Dependencies.kt
object Deps {
    const val springBootStarterWeb = "org.springframework.boot:spring-boot-starter-web"
}
```

---

### 🧪 Tareas personalizadas

Desde `CustomTasks.kt` se definen tareas como:

```kotlin
tasks.register("printVersion") {
    group = "info"
    description = "Imprime la versión del proyecto"
    doLast {
        println("Versión actual: ${project.version}")
    }
}
```

---

### 📂 Archivos profesionales incluidos

El repositorio contiene archivos esenciales para proyectos maduros:

- `README.md`: documentación de uso
- `LICENSE`: licencia MIT
- `CHANGELOG.md`: historial de cambios
- `.gitignore`: configurado para entornos Java, Gradle e IntelliJ

---


## 📚 Recursos adicionales

- 📘 [Documentación oficial de Gradle](https://docs.gradle.org/current/userguide/)
- 🚀 [Spring Initializr - start.spring.io](https://start.spring.io/)
- 📦 [Guía oficial del plugin de Spring Boot](https://docs.spring.io/spring-boot/docs/current/gradle-plugin/reference/htmlsingle/)
- 🧩 [Guía oficial de Kotlin DSL](https://docs.gradle.org/current/userguide/kotlin_dsl.html)
- 🌱 [Guía de Spring Boot con Kotlin (opcional)](https://spring.io/guides/tutorials/spring-boot-kotlin/)

---

## 🧠 Ejercicio propuesto

**Objetivo**: Explorar y adaptar el repositorio de ejemplo.

> 🧪 Cloná el repositorio base del eBook:  
> [github.com/marcoslozina/gradle-profesional-ejemplo](https://github.com/marcoslozina/gradle-profesional-ejemplo)

- Ejecutá `./gradlew printVersion` y verificá los módulos incluidos
- Navegá `buildSrc` e intentá personalizar una tarea o modificar una dependencia

---

## ✅ Checklist de revisión

- ✅ Cloné el repositorio `gradle-profesional-ejemplo`
- ✅ Verifiqué la estructura multimódulo y los archivos de configuración
- ✅ Comprendí el rol de `buildSrc` y sus clases (`Dependencies`, `Plugins`, `CustomTasks`)
- ✅ Ejecuté tareas como `printVersion` desde consola
- ✅ Exploré y edité valores en `gradle.properties`
- ✅ Confirmé que el proyecto compila correctamente con `./gradlew build`  