# 4. Arquitectura y decisiones técnicas

El equipo debe demostrar que no solamente puede programar la solución, sino también explicar por qué la construyó de esa forma.

No se espera una arquitectura compleja. Para este diagnóstico, una solución simple y bien justificada es preferible a una arquitectura sobredimensionada.

---

## 4.1 Diagrama de arquitectura

Incluyan un diagrama sencillo que muestre, como mínimo:

```text
Usuario
  ↓
Frontend
  ↓ HTTP/JSON
Backend / API
  ↓
Base de datos
```

Pueden utilizar Mermaid, PlantUML, draw.io u otra herramienta conocida por el equipo.

El diagrama debe reflejar la implementación real.

---

## 4.2 Responsabilidades

Expliquen brevemente qué responsabilidad tiene cada componente:

### Frontend

- presentación;
- interacción con el usuario;
- consumo de la API;
- validaciones de experiencia de usuario que correspondan.

### Backend

- exposición de endpoints;
- validación de datos;
- reglas de negocio;
- coordinación con persistencia;
- respuestas HTTP y manejo de errores.

### Base de datos

- almacenamiento persistente;
- integridad básica de los datos.

---

## 4.3 Decisiones arquitectónicas obligatorias

El equipo deberá documentar como mínimo **5 decisiones**.

Cada decisión debe contener:

1. **Contexto:** qué problema o necesidad existía.
2. **Decisión:** qué alternativa eligió el equipo.
3. **Justificación:** por qué fue elegida.
4. **Consecuencias:** qué ventajas y costos introduce.

No se espera un ADR formal completo, pero pueden utilizar ese formato si ya lo conocen.

### Decisiones mínimas a documentar

#### DA-01 — Tecnología de frontend

¿Por qué utilizaron React, JavaScript vanilla u otra alternativa?

#### DA-02 — Tecnología de backend

¿Por qué utilizaron Node/Express, Spring Boot u otra alternativa conocida?

#### DA-03 — Persistencia

¿Por qué escogieron la base de datos utilizada?

#### DA-04 — Organización del backend

¿Cómo separaron rutas/controladores, lógica y acceso a datos? ¿Por qué?

#### DA-05 — Estrategia de contenerización

¿Qué componentes se ejecutan en contenedores y por qué?

---

## 4.4 Decisiones adicionales sugeridas

Si corresponde, pueden justificar también:

- estructura de carpetas;
- formato de respuestas de la API;
- códigos HTTP utilizados;
- estrategia de validación;
- manejo de variables de entorno;
- estrategia Git del equipo;
- inicialización de la base de datos;
- health checks;
- puertos utilizados;
- separación entre configuración de desarrollo y ejecución en Docker.

---

## 4.5 Restricción importante

No es válido justificar una decisión únicamente con frases como:

> "porque es mejor"

> "porque es más moderno"

> "porque lo pidió la actividad"

La justificación debe relacionar la decisión con el contexto del problema, las competencias del equipo, la simplicidad, la mantenibilidad, el tiempo disponible o alguna otra razón técnica defendible.

---

## Entregable

La documentación puede quedar, por ejemplo, en:

```text
docs/
├── arquitectura.md
└── decisiones.md
```

También puede integrarse en un único documento si mantiene una estructura clara.
