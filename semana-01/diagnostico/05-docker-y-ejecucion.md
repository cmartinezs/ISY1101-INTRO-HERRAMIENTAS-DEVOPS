# 5. Docker y ejecución del sistema

El diagnóstico debe permitir observar si el equipo comprende los conceptos básicos necesarios para ejecutar una aplicación fullstack mediante contenedores.

No se busca optimización avanzada de imágenes ni orquestación productiva. Se busca una solución reproducible y comprensible.

---

## 5.1 Componentes esperados

La solución debería considerar, como mínimo:

- frontend;
- backend/API;
- base de datos.

Cada equipo debe decidir qué componentes contenerizar y justificarlo.

Como referencia, una composición típica puede ser:

```text
Docker Compose
├── frontend
├── backend
└── database
```

---

## 5.2 Dockerfile

El equipo deberá incluir los Dockerfile necesarios para construir los componentes de aplicación.

Como mínimo deben ser capaces de explicar:

- qué imagen base utilizan;
- qué archivos copian;
- cuándo se instalan dependencias;
- qué puerto expone el servicio;
- qué comando inicia la aplicación.

No copien un Dockerfile desde Internet sin poder explicar sus instrucciones.

---

## 5.3 Docker Compose

La raíz del proyecto debe incluir un archivo `compose.yaml` o `docker-compose.yml` que permita iniciar la solución.

La ejecución esperada debe ser equivalente a:

```bash
docker compose up --build
```

El equipo debe documentar:

- servicios;
- puertos;
- variables de entorno necesarias;
- redes, si fueron declaradas explícitamente;
- volúmenes utilizados;
- dependencias entre servicios.

---

## 5.4 Persistencia

Los datos no deberían desaparecer simplemente por detener y volver a iniciar los contenedores.

Si la base de datos se ejecuta en Docker, utilicen un volumen persistente y expliquen su propósito.

El docente puede comprobarlo mediante una secuencia similar a:

```bash
docker compose up -d
# crear datos desde la aplicación
docker compose down
docker compose up -d
# verificar que los datos continúan disponibles
```

El uso de `docker compose down -v` sí puede eliminar los volúmenes y no forma parte de esta comprobación de persistencia.

---

## 5.5 Configuración

No deben versionarse secretos ni contraseñas personales.

Si utilizan variables de entorno, agreguen un archivo de ejemplo, por ejemplo:

```text
.env.example
```

La aplicación debe poder configurarse sin modificar código fuente para cambiar valores como:

- host de base de datos;
- puerto;
- nombre de base de datos;
- credenciales de desarrollo;
- URL del backend consumida por el frontend, cuando corresponda.

---

## 5.6 Verificaciones mínimas

Antes de considerar terminado el diagnóstico, el equipo deberá comprobar:

1. Las imágenes se construyen sin error.
2. Los contenedores inician correctamente.
3. El frontend puede comunicarse con el backend.
4. El backend puede comunicarse con la base de datos.
5. El CRUD funciona utilizando la solución levantada en Docker.
6. Las funcionalidades adicionales también funcionan.
7. Un integrante puede clonar el repositorio en un entorno limpio y seguir el README para ejecutar la aplicación.

---

## 5.7 Conceptos que cada integrante debe poder explicar

Al finalizar el trabajo, cualquier integrante debería poder responder, al menos en términos básicos:

- diferencia entre imagen y contenedor;
- propósito de un Dockerfile;
- propósito de Docker Compose;
- diferencia entre `build` y `up`;
- por qué un volumen puede ser necesario;
- cómo se comunican los servicios;
- qué problema resuelven las variables de entorno;
- qué ocurre cuando un contenedor se elimina.

Estas ideas también serán retomadas en el cuestionario individual.
