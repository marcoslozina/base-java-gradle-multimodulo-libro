
# 10. ✅ Testing e Integración Continua con Gradle

Una base profesional no solo debe compilar correctamente. También debe contar con mecanismos de validación continua que aseguren calidad, estabilidad y confiabilidad.  
En esta sección abordamos cómo implementar **pruebas automatizadas** y configurar **pipelines de CI** utilizando herramientas estándar del ecosistema: Gradle, JUnit, JaCoCo y GitHub Actions.

---

## 🧪 Testing automatizado con JUnit

El proyecto `gradle-profesional-ejemplo` utiliza `spring-boot-starter-test` como base para la estrategia de pruebas. Esta dependencia ya se encuentra definida en el archivo `build.gradle.kts` común:

```kotlin
dependencies {
    testImplementation("org.springframework.boot:spring-boot-starter-test")
}
```

Para ejecutar los tests:

```bash
./gradlew test
```

Los resultados se encuentran en:  
📁 `build/test-results/test/`

---

## 📈 Cobertura de código con JaCoCo

La cobertura está integrada en el build raíz. Verificá que el plugin esté habilitado:

```kotlin
plugins {
    jacoco
}
```

Y la tarea `jacocoTestReport` definida:

```kotlin
tasks.jacocoTestReport {
    dependsOn(test)
    reports {
        xml.required.set(true)
        html.required.set(true)
    }
}
```

Para ejecutarla:

```bash
./gradlew jacocoTestReport
```

Reporte generado en:  
📁 `build/reports/jacoco/test/html/index.html`

---

## 🤖 Integración Continua (CI) con GitHub Actions

Este proyecto ya incluye una configuración funcional de CI en `.github/workflows/ci.yml`. La pipeline ejecuta:

- Checkout del código
- Compilación y testeo
- Generación de cobertura con JaCoCo

Extracto relevante del archivo:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Set up JDK
        uses: actions/setup-java@v3
        with:
          java-version: '21'
          distribution: 'temurin'

      - name: Build with Gradle
        run: ./gradlew build

      - name: Run tests
        run: ./gradlew test

      - name: Generate coverage report
        run: ./gradlew jacocoTestReport
```

---

## 🛠️ Tareas Gradle personalizadas

El proyecto incluye tareas personalizadas definidas en `buildSrc/CustomTasks.kt`, como:

```kotlin
tasks.register("testCoverage") {
    group = "verification"
    description = "Ejecuta tests y genera reporte de cobertura"
    dependsOn("test", "jacocoTestReport")
}
```

Esto permite consolidar múltiples pasos en una sola orden reproducible:

```bash
./gradlew testCoverage
```

---

## 📚 Buenas prácticas adicionales

- 📌 Verificá que las pruebas cubran tanto lógica de dominio como adaptadores
- 📌 Integra reportes de cobertura en CI (por ejemplo, con Codecov)
- 📌 Usá tareas `check`, `build` y `verification` en tu pipeline de forma consistente
- 📌 Automatizá validaciones antes de hacer merges en ramas principales (`main`, `release`)

---

## ✅ Conclusión

La integración de pruebas y CI es esencial en cualquier equipo profesional moderno.  
No solo previene errores, sino que establece una base sólida para escalar con confianza.

---

## 🧠 Ejercicio propuesto

**Objetivo**: Automatizar validaciones en tu pipeline de CI.

> ⚙️ Agregá un archivo `.github/workflows/ci.yml` en tu proyecto Gradle.
> - Ejecutá tareas `build`, `test` y `jacocoTestReport`.
> - Activá los reportes HTML y verificá tu cobertura localmente.
> - (Opcional) Subí el reporte a un servicio como Codecov o Coveralls.

💬 **Reflexioná**: ¿qué errores detectó tu pipeline antes de tiempo?  
¿Cómo impacta esto en la calidad del equipo?

---

## ✅ Checklist de implementación

- ✅ Agregué y ejecuté pruebas automatizadas con JUnit
- ✅ Activé el plugin JaCoCo y generé reportes de cobertura HTML
- ✅ Configuré un pipeline de CI con GitHub Actions
- ✅ Consolidé tareas en comandos personalizados como `testCoverage`
- ✅ Verifiqué que todos los módulos se compilan correctamente en CI
- ✅ Aseguré que los reportes se mantengan actualizados con cada commit