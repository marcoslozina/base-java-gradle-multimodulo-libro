
# 6. 📌 Gestión de versiones con BOM en Spring Boot

📁 Carpeta: `05-bom-spring`

---

## 🎯 Introducción

En proyectos profesionales con Spring Boot, mantener la coherencia entre versiones de librerías es fundamental para evitar conflictos, errores sutiles y dificultades de mantenimiento. Aquí es donde el concepto de **BOM** (Bill of Materials) resulta esencial.

El BOM es un archivo que declara un conjunto de versiones estables y compatibles de librerías, permitiendo declarar dependencias **sin especificar sus versiones manualmente**. Spring Boot incorpora su propio BOM, el cual se activa automáticamente al usar el plugin `org.springframework.boot`.

---

## 🧱 ¿Cómo funciona?

Gradle utiliza el BOM cuando aplicamos uno de los siguientes mecanismos:

- El plugin oficial de Spring Boot:
  ```kotlin
  id("org.springframework.boot") version "3.2.1"
  ```
- El plugin `io.spring.dependency-management` (en desuso para versiones modernas).

En tu proyecto (`gradle-profesional-ejemplo`), la declaración actual de plugins es la siguiente:

```kotlin
plugins {
    id("org.springframework.boot") version "3.2.1"
    id("io.spring.dependency-management") version "1.1.4"
}
```

Esto asegura que todas las dependencias `spring-boot-starter-*` usen versiones consistentes con el BOM.

---

## ✅ Ejemplo en tu proyecto real

Archivo: `gradle-profesional-ejemplo/build.gradle.kts`

```kotlin
dependencies {
    implementation("org.springframework.boot:spring-boot-starter-web")
    implementation("org.springframework.boot:spring-boot-starter-actuator")
    testImplementation("org.springframework.boot:spring-boot-starter-test")
}
```

👉 Ninguna dependencia especifica su versión. Esta es gestionada por el BOM, manteniendo la coherencia.

---

## ❌ ¿Qué evitar?

Evitar declarar versiones explícitas como en el siguiente ejemplo:

```kotlin
// ⚠️ Mal ejemplo
implementation("org.springframework.boot:spring-boot-starter-web:3.2.1")
```

Esto puede generar conflictos con otras versiones internas del BOM, rompiendo la estabilidad del build.

---

## 💡 Alternativa moderna: Uso explícito del BOM con `platform()`

A partir de Gradle 5+, se puede importar un BOM manualmente con `platform()`. Por ejemplo:

```kotlin
dependencies {
    implementation(platform("org.springframework.boot:spring-boot-dependencies:3.2.1"))
    implementation("org.springframework.boot:spring-boot-starter-web")
}
```

Esto es útil si no estás usando el plugin completo de Spring Boot pero querés aprovechar su BOM.

---

## 📚 Tipos de dependencias en Gradle

| Tipo                 | Descripción                                                      |
|----------------------|------------------------------------------------------------------|
| `implementation`     | Recomendado por defecto, mantiene bajo acoplamiento              |
| `api`                | Expone dependencias a otros módulos (usarlo solo si es necesario) |
| `compileOnly`        | Solo necesario en compilación, como anotaciones                  |
| `runtimeOnly`        | Se usa solo en tiempo de ejecución                               |
| `testImplementation` | Solo accesible en tests                                          |

---

## 🔄 Flujo profesional de actualización de versiones

1. Verificar la última versión estable de Spring Boot en [start.spring.io](https://start.spring.io)
2. Leer el [changelog oficial](https://github.com/spring-projects/spring-boot/releases)
3. Actualizar la versión del plugin en `build.gradle.kts`
4. Ejecutar:

```bash
./gradlew dependencyUpdates
```

Con el siguiente plugin para detectar versiones obsoletas:

```kotlin
plugins {
    id("com.github.ben-manes.versions") version "0.48.0"
}
```

5. Ejecutar los tests automatizados para validar la compatibilidad.
6. Automatizar este flujo con herramientas como RenovateBot o GitHub Actions.

---

## ❗ Errores frecuentes

- ❌ Declarar versiones explícitas en dependencias del ecosistema Spring Boot
- ❌ Usar `api` sin justificación técnica, exponiendo detalles internos
- ❌ Incluir librerías externas que tienen versiones incompatibles con el BOM

---

## 🧠 Ejercicio propuesto

**Objetivo**: Incorporar un BOM de forma explícita con `platform()`.

1. Crear un nuevo módulo.
2. Agregar esta configuración en el `build.gradle.kts` del nuevo módulo:

```kotlin
dependencies {
    implementation(platform("org.springframework.boot:spring-boot-dependencies:3.2.1"))
    implementation("org.springframework.boot:spring-boot-starter-validation")
}
```

3. Ejecutar el proyecto y comprobar que la resolución de dependencias funciona correctamente sin versiones explícitas.

---

## ✅ Checklist de la sección

- ✅ El plugin `org.springframework.boot` está aplicado correctamente
- ✅ No se declaran versiones manualmente en `spring-boot-starter-*`
- ✅ Las actualizaciones de Spring Boot se centralizan en un solo lugar
- ✅ Se usa `implementation` salvo casos justificados con `api` o `compileOnly`
- ✅ Se automatiza la verificación de versiones con `dependencyUpdates`
- ✅ Se ejecutan tests luego de cualquier actualización de versión
- ✅ El equipo comprende y respeta la política del BOM 