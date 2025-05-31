
# 7. 🧠 Buenas prácticas y errores comunes

---

## ✅ Buenas prácticas recomendadas

> A continuación se detallan buenas prácticas clave acompañadas de ejemplos concretos en Kotlin DSL (`build.gradle.kts`).

1. **Centralizar configuración en `buildSrc/`**

📌 Ejemplo:

```kotlin
// buildSrc/src/main/kotlin/Dependencies.kt
object Deps {
    const val springBootStarterWeb = "org.springframework.boot:spring-boot-starter-web"
}

// build.gradle.kts
dependencies {
    implementation(Deps.springBootStarterWeb)
}
```

Organizá las dependencias y convenciones en clases como `Dependencies.kt` o `Plugins.kt`. Esto reduce la duplicación y mejora la mantenibilidad del proyecto.

2. **Reutilizar configuración con `subprojects {}` o `allprojects {}`**

Estos bloques permiten aplicar reglas comunes (plugins, repositorios, compiladores, encoding, etc.) a todos los módulos, manteniendo scripts más limpios.

3. **Utilizar Kotlin DSL (`.kts`) para los scripts de build**

El DSL tipado permite autocompletado, validación en tiempo de compilación y menor propensión a errores. Ideal si usás IntelliJ IDEA o Android Studio.

4. **Definir versiones y propiedades en `gradle.properties`**

📌 Ejemplo:

```properties
springBootVersion=3.2.1
```

```kotlin
plugins {
    id("org.springframework.boot") version "${springBootVersion}"
}
```

Evitá hardcodear versiones en los scripts. Usar `gradle.properties` centraliza valores y permite sobrescribirlos según el entorno (CI/CD, local, etc.).

5. **Automatizar la detección de actualizaciones**

Incorporá el plugin `com.github.ben-manes.versions` y tareas personalizadas para mantener dependencias actualizadas de forma segura.

6. **Configurar `build scans` para diagnósticos avanzados**

Activar los *build scans* (`--scan`) ayuda a diagnosticar cuellos de botella y errores complejos en pipelines de CI o builds lentos.

7. **Usar convenciones de nombres coherentes en módulos y carpetas**

Mantener un esquema claro (`application`, `domain`, `infrastructure`, etc.) mejora la comprensión del proyecto, especialmente en equipos grandes.

8. **Aplicar convenciones compartidas con `convention plugins`**

En vez de repetir configuraciones con `subprojects {}`, podés usar plugins Gradle personalizados para aplicar convenciones limpias y versionables.

9. **Documentar las tareas personalizadas**

Usar `description` y `group` en cada `task` facilita el descubrimiento de funcionalidades dentro del build.

10. **Aislar configuraciones específicas por entorno (local, CI, producción)**

Usar perfiles (`-Pprofile=ci`) o propiedades externas para adaptar el comportamiento sin modificar los scripts.

11. **Versionar tus builds con lógica semántica o Git tags**

Implementá tareas para que el `version` del proyecto se base en un tag o commit, lo que ayuda a automatizar releases y evitar errores humanos.

12. **Evitar tareas inútiles con `onlyIf {}` o condiciones inteligentes**

Reducí tiempos de build asegurando que las tareas realmente se ejecuten solo cuando corresponde.

---

## ❌ Errores comunes a evitar

> A continuación se presentan errores frecuentes junto con ejemplos que deberías evitar.

1. **Usar SDKMAN con versiones inestables como Java 23**

Algunas herramientas del ecosistema Gradle pueden no ofrecer soporte inmediato. Usar versiones estables minimiza errores con plugins o builds rotos.

2. **No fijar versiones de plugins o dependencias**

❌ Ejemplo:

```kotlin
implementation("org.springframework.boot:spring-boot-starter-web:+")
```

✅ Corrección:

```kotlin
implementation("org.springframework.boot:spring-boot-starter-web:3.2.1")
```

Dejar versiones flotantes (`+`) puede provocar builds no reproducibles o fallos inesperados si las versiones cambian en los repositorios.

3. **Hardcodear strings de dependencias en cada módulo**

❌ Ejemplo:

```kotlin
implementation("org.springframework.boot:spring-boot-starter-data-jpa")
```

✅ Corrección (centralizado en buildSrc):

```kotlin
implementation(Deps.springBootStarterDataJpa)
```

Esto incrementa el esfuerzo de mantenimiento y genera inconsistencias. En su lugar, usá constantes centralizadas (por ejemplo, en `Deps.kt`).

4. **No crear tareas personalizadas reutilizables**

Repetir pasos manuales en scripts o pipelines puede evitarse con tareas Gradle bien definidas y parametrizadas (`register("lintAll") { ... }`).

5. **No limpiar ni estructurar los scripts**

Un `build.gradle.kts` desordenado o con responsabilidades mezcladas dificulta su lectura, testeo y evolución.

---

## 🧠 Ejercicio propuesto

**Objetivo**: Evaluar la calidad de un build existente.

> ✅ Revisá un `build.gradle.kts` que hayas hecho antes.  
> Identificá al menos 3 malas prácticas y corregilas según lo aprendido:
> - Plugins redundantes
> - Dependencias duplicadas
> - Código repetido entre módulos

---

## ✅ Checklist de la sección

- ✅ Todas las versiones están centralizadas en `gradle.properties` o `buildSrc`
- ✅ El código está limpio y bien estructurado con bloques comunes reutilizados
- ✅ No se usan versiones flotantes (`+`) en ninguna dependencia
- ✅ Se utilizan tareas personalizadas en vez de pasos manuales repetidos
- ✅ Se sigue el DSL de Kotlin (`.kts`) para un mejor soporte IDE
- ✅ El build es reproducible, limpio y seguro para escalar en equipo
- ✅ Se aplican convenciones consistentes en nombres y estructura de módulos
- ✅ Las tareas están documentadas con `description` y `group`
- ✅ Se aprovechan features como `onlyIf` y `build scans` para optimizar procesos
- ✅ Se utiliza versionado semántico y adaptabilidad según entorno