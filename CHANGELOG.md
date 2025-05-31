
# 📋 Changelog

## [1.0.0] - 2025-05-26
### Added
- Creación del proyecto base: `base-java-gradle-multimodulo`
- Estructura inicial multimódulo con los módulos: `application`, `domain`, `infrastructure`, `config`
- Configuración del `build.gradle.kts` raíz y de módulos individuales
- Configuración de `buildSrc` para centralizar versiones y dependencias (`Dependencies.kt`, `Plugins.kt`)
- Integración de Java 21 y Spring Boot 3.2
- Aplicación de Kotlin DSL para todos los scripts de Gradle
- Inclusión del plugin `spring-dependency-management` y uso de BOM
- Tareas personalizadas de Gradle: `printVersion`, `lintAll`
- Configuración de `gradle.properties` con control de versiones
- Inclusión de archivo `.gitignore` adaptado a herramientas modernas (IntelliJ, Gradle, Eclipse)
- Configuración de `toolchain` con Java 23 de forma centralizada
- README para el proyecto de ejemplo
- Estructura del eBook creada: `chapters`, `assets`, `templates`
- README del eBook generado con subtítulo explicativo
- Licencia actualizada a “Todos los derechos reservados” (ISBN, DNDA, Safe Creative)
- Registro del libro con título: *Java Multimódulo con Gradle y Spring Boot*