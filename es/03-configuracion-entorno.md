# 🛠️ Configuración profesional del entorno

## 🎯 Objetivo

Antes de comenzar con el desarrollo, es fundamental configurar correctamente el entorno para compilar, ejecutar y depurar proyectos Java modernos sin inconvenientes.

---

## 📋 Requisitos previos

- **Java Development Kit (JDK)**: versión **21**
- **Gradle**: versión **8.7** o superior
- **IDE recomendado**: IntelliJ IDEA (Community o Ultimate)

---

## 🛠️ Instalación y configuración (Linux/macOS)

### Descargar e instalar Gradle manualmente

```bash
wget https://services.gradle.org/distributions/gradle-8.7-bin.zip
sudo unzip gradle-8.7-bin.zip -d /opt/gradle
```

### Configurar variables de entorno

```bash
echo 'export GRADLE_HOME=/opt/gradle/gradle-8.7' >> ~/.bashrc
echo 'export PATH=$PATH:$GRADLE_HOME/bin' >> ~/.bashrc

echo 'export JAVA_HOME=/usr/lib/jvm/java-21-openjdk' >> ~/.bashrc
echo 'export PATH=$PATH:$JAVA_HOME/bin' >> ~/.bashrc

source ~/.bashrc
```

---

## ✅ Verificación del entorno

```bash
java -version             # Esperado: versión 21.x
gradle -v                # Esperado: Gradle 8.7 o superior
echo $JAVA_HOME          # Esperado: /usr/lib/jvm/java-21-openjdk
echo $GRADLE_HOME        # Esperado: /opt/gradle/gradle-8.7
```

💡 En **Windows**, se recomienda usar **Git Bash** o **WSL** para evitar problemas de entorno.

---

## 🧩 Configuración en IntelliJ IDEA

1. Abrí IntelliJ IDEA y seleccioná "Open" o "Import Project".
2. Seleccioná la carpeta raíz del proyecto.
3. IntelliJ detectará `build.gradle.kts` y sugerirá importar como proyecto Gradle.
4. Verificá en Project Structure que esté configurado lo siguiente:

- ✅ JDK 21 como **Project SDK**
- ✅ Gradle desde el sistema (no el wrapper)
- ✅ DSL de Kotlin (`.kts`), no Groovy

---

## ⚙️ Atajos y comandos útiles en IntelliJ

| Acción                           | Ubicación en IntelliJ                                  |
|----------------------------------|---------------------------------------------------------|
| Recargar configuración Gradle   | Botón "Refresh" en Gradle Tool Window                 |
| Configurar JDK del proyecto     | File → Project Structure → Project SDK                 |
| Variables de entorno            | Run → Edit Configurations → Environment Variables      |
| Ejecutar tareas Gradle          | Tool Window → Gradle → doble clic en la tarea          |
| Build completo del proyecto     | Ctrl + F9 o Build → Rebuild                            |

---

## 🧪 Comandos útiles de Gradle

| Comando                 | Descripción                                        |
|-------------------------|----------------------------------------------------|
| `./gradlew build`       | Compila el proyecto y ejecuta tests                |
| `./gradlew clean`       | Limpia artefactos de compilación                   |
| `./gradlew test`        | Ejecuta los tests del proyecto                     |
| `./gradlew dependencies`| Muestra el árbol de dependencias                  |
| `./gradlew tasks`       | Lista todas las tareas disponibles                 |
| `./gradlew bootRun`     | Ejecuta una app Spring Boot (si aplica)            |

---

## ⚠️ Problemas frecuentes

- ❌ No configurar `JAVA_HOME` o `GRADLE_HOME` → errores al compilar o abrir el proyecto.
- ❌ Múltiples versiones activas de Java o Gradle → posibles conflictos.
- ❌ Uso de SDKMAN con JDK 21 → puede causar incompatibilidades si no está bien configurado.
- ❌ No sincronizar el proyecto → usar "Reload Gradle Project" en IntelliJ.
- ❌ No seleccionar correctamente el DSL o el SDK → errores en el IDE.

---

## 🧠 Ejercicio propuesto

🎯 Objetivo: Verificar tu entorno de desarrollo.

1. Instalá **Gradle 8.7** manualmente y configurá la variable `JAVA_HOME`.
2. Ejecutá `gradle -v` y confirmá que estás usando JDK 21.
3. Creá un pequeño `build.gradle.kts` con esta tarea:

```kotlin
tasks.register("hello") {
   doLast {
      println("👋 ¡Hola desde Gradle con Kotlin DSL!")
   }
}
```

4. Ejecutá la tarea:

```bash
./gradlew hello
```


---

## 🧩 Compatibilidad entre versiones de Java, Gradle y Spring Boot

Spring Boot aún **no ofrece soporte completo** para Java 23 en todas sus herramientas, especialmente si usás el DSL de Kotlin (`build.gradle.kts`). Esto puede generar errores al sincronizar el proyecto o durante la compilación con el plugin `spring-boot`.

Por eso, se recomienda utilizar **Java 21 LTS**, que sí cuenta con **compatibilidad total** con:

- Gradle (hasta 8.7+)
- Spring Boot (hasta la 3.2.x)
- Kotlin DSL (`.kts`)
- Librerías del ecosistema moderno de Java

---

## 📊 Tabla comparativa de compatibilidad (resumen)

| Tecnología / Versión        | Java 21 ✅ (recomendado) | Java 23 ⚠️ (experimental) |
|-----------------------------|--------------------------|----------------------------|
| Gradle 8.7+                 | ✅ Totalmente soportado  | ⚠️ Puede fallar con toolchain |
| Spring Boot 3.2+            | ✅ Soportado oficialmente | ❌ No completamente soportado |
| Kotlin DSL (`.kts`)         | ✅ Totalmente funcional  | ⚠️ Incompatibilidades posibles |
| IDE IntelliJ IDEA           | ✅ Soporte completo       | ⚠️ Requiere configuración manual |
| SDKMAN                      | ✅ Compatible con JDK 21 | ⚠️ JDK 23 no siempre disponible |
| Plug-ins (Checkstyle, SpotBugs, etc.) | ✅ Funciona correctamente | ⚠️ Algunos no reconocen Java 23 |



---

## ✅ Checklist de la sección

- ✅ 🔍 Instalé **Java 21** y confirmé con `java -version`
- ✅ 🧱 Instalé **Gradle 8.7** y confirmé con `gradle -v`
- ✅ ⚙️ Configuré las variables de entorno `JAVA_HOME` y `GRADLE_HOME`
- ✅ 📄 Creé y configuré correctamente `gradle.properties`
- ✅ 🧹 Agregué el archivo `.editorconfig` con reglas de estilo
- ✅ 💻 Verifiqué que IntelliJ IDEA usa **Kotlin DSL (`.kts`)** y **JDK 21**
- ✅ 🧪 Ejecuté una tarea simple (`hello`) desde Gradle
- ✅ 📊 Analicé la tabla de compatibilidad y comprendí por qué **Java 21** es recomendado  
