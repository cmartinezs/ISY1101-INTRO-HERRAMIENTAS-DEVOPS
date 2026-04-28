# Guía: Automatización de controles de calidad en un pipeline CI/CD con GitHub Actions

---

| Sigla/Asignatura | Semana Disponible EFT | Experiencia de Aprendizaje |
|---|---:|---|
| ISY1101 - Introducción a Herramientas DevOps | 18 | EA 2 |

| Tiempo | Modalidad de Trabajo | Indicadores de Logro |
|---|---|---|
| 5 hrs | Presencial | IL 2.3 |

---

## Resultados de aprendizaje

· **RA2** Aplica herramientas de calidad de software dentro de un flujo de desarrollo, evaluando el estado de un artefacto mediante análisis estático y dinámico para determinar su aptitud de integración en un proceso CI/CD.

---

## Contenidos

Automatización de controles de calidad dentro de un pipeline CI/CD, incorporando pruebas unitarias, cobertura, análisis con SonarQube, validaciones de aceptación, pruebas E2E y pruebas de rendimiento con JMeter. La actividad utiliza GitHub Actions como ejemplo de plataforma CI/CD, manteniendo un enfoque adaptable a distintos lenguajes, frameworks y tipos de artefactos.

---

## Actividades

### Actividad: Implementación automatizada de controles de calidad en CI/CD

En esta actividad, las y los estudiantes deberán tomar las validaciones ejecutadas manualmente en la actividad anterior y automatizarlas dentro de un pipeline CI/CD.

La actividad es **agnóstica a la tecnología del artefacto de software**, por lo que puede aplicarse sobre una API REST, aplicación web, backend, frontend, microservicio u otro sistema desarrollado previamente, siempre que permita ejecutar comandos de pruebas, análisis y validación desde terminal.

El pipeline deberá ejecutar controles de **análisis estático** y **análisis dinámico**, generando evidencia de los resultados y definiendo qué fallos deben bloquear el avance del flujo.

---

## Objetivo

Los estudiantes deberán implementar un pipeline CI/CD que automatice las validaciones de calidad aplicadas previamente de forma manual, usando GitHub Actions u otra herramienta equivalente, para determinar si un artefacto de software puede avanzar dentro de un flujo de integración continua.

---

## Puntos a recalcar

· Un pipeline CI/CD permite ejecutar validaciones de forma automática ante cambios en el repositorio.  
· Los test unitarios, la cobertura y SonarQube deben ejecutarse antes de aceptar cambios como integrables.  
· Las pruebas dinámicas requieren levantar el sistema o usar un ambiente de prueba disponible.  
· Los secretos, tokens y credenciales no deben quedar escritos directamente en archivos del repositorio.  
· Un pipeline puede bloquearse por errores críticos o solo emitir advertencias según el criterio definido por el equipo.  
· Automatizar una herramienta no reemplaza la interpretación técnica de sus resultados.  
· El pipeline debe reflejar los comandos reales usados por el proyecto, no comandos genéricos copiados sin validar.

---

## Herramientas sugeridas

Las herramientas pueden variar según la tecnología del proyecto, pero se recomienda utilizar:

· GitHub Actions como plataforma CI/CD.  
· Herramienta de test unitario propia del stack del proyecto.  
· Herramienta de cobertura propia del stack del proyecto.  
· SonarQube o SonarCloud para análisis de calidad de código.  
· SonarScanner, Maven, Gradle, npm, dotnet u otra herramienta compatible.  
· Herramienta de pruebas de aceptación o E2E, si el proyecto la posee.  
· Docker o Docker Compose, si el sistema requiere servicios auxiliares.  
· JMeter para pruebas de rendimiento en modo consola.  
· GitHub Secrets para tokens, URLs y credenciales.

---

## Prerrequisitos

Antes de iniciar la actividad, cada equipo debe contar con:

· Repositorio del artefacto publicado en GitHub.  
· Código fuente del artefacto evaluado.  
· Comandos manuales ya identificados para test, cobertura, SonarQube, E2E y JMeter.  
· Archivo `.jmx` de JMeter creado y validado manualmente.  
· Proyecto creado en SonarQube o SonarCloud.  
· Token de análisis de SonarQube o SonarCloud.  
· Permisos para crear archivos dentro de `.github/workflows/`.  
· Conocimiento de qué validaciones deben bloquear el pipeline y cuáles solo deben generar advertencia.

---

## Actividad en clase

### 1. Recuperar los comandos de la actividad manual

El equipo debe identificar los comandos que ya ejecutó manualmente en la actividad anterior.

Debe completar:

| Validación | Comando manual utilizado | ¿Debe automatizarse? |
|---|---|---|
| Test unitarios |  |  |
| Coverage |  |  |
| SonarQube |  |  |
| Levantar sistema |  |  |
| Aceptación / mocks |  |  |
| E2E real |  |  |
| JMeter |  |  |

Ejemplos de comandos posibles:

```bash
npm test
```

```bash
mvn test
```

```bash
pytest --cov
```

```bash
dotnet test
```

```bash
jmeter -n -t quality-performance-test.jmx -l results.jtl -e -o report
```

---

### 2. Definir el flujo del pipeline

El equipo debe definir qué etapas tendrá el pipeline y en qué orden se ejecutarán.

Orden recomendado:

```text
1. Descargar código fuente.
2. Preparar lenguaje, runtime o SDK.
3. Instalar dependencias.
4. Ejecutar test unitarios.
5. Generar cobertura.
6. Ejecutar análisis con SonarQube o SonarCloud.
7. Levantar el sistema o ambiente de prueba.
8. Ejecutar pruebas de aceptación o E2E.
9. Ejecutar prueba de rendimiento con JMeter.
10. Publicar evidencias como artefactos del pipeline.
```

No todos los proyectos tendrán todas las etapas. Si una etapa no aplica, el equipo debe justificarlo.

---

### 3. Crear la estructura de GitHub Actions

Dentro del repositorio, el equipo debe crear la siguiente carpeta:

```text
.github/workflows/
```

Luego debe crear un archivo de workflow, por ejemplo:

```text
.github/workflows/quality-pipeline.yml
```

Estructura mínima:

```yaml
name: Quality Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  quality:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
```

El pipeline se ejecutará cuando existan cambios enviados a `main` o cuando se cree un Pull Request hacia `main`.

---

## Parte A: Automatización del análisis estático

### 4. Preparar el ambiente según la tecnología

El equipo debe configurar el runtime necesario para su proyecto.

Ejemplo para Node.js:

```yaml
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Install dependencies
        run: npm ci
```

Ejemplo para Java con Maven:

```yaml
      - name: Setup Java
        uses: actions/setup-java@v4
        with:
          distribution: 'temurin'
          java-version: '17'

      - name: Install dependencies
        run: mvn dependency:resolve
```

Ejemplo para Python:

```yaml
      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.12'

      - name: Install dependencies
        run: pip install -r requirements.txt
```

Ejemplo para .NET:

```yaml
      - name: Setup .NET
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: '8.0.x'

      - name: Restore dependencies
        run: dotnet restore
```

El equipo debe adaptar esta etapa al stack real de su artefacto.

---

### 5. Automatizar test unitarios

El pipeline debe ejecutar los test unitarios del proyecto.

Ejemplos:

```yaml
      - name: Run unit tests
        run: npm test
```

```yaml
      - name: Run unit tests
        run: mvn test
```

```yaml
      - name: Run unit tests
        run: pytest
```

```yaml
      - name: Run unit tests
        run: dotnet test
```

Si los test unitarios fallan, esta etapa normalmente debe bloquear el pipeline.

---

### 6. Automatizar cobertura

El pipeline debe generar evidencia de cobertura usando la herramienta correspondiente al proyecto.

Ejemplos:

```yaml
      - name: Run coverage
        run: npm test -- --coverage
```

```yaml
      - name: Run coverage
        run: mvn verify
```

```yaml
      - name: Run coverage
        run: pytest --cov --cov-report=xml
```

```yaml
      - name: Run coverage
        run: dotnet test /p:CollectCoverage=true
```

El equipo debe publicar el reporte de cobertura como artefacto si la herramienta genera archivos.

Ejemplo:

```yaml
      - name: Upload coverage report
        uses: actions/upload-artifact@v4
        with:
          name: coverage-report
          path: coverage/
```

La ruta debe adaptarse al proyecto. Algunos ejemplos comunes son `coverage/`, `target/site/jacoco/`, `htmlcov/` o `TestResults/`.

---

### 7. Configurar secretos para SonarQube o SonarCloud

El token de SonarQube no debe escribirse directamente en el workflow.

En GitHub, el equipo debe ingresar a:

```text
Settings > Secrets and variables > Actions > New repository secret
```

Debe crear, al menos:

| Secreto | Uso |
|---|---|
| `SONAR_TOKEN` | Token usado para autenticar el análisis |
| `SONAR_HOST_URL` | URL de SonarQube, si se usa instancia propia |

Ejemplo de valores:

```text
SONAR_HOST_URL=http://servidor-sonarqube:9000
SONAR_TOKEN=token_generado_en_sonarqube
```

Si se usa SonarCloud, normalmente se usa `SONAR_TOKEN` y la configuración del proyecto en SonarCloud.

---

### 8. Automatizar análisis con SonarQube o SonarCloud

El análisis puede ejecutarse con Maven, Gradle, SonarScanner CLI o acciones oficiales, según el stack.

Ejemplo genérico con SonarScanner:

```yaml
      - name: Run SonarQube analysis
        run: |
          npx sonar-scanner \
            -Dsonar.projectKey=calidad-ci-cd-demo \
            -Dsonar.sources=. \
            -Dsonar.host.url=${{ secrets.SONAR_HOST_URL }} \
            -Dsonar.token=${{ secrets.SONAR_TOKEN }}
```

Ejemplo con Maven:

```yaml
      - name: Run SonarQube analysis with Maven
        run: |
          mvn clean verify sonar:sonar \
            -Dsonar.projectKey=calidad-ci-cd-demo \
            -Dsonar.host.url=${{ secrets.SONAR_HOST_URL }} \
            -Dsonar.token=${{ secrets.SONAR_TOKEN }}
```

Ejemplo con SonarCloud Action:

```yaml
      - name: SonarCloud Scan
        uses: SonarSource/sonarqube-scan-action@v5
        env:
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
```

Para usar la acción oficial, el proyecto puede requerir un archivo `sonar-project.properties` en la raíz del repositorio.

Ejemplo:

```properties
sonar.projectKey=calidad-ci-cd-demo
sonar.organization=organizacion-sonarcloud
sonar.sources=.
sonar.sourceEncoding=UTF-8
```

El token debe mantenerse en GitHub Secrets, no en este archivo.

---

### 9. Decidir si el Quality Gate bloquea el pipeline

El equipo debe definir si un Quality Gate fallido bloqueará el pipeline.

Ejemplo usando una acción de Quality Gate:

```yaml
      - name: Check SonarQube Quality Gate
        uses: SonarSource/sonarqube-quality-gate-action@v1
        timeout-minutes: 5
        env:
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
```

Si el proyecto usa SonarQube propio, puede ser necesario configurar adicionalmente `SONAR_HOST_URL`.

El equipo debe justificar la decisión:

```text
El Quality Gate [sí/no] bloqueará el pipeline porque...
```

---

## Parte B: Automatización del análisis dinámico

### 10. Levantar el sistema en el pipeline

Para ejecutar pruebas dinámicas, el sistema debe estar disponible durante el pipeline.

Ejemplo para Node.js:

```yaml
      - name: Start application
        run: |
          npm run dev &
          sleep 10
```

Ejemplo para Java con Maven:

```yaml
      - name: Start application
        run: |
          mvn spring-boot:run &
          sleep 20
```

Ejemplo con Docker Compose:

```yaml
      - name: Start services
        run: docker compose up -d
```

Luego se debe validar que el sistema responda:

```yaml
      - name: Check application health
        run: curl --fail http://localhost:8080/health
```

La URL debe adaptarse al artefacto evaluado.

---

### 11. Automatizar pruebas de aceptación o E2E

Si el proyecto cuenta con pruebas automatizadas de aceptación o E2E, deben ejecutarse en esta etapa.

Ejemplos:

```yaml
      - name: Run E2E tests
        run: npm run test:e2e
```

```yaml
      - name: Run acceptance tests
        run: mvn test -Dtest=*AcceptanceTest
```

```yaml
      - name: Run API flow validation
        run: |
          curl --fail http://localhost:8080/api/productos
```

Si el proyecto no posee pruebas E2E automatizadas, el equipo puede automatizar al menos una validación HTTP representativa del flujo principal.

Ejemplo para crear y consultar un recurso:

```yaml
      - name: Validate main API flow
        run: |
          curl --fail -X POST http://localhost:8080/api/productos \
            -H "Content-Type: application/json" \
            -d '{"nombre":"Producto CI","precio":1000}'
          curl --fail http://localhost:8080/api/productos
```

El equipo debe indicar si esta prueba usa mocks o componentes reales.

---

### 12. Automatizar prueba de rendimiento con JMeter

El archivo `.jmx` creado en la actividad manual debe quedar dentro del repositorio, por ejemplo:

```text
performance/quality-performance-test.jmx
```

En GitHub Actions se puede ejecutar JMeter usando Docker:

```yaml
      - name: Run JMeter performance test
        run: |
          mkdir -p performance-results report
          docker run --rm \
            --network host \
            -v ${{ github.workspace }}/performance:/tests \
            -v ${{ github.workspace }}/performance-results:/results \
            justb4/jmeter:latest \
            -n -t /tests/quality-performance-test.jmx \
            -l /results/results.jtl \
            -e -o /results/report
```

Si `--network host` no funciona en el ambiente usado, el equipo debe adaptar la red o ejecutar JMeter desde una imagen que pueda alcanzar el servicio por nombre de contenedor.

Luego se deben publicar los resultados:

```yaml
      - name: Upload JMeter results
        uses: actions/upload-artifact@v4
        with:
          name: jmeter-results
          path: performance-results/
```

La prueba de rendimiento puede bloquear el pipeline si el porcentaje de error es alto o si los tiempos de respuesta superan el umbral definido por el equipo.

---

### 13. Definir umbrales de rendimiento

El equipo debe definir criterios mínimos para interpretar la prueba de JMeter.

Ejemplo:

| Métrica | Umbral propuesto | ¿Bloquea pipeline? |
|---|---:|---|
| Porcentaje de error | Mayor a 5% | Sí |
| Tiempo promedio | Mayor a 1000 ms | Advertencia |
| Percentil 90 | Mayor a 2000 ms | Advertencia |

Si el equipo desea bloquear el pipeline automáticamente por rendimiento, debe incorporar una validación sobre el archivo `results.jtl` o usar un plugin/herramienta que interprete resultados de JMeter.

---

## Parte C: Pipeline completo de referencia

### 14. Ejemplo base para proyecto Node.js

Este ejemplo debe adaptarse al proyecto real. No debe copiarse sin modificar comandos, puertos, rutas ni claves de SonarQube.

```yaml
name: Quality Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  quality:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Install dependencies
        run: npm ci

      - name: Run unit tests with coverage
        run: npm test -- --coverage

      - name: Run SonarQube analysis
        run: |
          npx sonar-scanner \
            -Dsonar.projectKey=calidad-ci-cd-demo \
            -Dsonar.sources=. \
            -Dsonar.host.url=${{ secrets.SONAR_HOST_URL }} \
            -Dsonar.token=${{ secrets.SONAR_TOKEN }}

      - name: Start application
        run: |
          npm run dev &
          sleep 10

      - name: Validate main endpoint
        run: curl --fail http://localhost:3000/

      - name: Run JMeter performance test
        run: |
          mkdir -p performance-results
          docker run --rm \
            --network host \
            -v ${{ github.workspace }}/performance:/tests \
            -v ${{ github.workspace }}/performance-results:/results \
            justb4/jmeter:latest \
            -n -t /tests/quality-performance-test.jmx \
            -l /results/results.jtl \
            -e -o /results/report

      - name: Upload coverage report
        uses: actions/upload-artifact@v4
        with:
          name: coverage-report
          path: coverage/

      - name: Upload JMeter results
        uses: actions/upload-artifact@v4
        with:
          name: jmeter-results
          path: performance-results/
```

---

### 15. Ejemplo base para proyecto Java con Maven

```yaml
name: Quality Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  quality:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup Java
        uses: actions/setup-java@v4
        with:
          distribution: 'temurin'
          java-version: '17'

      - name: Run tests, coverage and SonarQube analysis
        run: |
          mvn clean verify sonar:sonar \
            -Dsonar.projectKey=calidad-ci-cd-demo \
            -Dsonar.host.url=${{ secrets.SONAR_HOST_URL }} \
            -Dsonar.token=${{ secrets.SONAR_TOKEN }}

      - name: Start application
        run: |
          mvn spring-boot:run &
          sleep 20

      - name: Validate health endpoint
        run: curl --fail http://localhost:8080/health

      - name: Run JMeter performance test
        run: |
          mkdir -p performance-results
          docker run --rm \
            --network host \
            -v ${{ github.workspace }}/performance:/tests \
            -v ${{ github.workspace }}/performance-results:/results \
            justb4/jmeter:latest \
            -n -t /tests/quality-performance-test.jmx \
            -l /results/results.jtl \
            -e -o /results/report

      - name: Upload JMeter results
        uses: actions/upload-artifact@v4
        with:
          name: jmeter-results
          path: performance-results/
```

---

## Parte D: Evaluación del pipeline

### 16. Clasificar validaciones automatizadas

El equipo debe completar:

| Validación | Tipo de análisis | Etapa del pipeline | Resultado |
|---|---|---|---|
| Test unitarios | Estático |  |  |
| Coverage | Estático |  |  |
| SonarQube | Estático |  |  |
| Quality Gate | Estático |  |  |
| Aceptación / mocks | Dinámico |  |  |
| E2E real | Dinámico |  |  |
| Rendimiento con JMeter | Dinámico |  |  |

---

### 17. Definir criterios de bloqueo del pipeline

El equipo debe completar:

| Validación | ¿Bloquea pipeline? | ¿Genera advertencia? | Justificación |
|---|---|---|---|
| Test unitarios fallidos |  |  |  |
| Baja cobertura |  |  |  |
| Quality Gate fallido |  |  |  |
| Escenario de aceptación fallido |  |  |  |
| Test E2E fallido |  |  |  |
| Alto porcentaje de error en JMeter |  |  |  |
| Tiempo de respuesta elevado |  |  |  |

Ejemplo:

```text
Si el Quality Gate falla, el pipeline debe bloquearse porque indica que el artefacto no cumple las condiciones mínimas de calidad definidas para integrarse.
```

---

### 18. Analizar una ejecución real del pipeline

El equipo debe ejecutar el pipeline y revisar el resultado en GitHub Actions.

Debe registrar:

· Nombre del workflow ejecutado.  
· Rama o Pull Request que disparó la ejecución.  
· Etapas exitosas.  
· Etapas fallidas.  
· Evidencia de logs.  
· Evidencia de artefactos generados.  
· Resultado del análisis SonarQube o SonarCloud.  
· Resultado de JMeter, si aplica.

Si una etapa falla, el equipo debe indicar:

· Qué etapa falló.  
· Qué comando falló.  
· Qué causa técnica se identifica.  
· Qué corrección se propone.

---

### 19. Emitir conclusión técnica

El equipo debe emitir una conclusión final indicando si el artefacto puede avanzar dentro del flujo CI/CD automatizado.

Formato sugerido:

```text
El artefacto evaluado [sí/no] se encuentra en condiciones de avanzar dentro del pipeline CI/CD, debido a que...

Las validaciones automatizadas que resultaron exitosas fueron...

Las validaciones que fallaron o requieren mejora fueron...

Los criterios que deberían bloquear el pipeline son...

Antes de usar este pipeline en un ambiente real, se recomienda...
```

---

## Salida del lab

Los/las estudiantes deben poder mostrar su pantalla con:

· Archivo de workflow creado en `.github/workflows/`.  
· Ejecución del pipeline en GitHub Actions.  
· Evidencia de test unitarios automatizados.  
· Evidencia de cobertura automatizada.  
· Evidencia de análisis SonarQube o SonarCloud.  
· Estado del Quality Gate.  
· Evidencia de validación dinámica o E2E.  
· Evidencia de ejecución JMeter desde el pipeline, si aplica.  
· Artefactos generados por el pipeline.  
· Conclusión técnica del estado del artefacto.

---

## Evidencia requerida

· Archivo PPT con evidencias breves, que incluya:

· Nombre del artefacto evaluado.  
· Tecnología utilizada.  
· Diagrama o descripción simple del pipeline implementado.  
· Captura del archivo workflow.  
· Captura de ejecución en GitHub Actions.  
· Captura de test unitarios en el pipeline.  
· Captura o reporte de coverage.  
· Captura del dashboard de SonarQube o SonarCloud.  
· Captura del Quality Gate.  
· Evidencia de pruebas dinámicas o E2E.  
· Evidencia de JMeter y artefactos generados.  
· Tabla de criterios de bloqueo del pipeline.  
· Conclusión técnica indicando si el artefacto puede avanzar en CI/CD.

---

## Recomendación de estructura para el PPT

### Diapositiva 1: Portada

· Nombre de la actividad.  
· Nombre de integrantes.  
· Sección.  
· Fecha.  
· Artefacto evaluado.

### Diapositiva 2: Descripción del artefacto

· Tipo de sistema.  
· Tecnología utilizada.  
· Flujo funcional evaluado.  
· Comandos manuales base.

### Diapositiva 3: Diseño del pipeline

· Etapas implementadas.  
· Orden de ejecución.  
· Criterios de bloqueo.

### Diapositiva 4: Workflow GitHub Actions

· Archivo `.yml`.  
· Eventos que disparan el pipeline.  
· Jobs y steps principales.

### Diapositiva 5: Test y coverage

· Evidencia de ejecución.  
· Resultado obtenido.  
· Reporte generado.

### Diapositiva 6: SonarQube o SonarCloud

· Configuración de secretos.  
· Análisis ejecutado.  
· Estado del Quality Gate.

### Diapositiva 7: Validaciones dinámicas

· Ambiente levantado.  
· Pruebas de aceptación o E2E.  
· Resultado.

### Diapositiva 8: JMeter

· Archivo `.jmx`.  
· Ejecución en pipeline.  
· Artefactos generados.

### Diapositiva 9: Fallos y correcciones

· Etapas fallidas, si existieron.  
· Causa técnica.  
· Corrección propuesta.

### Diapositiva 10: Conclusión CI/CD

· ¿El artefacto puede avanzar?  
· ¿Qué bloquea el pipeline?  
· ¿Qué mejoras se recomiendan?

---

## Criterios sugeridos de evaluación

| Criterio | Puntaje |
|---|---:|
| Identifica correctamente comandos manuales a automatizar | 10 |
| Implementa workflow funcional en GitHub Actions | 20 |
| Automatiza test unitarios y cobertura | 15 |
| Automatiza análisis SonarQube o SonarCloud | 20 |
| Gestiona tokens y secretos de forma segura | 10 |
| Automatiza al menos una validación dinámica o E2E | 10 |
| Ejecuta o integra JMeter en el pipeline | 10 |
| Define criterios coherentes de bloqueo | 10 |
| Presenta evidencias claras y ordenadas | 5 |
| **Total** | **100** |

---

## Cierre de la actividad

Al finalizar esta actividad, las y los estudiantes habrán transformado controles manuales de calidad en etapas automatizadas de un pipeline CI/CD. Con esto podrán evaluar un artefacto de software de forma repetible cada vez que se realicen cambios en el repositorio, aplicando criterios técnicos para decidir si el artefacto puede avanzar o debe ser corregido.

---

2026
