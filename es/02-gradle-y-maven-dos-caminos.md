
# 2. Gradle y Maven: Dos caminos para construir proyectos Java

Gradle y Maven son las dos herramientas de automatización de builds más populares en el ecosistema Java. Ambas permiten compilar código, gestionar dependencias, empaquetar artefactos y ejecutar pruebas. Aunque sus filosofías y mecanismos internos difieren, **comparten el objetivo de automatizar tareas repetitivas y asegurar builds consistentes**.

---

## 🔍 Comparativa general

<br>

| **Característica**         | **Gradle**                           | **Maven**                     |
|----------------------------|--------------------------------------|-------------------------------|
| Lenguaje de configuración  | Kotlin/Groovy (DSL flexible)         | XML (estructura declarativa)  |
| Velocidad de compilación   | Alta (build incremental y caché)     | Estable, pero menos optimizada|
| Modularización             | Soporte avanzado                     | Adecuado para estructuras estándar |
| Personalización            | Alta (hooks, tareas, plugins)        | Moderada                      |
| Sistema de tareas          | Basado en tareas (task-based)        | Basado en fases (phase-based) |
| Ecosistema de plugins      | Muy amplio y en crecimiento          | Estable y maduro              |
| Curva de aprendizaje       | Moderada (requiere entender el DSL)  | Suave (basado en convenciones) |

Gradle adopta una filosofía **basada en tareas**, donde cada paso del build puede componerse y extenderse fácilmente.  
Maven, en cambio, utiliza un **modelo basado en fases**, con convenciones predeterminadas que simplifican configuraciones típicas.

---

## 🚀 Ventajas principales de Gradle

- **Alto rendimiento**: gracias a la compilación incremental, caché local/remota y ejecución paralela.
- **DSL expresiva**: configuración declarativa con posibilidad de lógica programática.
- **Soporte fuerte para proyectos multimódulo**, ideal para microservicios o monorepos.
- **Gran integración con herramientas modernas** como Android Studio, Docker, GitHub Actions, etc.

---

## 📘 Ejemplo comparativo

Veamos cómo se define una dependencia en Maven frente a Gradle:

### 📄 `pom.xml` (Maven)

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.ejemplo</groupId>
    <artifactId>demo</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <version>3.2.5</version>
        </dependency>
    </dependencies>
</project>
```

### 📄 `build.gradle.kts` (Gradle)

```kotlin
plugins {
    id("org.springframework.boot") version "3.2.5"
}

dependencies {
    implementation("org.springframework.boot:spring-boot-starter-web")
}
```

📁 **Recomendación**: Agregá al repositorio una carpeta `02-gradle-y-maven` con ambos ejemplos (`pom.xml` y `build.gradle.kts`) para que el lector los pueda comparar directamente.

---

## 📌 ¿Y cuándo elegir Maven?

- Cuando se trabaja en proyectos con estructuras simples o muy estandarizadas.
- En equipos que ya dominan Maven o usan herramientas que lo requieren.
- Para comenzar rápidamente sin necesidad de lógica personalizada.

---

## ⚖️ Benchmark sugerido

> Gradle puede ser hasta un **2-3x más rápido que Maven** en builds incrementales complejos, gracias a su sistema de caché y ejecución paralela.  
> 🔗 [Gradle Build Tool Performance](https://gradle.org/performance/)

> En [LinkedIn Engineering](https://engineering.linkedin.com/blog/2019/01/how-we-improved-our-gradle-build-times-by-over-40-percent), se logró una mejora sustancial en los tiempos de build al migrar de Maven a Gradle.

---

## ✅ Conclusión

Tanto **Gradle como Maven** son opciones válidas y potentes.  
La elección entre uno y otro debe basarse en las **necesidades del equipo, la complejidad del proyecto y el entorno técnico**.

> Gradle ofrece una plataforma poderosa y moderna para quienes buscan flexibilidad, rendimiento y control detallado sobre su build.

---

## 🧠 Ejercicio propuesto

**Objetivo**: Comparar herramientas de construcción en un caso real.

> 🔍 Buscá un proyecto que use Maven y analizá:
> - ¿Qué tareas podrían beneficiarse al usar Gradle?
> - ¿Cómo afectaría al flujo de trabajo diario?
> - ¿Qué partes del `pom.xml` se traducirían directamente en Gradle DSL?

---

## ✅ Checklist de la sección

- ✅ 📚 Comprendí las diferencias clave entre Gradle y Maven
- ✅ 🧠 Identifiqué cuándo usar Gradle y cuándo es preferible Maven
- ✅ 💡 Entendí cómo funciona el modelo basado en tareas (Gradle) vs fases (Maven)
- ✅ 📄 Analicé ambos archivos de ejemplo (`pom.xml` y `build.gradle.kts`)
- ✅ 📁 Creé la carpeta `02-gradle-y-maven` en mi proyecto con los ejemplos incluidos
- ✅ ⚖️ Leí los benchmarks y casos reales como el de LinkedIn
- ✅ 🧪 Reflexioné sobre qué beneficios traería Gradle a un proyecto Maven actual