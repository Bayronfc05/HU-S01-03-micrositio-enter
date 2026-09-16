# Ejercicio E3 — Cacería de códigos de estado HTTP

Evidencias de tráfico real capturadas mediante las herramientas DevTools del navegador y comandos de terminal (`curl`):

---

## 1. Código 200 OK
* **URL / Recurso:** Pestaña de inicio del navegador
* **Familia:** 2xx (Éxito)
* **¿Qué significa?:** La petición fue recibida, procesada y respondida correctamente por el servidor. El recurso solicitado se entregó con éxito en el cuerpo de la respuesta.
* **¿De quién es la responsabilidad?:** Comportamiento normal del protocolo (Éxito).
* **Captura de pantalla:** `![Código 200 OK](img/200.jpg)`

---

## 2. Código 301 Moved Permanently
* **URL / Recurso:** `http://bayronfc05.github.io/HU-S01-03-micrositio-enter/`
* **Familia:** 3xx (Redirección)
* **¿Qué significa?:** El recurso solicitado fue movido de manera permanente a una nueva ubicación. El servidor devuelve el encabezado `Location` indicando la nueva URL segura (`https://`).
* **Herramienta utilizada:** Terminal Git Bash mediante el comando `curl -I`.
* **¿De quién es la responsabilidad?:** Del servidor, que redirige activamente las conexiones no seguras (HTTP) hacia el protocolo seguro (HTTPS).
* **Captura de pantalla:** `![Código 301 Moved Permanently](img/301.png)`

---

## 3. Código 304 Not Modified
* **URL / Recurso:** `https://bayronfc05.github.io/HU-S01-03-micrositio-enter/`
* **Familia:** 3xx (Caché / Redirección implícita)
* **¿Qué significa?:** Al recargar la página, el navegador envía una petición condicional comprobando si el recurso cambió. El servidor responde que el archivo no ha sido modificado, por lo que el navegador reutiliza la copia guardada en su memoria local para optimizar tiempo y ancho de banda.
* **¿De quién es la responsabilidad?:** Optimización de recursos entre cliente y servidor.
* **Captura de pantalla:** `![Código 304 Not Modified](img/304.png)`

---

## 4. Código 404 Not Found
* **URL / Recurso:** `https://bayronfc05.github.io/HU-S01-03-micrositio-enter/no-existe.html`
* **Familia:** 4xx (Error del cliente)
* **¿Qué significa?:** El servidor no pudo encontrar el recurso solicitado dentro de la ruta especificada.
* **¿De quién es la responsabilidad?:** Del cliente, por ingresar una ruta inexistente o solicitar un recurso eliminado.
* **Captura de pantalla:** `![Código 404 Not Found](img/404.png)`