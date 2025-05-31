
# 📘 Glosario

Este glosario recopila los términos clave utilizados a lo largo del eBook para facilitar su comprensión y consulta rápida.

---

### 🔧 Gradle
Herramienta moderna de automatización de builds para la JVM y otros entornos. Permite compilar, testear, empaquetar y desplegar aplicaciones. Destaca por su rendimiento incremental, uso de caché y flexibilidad mediante DSL en Kotlin o Groovy.

---

### 🧠 DSL (Domain Specific Language)
Lenguaje específico de dominio que permite describir procesos complejos de forma declarativa. Gradle ofrece soporte para Kotlin DSL (tipado, moderno) y Groovy DSL (dinámico, ampliamente adoptado).

---

### 📦 BOM (Bill of Materials)
Conjunto de versiones compatibles entre dependencias, centralizado en un archivo compartido. Gradle lo interpreta automáticamente si se usa Spring Boot o el plugin `io.spring.dependency-management`.

---

### 🧩 `buildSrc/`
Subproyecto especial que permite encapsular lógica del build como código real en Kotlin o Java. Se compila automáticamente antes del resto del proyecto, y su contenido está disponible globalmente.

---

### 🔌 Plugin
Componente reutilizable que agrega tareas, configuraciones o convenciones al proyecto Gradle. Puede ser oficial, de terceros o personalizado, y se declara con `id(...)` en el bloque `plugins`.

---

### 📚 Dependencia
Biblioteca externa o interna que el proyecto necesita para compilar o ejecutarse. Se declara con configuraciones como `implementation`, `testImplementation`, `runtimeOnly`, entre otras.

---

### 🧪 JUnit
Framework de pruebas unitarias para Java. Gradle lo integra fácilmente mediante `spring-boot-starter-test` o `junit-jupiter`. Es la base de la mayoría de estrategias de testing automatizado en el ecosistema JVM.

---

### 📈 JaCoCo
Herramienta de cobertura de código. Informa qué líneas fueron ejecutadas por los tests, ayudando a evaluar la efectividad del testing. Gradle lo soporta mediante el plugin `jacoco`.

---

### 🔄 CI/CD (Integración Continua / Despliegue Continuo)
CI (Integración Continua) automatiza compilación y testing en cada cambio.  
CD (Despliegue Continuo) extiende esta automatización hasta producción. Herramientas comunes: GitHub Actions, GitLab CI/CD, Jenkins.

---

### 🧱 Multimódulo
Organización del proyecto en submódulos independientes, conectados por configuración. Favorece el testing aislado, la reutilización y la escalabilidad en arquitecturas complejas.

---

### 🧰 Monorepo
Estructura de repositorio único que contiene múltiples módulos o servicios. Facilita el control de versiones y la consistencia entre proyectos relacionados.

---

### 🧪 Tarea Gradle
Unidad atómica de ejecución en un build Gradle. Cada `task` representa una acción concreta, como compilar (`build`), limpiar (`clean`), correr tests (`test`) o ejecutar la app (`bootRun`).

---

### 🛠️ `build.gradle.kts`
Archivo de configuración de build escrito en Kotlin DSL. Define plugins, dependencias, tareas, repositorios y configuración del proyecto.

---

### 🧾 `gradle.properties`
Archivo de propiedades globales o por entorno. Se usa para definir versiones, flags, credenciales, parámetros JVM o configuración reutilizable entre módulos.

---

### 📂 `settings.gradle.kts`
Archivo que configura el proyecto raíz, su nombre y los submódulos incluidos. También puede aplicar lógica condicional para builds compuestos.

---

### 🌐 `start.spring.io`
Generador online oficial de proyectos Spring Boot. Permite seleccionar dependencias, versión, empaquetado, sistema de build y lenguaje (Java, Kotlin, Groovy).