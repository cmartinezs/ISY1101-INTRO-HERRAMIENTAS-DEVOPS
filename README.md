# ISY1101 - Introducción a Herramientas DevOps

Repositorio de documentación y actividades para la asignatura **ISY1101 - Introducción a Herramientas DevOps**.

El material está orientado a que las y los estudiantes comprendan cómo aplicar controles de calidad de software dentro de un flujo CI/CD, primero de forma manual y luego automatizada mediante un pipeline.

## Guías disponibles

### 1. Aplicación manual de herramientas de calidad

Archivo: `actividad_calidad_ci_cd_sonarqube_jmeter.md`

Esta guía aborda la ejecución manual de controles de calidad sobre un artefacto de software:

· Test unitarios.  
· Cobertura de pruebas.  
· Análisis con SonarQube.  
· Interpretación del Quality Gate.  
· Escenarios de aceptación con Gherkin.  
· Pruebas con mocks.  
· Validación E2E.  
· Pruebas de rendimiento con JMeter.

### 2. Automatización de controles de calidad en CI/CD

Archivo: `actividad_calidad_ci_cd_automatizada_github_actions.md`

Esta guía toma las validaciones realizadas manualmente y las lleva a un pipeline CI/CD usando GitHub Actions como plataforma de referencia.

Incluye:

· Estructura de workflows.  
· Ejecución automática de test y cobertura.  
· Integración con SonarQube o SonarCloud.  
· Uso de secretos como `SONAR_TOKEN`.  
· Validaciones dinámicas y E2E.  
· Ejecución de JMeter desde el pipeline.  
· Publicación de evidencias como artefactos.  
· Definición de criterios de bloqueo del pipeline.

## Enfoque de las actividades

Las guías son agnósticas a la tecnología del artefacto evaluado. Pueden aplicarse sobre APIs REST, aplicaciones web, backends, frontends, microservicios u otros sistemas desarrollados previamente.

Los comandos incluidos son ejemplos y deben adaptarse al lenguaje, framework y herramientas utilizadas por cada equipo.

## Evidencias esperadas

Cada actividad solicita evidencias breves, normalmente presentadas en un archivo PPT, incluyendo:

· Comandos ejecutados.  
· Resultados de pruebas.  
· Reportes de cobertura.  
· Métricas de SonarQube o SonarCloud.  
· Estado del Quality Gate.  
· Evidencias de pruebas E2E o dinámicas.  
· Resultados de JMeter.  
· Conclusión técnica sobre la aptitud del artefacto para CI/CD.

## Nota

Este repositorio es solo de documentación y actividades académicas. No contiene una aplicación ejecutable, dependencias, scripts de build ni configuración CI/CD propia del repositorio.
