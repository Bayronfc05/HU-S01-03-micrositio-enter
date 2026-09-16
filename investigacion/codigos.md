# Experimento X6 — Simulación y Captura de Códigos de Estado HTTP

**Dominio analizado:** `bayronfc05.github.io`
**Herramienta utilizada:** DevTools (pestaña *Network*)

## Resumen

Para este experimento me propuse provocar y capturar distintos códigos de estado HTTP usando las herramientas de desarrollador del navegador. Quería entender no solo *qué* código devuelve el servidor en cada caso, sino *quién* es realmente el responsable de esa respuesta: el servidor de origen, la CDN, mi propia caché local, o el navegador actuando por su cuenta. En total probé seis escenarios: `200`, `301`, `307`, `304`, `404` y `401`.

## 1. Evidencia y capturas de DevTools

### 1.1. Código `200 OK` — Solicitud exitosa

Empecé por lo más simple: entrar al micrositio con una recarga limpia (`Ctrl + F5`) mientras tenía la pestaña *Network* abierta, para asegurarme de que la petición viajara realmente hasta el servidor sin usar caché.

- **URL:** `https://bayronfc05.github.io/HU-S01-03-micrositio-enter/`
- **Método:** `GET`
- **Resultado:** `Status: 200 OK`, con la entrega completa del documento HTML.

### 1.2. Código `301 Moved Permanently` — Redirección real del servidor

Aquí quería obligar al servidor a redirigirme de verdad, no que el navegador lo resolviera por su cuenta. Por eso abrí una pestaña InPrivate con *Preserve log* activado y entré por `http://` a propósito, evitando cualquier historial HSTS que pudiera interferir.

- **URL:** `http://bayronfc05.github.io/HU-S01-03-micrositio-enter/`
- **Método:** `GET`
- **Resultado:** `Status: 301 Moved Permanently`, con `Location: https://bayronfc05.github.io/HU-S01-03-micrositio-enter/`.

### 1.3. Código `307 Internal Redirect` — Redirección local por HSTS

Después probé lo contrario: entrar por `http://` pero desde mi sesión normal del navegador, la que ya había visitado el sitio antes. En vez de una petición real a GitHub, el navegador interceptó la solicitud él mismo.

- **URL:** `http://bayronfc05.github.io/HU-S01-03-micrositio-enter/`
- **Método:** `GET`
- **Resultado:** `Status: 307 Internal Redirect`, con `Non-Authoritative-Reason: HSTS`.

### 1.4. Código `304 Not Modified` — Validación condicional / caché

Con el sitio ya cargado una vez, simplemente presioné `F5` dejando la caché del navegador habilitada, para ver cómo se comportaba la validación del recurso.

- **URL:** `https://bayronfc05.github.io/HU-S01-03-micrositio-enter/`
- **Método:** `GET`
- **Resultado:** `Status: 304 Not Modified`, con `Size: memory cache` / `disk cache`.

### 1.5. Código `404 Not Found` — Recurso inexistente

Para forzar un error del cliente, inventé una ruta que sabía que no existía en el repositorio.

- **URL:** `https://bayronfc05.github.io/HU-S01-03-micrositio-enter/pagina-que-no-existe`
- **Método:** `GET`
- **Resultado:** `Status: 404 Not Found`, con la página de error personalizada de GitHub.

### 1.6. Código `401 Unauthorized` — Autenticación requerida

Por último quise probar un caso donde el problema no fuera "el recurso no existe" sino "no tengo permiso para verlo". Consulté directamente la API REST de GitHub sin enviar ningún token ni credencial.

- **URL:** `https://api.github.com/user`
- **Método:** `GET`
- **Resultado:** `Status: 401 Unauthorized`, con el payload `{"message": "Requires authentication", "status": "401"}`.

## 2. Cuadro comparativo de respuestas HTTP capturadas

| Código | Estado | Origen de Respuesta | Escenario / Justificación Técnica |
| --- | --- | --- | --- |
| **`200`** | `OK` | Servidor Web / CDN | Carga inicial del documento HTML procesada con éxito. |
| **`301`** | `Moved Permanently` | Servidor Web (`GitHub.com`) | Redirección de protocolo enviada por el servidor remoto (`HTTP` → `HTTPS`). |
| **`307`** | `Internal Redirect` | Cliente (Navegador) | Intercepción de seguridad local generada por la directiva HSTS previa. |
| **`304`** | `Not Modified` | Servidor / Caché | Confirmación de validez de caché local basada en la coincidencia del ETag. |
| **`404`** | `Not Found` | Servidor Web | Solicitud a un recurso que no existe en el árbol de archivos. |
| **`401`** | `Unauthorized` | Servidor API (`api.github.com`) | Rechazo explícito por ausencia total de encabezados de autorización. |

## 3. Análisis e interpretación técnica

Lo que más me llamó la atención al comparar estos seis casos fue lo distinto que es el "responsable" detrás de cada código:

1. **La diferencia entre `301` y `307` (HSTS) me pareció la más reveladora.** El `301` sí es una respuesta real que viajó por el socket TCP hasta `GitHub.com`, que me dijo explícitamente "muévete a esta otra URL". En cambio, el `307 Internal Redirect` nunca salió de mi máquina: mi propio navegador reconoció el dominio en su lista HSTS y cambió el esquema a HTTPS antes de que la petición llegara siquiera a la red.

2. **El `304` me sirvió para ver la caché en acción.** Al recargar con `F5` teniendo la caché habilitada, comprobé que el cliente conserva una copia local válida y que el servidor confirma esa validez sin reenviar el cuerpo del documento, ahorrando ancho de banda.

3. **`404` y `401` parecen similares pero representan problemas distintos.** El `404` me dijo "ese archivo no existe", mientras que el `401` me dijo "el archivo (o recurso) podría existir, pero primero necesito saber quién eres". Es una distinción importante a la hora de diagnosticar por qué falla una petición.


## 4. Conclusión

Con estas seis pruebas confirmé que un mismo flujo de navegación puede producir códigos de estado con orígenes muy distintos: el servidor de origen (`200`, `301`, `404`), la caché compartida entre cliente y servidor (`304`), la política de seguridad interna de mi propio navegador (`307`) y las reglas de autenticación de una API externa (`401`). Entender quién responde en cada caso —y no solo qué número aparece— es lo que realmente me ayuda a diagnosticar el comportamiento de una aplicación web.