# Guía: Aplicación manual de herramientas de calidad en un flujo CI/CD

---

| Sigla/Asignatura | Semana Disponible EFT | Experiencia de Aprendizaje |
|---|---:|---|
| ISY1101 – Introducción a Herramientas DevOps | 17 | EA 2 |

| Tiempo | Modalidad de Trabajo | Indicadores de Logro |
|---|---|---|
| 5 hrs | Presencial | IL 2.3 |

---

## Resultados de aprendizaje

· **RA2** Aplica herramientas de calidad de software dentro de un flujo de desarrollo, evaluando el estado de un artefacto mediante análisis estático y dinámico para determinar su aptitud de integración en un proceso CI/CD.

---

## Contenidos

Aplicar herramientas de calidad de software dentro del flujo de CI/CD, diferenciando controles de análisis estático y análisis dinámico. La actividad considera la ejecución manual de pruebas unitarias, revisión de cobertura, análisis de calidad con SonarQube, definición de pruebas de aceptación con Gherkin, validación E2E del sistema y ejecución de pruebas de rendimiento con JMeter.

---

## Actividades

### Actividad: Aplicación manual de herramientas de calidad en un flujo CI/CD

En esta actividad, las y los estudiantes deberán evaluar la calidad de un artefacto de software utilizando herramientas y prácticas asociadas a un flujo de CI/CD.

La actividad es **agnóstica a la tecnología del artefacto de software**, por lo que puede ser aplicada sobre una API REST, aplicación web, backend, frontend, microservicio u otro sistema desarrollado previamente, siempre que permita ejecutar pruebas, levantar el sistema y validar su comportamiento.

Primero se trabajará con controles de **análisis estático**, es decir, revisiones que se aplican principalmente sobre el código fuente sin necesidad de ejecutar completamente el sistema. Luego se trabajará con controles de **análisis dinámico**, donde el sistema debe estar ejecutándose para validar comportamiento, interoperabilidad y rendimiento.

Como parte del proceso, las y los estudiantes deberán ejecutar las herramientas de forma manual, interpretar los resultados obtenidos y determinar si el artefacto evaluado estaría en condiciones de avanzar dentro de un flujo CI/CD.

Esta actividad prepara una actividad posterior donde las mismas validaciones deberán ser incorporadas de forma automatizada en un pipeline.

---

## Objetivo

Los estudiantes deberán aplicar herramientas de calidad de software de forma manual sobre un artefacto de software, identificando controles de análisis estático y dinámico, interpretando sus resultados y definiendo criterios técnicos que permitan decidir si el artefacto puede avanzar o no dentro de un flujo CI/CD.

---

## Puntos a recalcar

· El análisis estático permite revisar aspectos del código sin ejecutar completamente el sistema.  
· Los test unitarios, la cobertura y SonarQube forman parte del análisis estático.  
· El análisis dinámico requiere ejecutar el sistema o parte de él.  
· Los test de aceptación, test E2E y pruebas de rendimiento forman parte del análisis dinámico.  
· Las herramientas no solo se ejecutan: sus resultados deben ser interpretados técnicamente.  
· En un flujo CI/CD, algunas validaciones pueden bloquear el pipeline y otras solo generar advertencias.  
· Antes de automatizar una herramienta en CI/CD, es importante comprender cómo se ejecuta manualmente.  
· La actividad no depende de un lenguaje o framework específico, sino del proceso de validación de calidad aplicado al artefacto.

---

## Herramientas sugeridas

Las herramientas pueden variar según la tecnología del proyecto, pero se recomienda utilizar:

· Herramienta de test unitario propia del stack del proyecto.  
· Herramienta de cobertura propia del stack del proyecto.  
· SonarQube para análisis de calidad de código.  
· SonarScanner, Maven, Gradle, npm u otra herramienta compatible con el proyecto.  
· Gherkin para describir escenarios de aceptación.  
· Herramienta de pruebas E2E o cliente HTTP para validar flujos reales.  
· JMeter para pruebas de rendimiento.  
· Navegador web, terminal y editor de código.

---

## Prerrequisitos

Antes de iniciar la actividad, cada equipo debe contar con:

· Un artefacto de software funcional que pueda ejecutarse localmente o en un ambiente de prueba.  
· Acceso al código fuente del artefacto evaluado.  
· Comandos identificados para ejecutar pruebas unitarias y generar cobertura, según el stack del proyecto.  
· Docker instalado, si se utilizará SonarQube local mediante contenedor.  
· SonarScanner CLI, Maven, Gradle, npm, dotnet u otra herramienta compatible para enviar el análisis a SonarQube.  
· JMeter instalado para crear y ejecutar el plan de pruebas de rendimiento.  
· Permisos para generar evidencias, capturas de pantalla y reportes.

La actividad se ejecuta de forma manual. No se debe construir todavía el pipeline CI/CD automatizado; esa automatización corresponde a una actividad posterior.

---

## Actividad en clase

### 1. Seleccionar el artefacto de software a evaluar

Cada equipo deberá seleccionar un artefacto de software funcional para la actividad.

Puede ser:

· Una API REST.  
· Una aplicación web.  
· Un backend.  
· Un frontend.  
· Un microservicio.  
· Un sistema multicapa.  
· Un proyecto entregado por el/la docente.

El artefacto debe permitir, como mínimo:

· Ejecutar pruebas unitarias.  
· Generar o revisar cobertura.  
· Ser analizado por SonarQube.  
· Ser ejecutado localmente o en un ambiente de prueba.  
· Permitir al menos un flujo funcional completo para pruebas E2E.  
· Permitir al menos una petición o acción repetible para pruebas de rendimiento.

---

### 2. Identificar el flujo funcional principal del sistema

Antes de ejecutar herramientas, el equipo debe identificar un flujo funcional que será usado durante la actividad.

Ejemplos:

· Crear, consultar, actualizar y eliminar un recurso.  
· Registrar un usuario e iniciar sesión.  
· Crear una solicitud y consultar su estado.  
· Agregar un producto a un carrito y confirmar la operación.  
· Enviar un formulario y revisar el resultado.  
· Consultar información desde una API.

El equipo debe registrar:

```text
Nombre del flujo:
Descripción breve:
Entrada esperada:
Resultado esperado:
Componentes involucrados:
Dependencias externas, si existen:
```

---

## Parte A: Análisis estático

### 3. Ejecutar test unitarios

El equipo debe ejecutar los test unitarios existentes en el proyecto.

El comando dependerá de la tecnología utilizada.

Ejemplos:

```bash
mvn test
```

```bash
gradle test
```

```bash
npm test
```

```bash
pytest
```

```bash
dotnet test
```

El equipo debe registrar:

· Comando utilizado.  
· Cantidad de test ejecutados.  
· Cantidad de test exitosos.  
· Cantidad de test fallidos.  
· Evidencia de la ejecución en consola o reporte generado.

Si existen test fallidos, el equipo debe indicar:

· Qué prueba falló.  
· Qué funcionalidad estaba validando.  
· Posible causa del error.  
· Si el artefacto debería avanzar o no en el flujo CI/CD.

---

### 4. Revisar cobertura de pruebas

El equipo debe generar o revisar la cobertura del proyecto.

El comando dependerá de la tecnología utilizada.

Ejemplos:

```bash
mvn verify
```

```bash
gradle test jacocoTestReport
```

```bash
npm test -- --coverage
```

```bash
pytest --cov
```

```bash
dotnet test /p:CollectCoverage=true
```

El equipo debe registrar:

· Herramienta utilizada para cobertura.  
· Porcentaje de cobertura total.  
· Archivos, clases, módulos o componentes con menor cobertura.  
· Funcionalidades críticas que no están cubiertas.  
· Evidencia del reporte generado.

El equipo debe responder:

```text
¿La cobertura actual es suficiente para confiar en el artefacto dentro de un flujo CI/CD? Justifique.
```

---

### 5. Levantar SonarQube

El equipo deberá disponer de una instancia de SonarQube local o proporcionada por el/la docente.

Ejemplo utilizando Docker:

```bash
docker run -d --name sonarqube -p 9000:9000 sonarqube:lts-community
```

Luego ingresar desde el navegador a:

```text
http://localhost:9000
```

Credenciales iniciales habituales:

```text
Usuario: admin
Contraseña: admin
```

Después del primer ingreso, SonarQube puede solicitar el cambio de contraseña.

El equipo debe validar:

· Que SonarQube esté ejecutándose correctamente.  
· Que se pueda acceder desde el navegador.  
· Que se pueda crear o visualizar un proyecto de análisis.

---

### 6. Crear proyecto en SonarQube

Dentro de SonarQube, el equipo debe:

1. Crear un nuevo proyecto.
2. Asignar un nombre representativo.
3. Definir una clave de proyecto.
4. Generar un token de análisis.
5. Guardar temporalmente el token para ejecutar el análisis.

Ejemplo de nombre:

```text
calidad-ci-cd-demo
```

Ejemplo de project key:

```text
calidad-ci-cd-demo
```

---

### 7. Ejecutar análisis de código con SonarQube

El equipo debe ejecutar el análisis desde la terminal del proyecto.

El comando dependerá de la tecnología utilizada.

Antes de ejecutar el análisis, el equipo debe identificar qué herramienta usará para enviar el código hacia SonarQube.

#### ¿Qué es SonarScanner?

SonarScanner es una herramienta de línea de comandos que toma el código fuente de un proyecto, lee su configuración de análisis y envía los resultados a una instancia de SonarQube.

Se utiliza especialmente cuando el proyecto no ejecuta el análisis directamente mediante Maven, Gradle u otra herramienta integrada del stack.

SonarScanner permite indicar, entre otros datos:

· Clave del proyecto en SonarQube.  
· Carpeta donde se encuentra el código fuente.  
· URL de la instancia de SonarQube.  
· Token de autenticación.  
· Rutas de reportes de cobertura, si existen.

#### Instalación de SonarScanner

La instalación puede variar según el sistema operativo. Una alternativa común es descargar SonarScanner CLI desde el sitio oficial de SonarSource:

```text
https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner/
```

Pasos generales:

1. Descargar SonarScanner CLI para el sistema operativo utilizado.
2. Descomprimir el archivo descargado.
3. Agregar la carpeta `bin` de SonarScanner a la variable de entorno `PATH`.
4. Abrir una nueva terminal.
5. Validar la instalación con:

```bash
sonar-scanner --version
```

Si el comando muestra la versión instalada, SonarScanner está disponible desde la terminal.

En proyectos Node.js también puede ejecutarse sin instalación global usando `npx`, por ejemplo:

```bash
npx sonar-scanner --version
```

#### Configuración de SonarScanner

SonarScanner puede configurarse de dos formas principales.

Opción 1: Pasar los parámetros directamente por comando:

```bash
sonar-scanner \
  -Dsonar.projectKey=calidad-ci-cd-demo \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=TOKEN_GENERADO
```

Opción 2: Crear un archivo `sonar-project.properties` en la raíz del proyecto evaluado:

```properties
sonar.projectKey=calidad-ci-cd-demo
sonar.sources=.
sonar.host.url=http://localhost:9000
sonar.token=TOKEN_GENERADO
```

Luego ejecutar:

```bash
sonar-scanner
```

En un proyecto real o en un pipeline CI/CD, el token no debe quedar escrito directamente en el archivo `sonar-project.properties`. Debe definirse como variable de entorno o secreto del pipeline.

Ejemplo con Maven:

```bash
mvn clean verify sonar:sonar \
  -Dsonar.projectKey=calidad-ci-cd-demo \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=TOKEN_GENERADO
```

Ejemplo con SonarScanner:

```bash
sonar-scanner \
  -Dsonar.projectKey=calidad-ci-cd-demo \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=TOKEN_GENERADO
```

Para proyectos desarrollados con otras tecnologías, el análisis debe adaptarse al stack utilizado. Lo importante es identificar qué herramienta permite generar pruebas, cobertura y análisis de código para ese proyecto.

Ejemplos orientativos:

```bash
gradle test jacocoTestReport sonarqube \
  -Dsonar.projectKey=calidad-ci-cd-demo \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=TOKEN_GENERADO
```

```bash
npm test -- --coverage
npx sonar-scanner \
  -Dsonar.projectKey=calidad-ci-cd-demo \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=TOKEN_GENERADO
```

```bash
dotnet sonarscanner begin /k:"calidad-ci-cd-demo" /d:sonar.host.url="http://localhost:9000" /d:sonar.token="TOKEN_GENERADO"
dotnet build
dotnet test
dotnet sonarscanner end /d:sonar.token="TOKEN_GENERADO"
```

```bash
pytest --cov
sonar-scanner \
  -Dsonar.projectKey=calidad-ci-cd-demo \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=TOKEN_GENERADO
```

En esta actividad el análisis se ejecuta manualmente para comprender el proceso. En una actividad posterior, estos mismos pasos deberán trasladarse a un pipeline CI/CD, usando variables seguras para valores como `sonar.token`, ejecutando primero las pruebas y la cobertura, y luego publicando el análisis hacia SonarQube.

El equipo debe validar:

· Que el análisis finalice correctamente.  
· Que el proyecto aparezca en SonarQube.  
· Que existan métricas visibles en el dashboard del proyecto.
· Que el Quality Gate tenga un estado visible para poder interpretarlo.

---

### 8. Analizar resultados de SonarQube

El equipo debe revisar las siguientes secciones:

· Bugs.  
· Vulnerabilidades.  
· Security Hotspots.  
· Code Smells.  
· Duplicación.  
· Mantenibilidad.  
· Confiabilidad.  
· Seguridad.  
· Deuda técnica.  
· Quality Gate.

El equipo debe completar la siguiente tabla:

| Métrica | Resultado obtenido | Observación |
|---|---:|---|
| Bugs |  |  |
| Vulnerabilidades |  |  |
| Security Hotspots |  |  |
| Code Smells |  |  |
| Duplicación |  |  |
| Deuda técnica |  |  |
| Estado del Quality Gate |  |  |

Luego debe responder:

```text
¿El análisis de SonarQube permite que el artefacto avance dentro de un flujo CI/CD? Justifique.
```

Si el Quality Gate falla, el equipo debe indicar qué condición provocó el fallo y si esa condición debería bloquear un pipeline automatizado en la siguiente actividad.

---

## Parte B: Análisis dinámico

### 9. Levantar el sistema en ambiente local o de prueba

El equipo debe ejecutar el artefacto en un ambiente donde pueda ser probado.

Puede ser:

· Localhost.  
· Docker.  
· Docker Compose.  
· Máquina virtual.  
· Instancia cloud.  
· Ambiente de pruebas proporcionado por el/la docente.

El equipo debe registrar:

· Comando utilizado para levantar el sistema.  
· URL base del sistema.  
· Puerto utilizado.  
· Dependencias necesarias.  
· Evidencia de que el sistema está disponible.

Ejemplos:

```bash
docker compose up -d
```

```bash
npm run dev
```

```bash
mvn spring-boot:run
```

```bash
python app.py
```

```bash
dotnet run
```

---

### 10. Definir test de aceptación con Gherkin

El equipo debe definir al menos dos escenarios de aceptación utilizando Gherkin.

Los escenarios deben representar reglas de negocio o comportamiento esperado del sistema.

Ejemplo genérico:

```gherkin
Feature: Operación principal del sistema

Scenario: Ejecutar operación válida
  Given el sistema se encuentra disponible
  And existe información válida para realizar la operación
  When el usuario ejecuta la operación principal
  Then el sistema responde exitosamente
  And el resultado queda disponible para consulta posterior
```

Ejemplo con error esperado:

```gherkin
Feature: Validación de reglas del sistema

Scenario: Rechazar operación con datos inválidos
  Given el sistema se encuentra disponible
  And el usuario ingresa datos inválidos
  When el usuario intenta ejecutar la operación
  Then el sistema rechaza la solicitud
  And se informa un mensaje de error adecuado
```

El equipo debe indicar:

· Qué flujo representa cada escenario.  
· Qué precondiciones necesita.  
· Qué resultado se espera.  
· Qué dependencia externa debería ser simulada con mock, si corresponde.

---

### 11. Ejecutar o simular pruebas de aceptación con mocks

El equipo debe ejecutar o documentar la validación de los escenarios de aceptación.

Cuando el sistema dependa de servicios externos, el equipo debe utilizar mocks o simulaciones.

Ejemplos de dependencias que pueden ser simuladas:

· Servicio de correo.  
· Servicio de pago.  
· API externa.  
· Servicio de autenticación.  
· Base de datos temporal o en memoria.  
· Respuesta fija de un servicio no disponible.

El equipo debe registrar:

· Qué dependencia fue simulada.  
· Por qué se simuló.  
· Qué respuesta entrega el mock.  
· Resultado de la prueba de aceptación.

El equipo debe responder:

```text
¿Qué ventaja entrega el uso de mocks en una prueba de aceptación dentro de un flujo CI/CD?
```

---

### 12. Ejecutar prueba E2E con interoperabilidad real

El equipo debe ejecutar al menos un flujo completo de extremo a extremo utilizando el sistema real en el ambiente definido.

A diferencia de la prueba con mocks, en esta etapa se deben usar los componentes reales disponibles en el ambiente de prueba.

El equipo debe validar:

· Que el sistema permita iniciar el flujo.  
· Que los componentes se comuniquen correctamente.  
· Que los datos se procesen correctamente.  
· Que exista una respuesta verificable.  
· Que el resultado final coincida con lo esperado.

Ejemplo para una API REST:

```text
1. Crear un recurso.
2. Consultar el recurso creado.
3. Actualizar el recurso.
4. Consultar nuevamente el recurso.
5. Eliminar el recurso.
6. Verificar que ya no exista.
```

Ejemplo para una aplicación web:

```text
1. Ingresar a la aplicación.
2. Completar formulario.
3. Enviar información.
4. Verificar mensaje de éxito.
5. Consultar información registrada.
6. Confirmar que el resultado sea correcto.
```

El equipo debe registrar:

· Pasos ejecutados.  
· Datos utilizados.  
· Resultado esperado.  
· Resultado obtenido.  
· Evidencia de ejecución.

---

### 13. Crear plan de pruebas en JMeter

El equipo debe abrir JMeter y crear un plan de pruebas para evaluar rendimiento básico.

Antes de configurar la prueba, el equipo debe confirmar que el sistema evaluado se encuentre ejecutándose y que la URL o endpoint seleccionado responda correctamente desde el navegador, cliente HTTP o terminal.

Estructura mínima:

```text
Test Plan
└── Thread Group
    ├── HTTP Request
    ├── View Results Tree
    └── Summary Report
```

El equipo debe configurar el Thread Group con valores iniciales:

```text
Number of Threads (users): 10
Ramp-up period: 10 segundos
Loop Count: 5
```

Luego debe configurar una petición o acción representativa del sistema.

Ejemplo para API REST:

```text
Protocol: http
Server Name or IP: localhost
Port Number: 8080
Method: GET
Path: /recurso-principal
```

Ejemplo para aplicación web:

```text
Protocol: http
Server Name or IP: localhost
Port Number: 3000
Method: GET
Path: /
```

El equipo debe guardar el plan con un nombre representativo:

```text
quality-performance-test.jmx
```

---

### 14. Ejecutar prueba de rendimiento desde JMeter

Primero, el equipo puede ejecutar la prueba desde la interfaz gráfica para validar que esté bien configurada.

Ejemplo de configuración para una API REST ejecutándose en `http://localhost:8080`:

```text
Thread Group
Number of Threads (users): 10
Ramp-up period: 10
Loop Count: 5

HTTP Request
Protocol: http
Server Name or IP: localhost
Port Number: 8080
Method: GET
Path: /api/productos

Listeners
View Results Tree
Summary Report
```

Ejemplo de configuración para una aplicación web ejecutándose en `http://localhost:3000`:

```text
Thread Group
Number of Threads (users): 10
Ramp-up period: 10
Loop Count: 5

HTTP Request
Protocol: http
Server Name or IP: localhost
Port Number: 3000
Method: GET
Path: /

Listeners
View Results Tree
Summary Report
```

Para configurar la prueba en la interfaz de JMeter:

1. Abrir JMeter.
2. Crear un `Thread Group` dentro del `Test Plan`.
3. Configurar usuarios, ramp-up e iteraciones.
4. Agregar un `HTTP Request` dentro del `Thread Group`.
5. Configurar protocolo, servidor, puerto, método HTTP y ruta.
6. Agregar los listeners `View Results Tree` y `Summary Report`.
7. Ejecutar la prueba desde el botón de inicio.
8. Revisar si las respuestas son exitosas antes de ejecutar en modo consola.

Debe revisar:

· Que las peticiones respondan correctamente.  
· Que no existan errores de conexión.  
· Que el endpoint o recurso probado sea el correcto.  
· Que se obtengan métricas en Summary Report.

Luego, debe ejecutar la prueba en modo consola o non-GUI.

Ejemplo:

```bash
jmeter -n -t quality-performance-test.jmx -l results.jtl -e -o report
```

El equipo debe validar:

· Que se genere el archivo `results.jtl`.  
· Que se genere la carpeta `report`.  
· Que el reporte HTML pueda abrirse desde el navegador.

---

### 15. Analizar resultados de JMeter

El equipo debe revisar las métricas obtenidas.

Debe completar la siguiente tabla:

| Métrica | Resultado obtenido | Observación |
|---|---:|---|
| Usuarios concurrentes |  |  |
| Ramp-up |  |  |
| Iteraciones |  |  |
| Tiempo promedio de respuesta |  |  |
| Tiempo mínimo |  |  |
| Tiempo máximo |  |  |
| Throughput |  |  |
| Porcentaje de error |  |  |
| Percentil 90 |  |  |

El equipo debe responder:

```text
¿El sistema mantiene un comportamiento aceptable bajo la carga aplicada? Justifique.
```

---

## Parte C: Evaluación del flujo CI/CD

### 16. Clasificar las validaciones realizadas

El equipo debe clasificar cada validación como parte de análisis estático o dinámico.

| Validación | Tipo de análisis | Herramienta usada | Resultado |
|---|---|---|---|
| Test unitarios | Estático |  |  |
| Coverage | Estático |  |  |
| SonarQube | Estático |  |  |
| Gherkin / aceptación con mocks | Dinámico |  |  |
| E2E real | Dinámico |  |  |
| Rendimiento con JMeter | Dinámico |  |  |

---

### 17. Definir criterios para un futuro pipeline

El equipo debe proponer qué reglas deberían usarse en una futura automatización CI/CD.

Estos criterios serán usados como base para decidir qué etapas del pipeline deberían bloquear el avance del artefacto y cuáles deberían quedar solo como advertencia.

Debe completar:

| Validación | ¿Bloquea pipeline? | ¿Genera advertencia? | Justificación |
|---|---|---|---|
| Test unitarios fallidos |  |  |  |
| Baja cobertura |  |  |  |
| Quality Gate fallido |  |  |  |
| Escenario Gherkin fallido |  |  |  |
| Test E2E fallido |  |  |  |
| Alto porcentaje de error en JMeter |  |  |  |
| Tiempo de respuesta elevado |  |  |  |

Ejemplo de criterio:

```text
Si existen test unitarios fallidos, el pipeline debe bloquearse porque no se puede asegurar que el comportamiento interno del sistema sea correcto.
```

El equipo también debe indicar qué datos tendrían que configurarse como variables o secretos del pipeline, por ejemplo `sonar.token`, URL de SonarQube, credenciales de servicios de prueba o valores de ambiente.

---

### 18. Emitir conclusión técnica

El equipo debe emitir una conclusión final indicando si el artefacto está o no en condiciones de avanzar hacia CI/CD.

Debe considerar:

· Resultado de test unitarios.  
· Nivel de cobertura.  
· Estado del Quality Gate.  
· Resultado de escenarios de aceptación.  
· Resultado de pruebas E2E.  
· Resultado de pruebas de rendimiento.  
· Riesgos detectados.

Formato sugerido:

```text
El artefacto evaluado [sí/no] se encuentra en condiciones de avanzar dentro de un flujo CI/CD, debido a que...

Las principales fortalezas identificadas fueron...

Los principales riesgos detectados fueron...

Antes de automatizar este proceso, se recomienda...
```

---

## Salida del lab

Los/las estudiantes deben poder mostrar su pantalla con:

· Ejecución de test unitarios.  
· Reporte o resultado de coverage.  
· Proyecto analizado en SonarQube.  
· Estado del Quality Gate.  
· Escenarios Gherkin definidos.  
· Evidencia de prueba de aceptación con mocks.  
· Evidencia de flujo E2E real.  
· Plan de prueba creado en JMeter.  
· Reporte o resumen de resultados de JMeter.  
· Conclusión técnica del estado del artefacto.

---

## Evidencia requerida

· Archivo PPT con evidencias breves, que incluya:

· Nombre del artefacto evaluado.  
· Descripción del flujo funcional principal.  
· Captura de ejecución de test unitarios.  
· Captura o reporte de coverage.  
· Captura del dashboard de SonarQube.  
· Captura del estado del Quality Gate.  
· Tabla con hallazgos principales de SonarQube.  
· Escenarios Gherkin definidos.  
· Evidencia de uso de mocks en prueba de aceptación.  
· Evidencia de ejecución E2E.  
· Captura del plan de pruebas en JMeter.  
· Captura del Summary Report o reporte HTML de JMeter.  
· Tabla con métricas de rendimiento.  
· Conclusión técnica indicando si el artefacto está apto o no para CI/CD.  
· Propuesta de qué controles deberían bloquear un pipeline automatizado.
· Identificación de comandos que luego podrían automatizarse en el pipeline CI/CD.

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
· URL o forma de ejecución.

### Diapositiva 3: Test unitarios

· Comando utilizado.  
· Resultado obtenido.  
· Evidencia.

### Diapositiva 4: Coverage

· Herramienta utilizada.  
· Porcentaje obtenido.  
· Componentes con baja cobertura.

### Diapositiva 5: SonarQube

· Captura del dashboard.  
· Métricas principales.  
· Estado del Quality Gate.

### Diapositiva 6: Gherkin y aceptación

· Escenarios definidos.  
· Dependencias simuladas con mocks.  
· Resultado.

### Diapositiva 7: Test E2E

· Flujo ejecutado.  
· Evidencia.  
· Resultado esperado versus resultado obtenido.

### Diapositiva 8: JMeter

· Configuración de usuarios, ramp-up e iteraciones.  
· Endpoint o recurso evaluado.  
· Evidencia del plan.

### Diapositiva 9: Resultados de rendimiento

· Tiempo promedio.  
· Throughput.  
· Porcentaje de error.  
· Percentil 90.  
· Evidencia del reporte.

### Diapositiva 10: Conclusión CI/CD

· ¿El artefacto está apto para CI/CD?  
· ¿Qué controles deberían bloquear el pipeline?  
· ¿Qué mejoras se recomiendan?

---

## Criterios sugeridos de evaluación

| Criterio | Puntaje |
|---|---:|
| Identifica correctamente el artefacto y flujo funcional evaluado | 10 |
| Ejecuta e interpreta test unitarios | 10 |
| Ejecuta e interpreta cobertura | 10 |
| Ejecuta e interpreta SonarQube | 20 |
| Define correctamente escenarios Gherkin | 10 |
| Diferencia pruebas con mocks y pruebas E2E reales | 10 |
| Ejecuta e interpreta prueba de rendimiento con JMeter | 15 |
| Propone criterios coherentes para CI/CD | 10 |
| Presenta evidencias claras y ordenadas | 5 |
| **Total** | **100** |

---

## Cierre de la actividad

Al finalizar esta actividad, las y los estudiantes habrán aplicado manualmente herramientas y prácticas de calidad que forman parte de un flujo CI/CD. La siguiente etapa consistirá en automatizar estas validaciones dentro de un pipeline, de modo que el sistema pueda ser evaluado automáticamente cada vez que se realicen cambios en el código fuente.

---

2026
