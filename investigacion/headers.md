# Experimento X4 — Inspección de Encabezados HTTP (Headers)

Documentación y desglose técnico de los encabezados de respuesta devueltos por el servidor al consultar la raíz del micrositio alojado en GitHub Pages.

---

## 1. Salida real del comando `curl -I`

```text
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 1673
Server: GitHub.com
Content-Type: text/html; charset=utf-8
Last-Modified: Wed, 16 Sep 2026 02:06:52 GMT
Access-Control-Allow-Origin: *
Strict-Transport-Security: max-age=31556952
ETag: "6aa9f9bc-689"
expires: Wed, 16 Sep 2026 02:18:34 GMT
Cache-Control: max-age=600
x-proxy-cache: MISS
X-GitHub-Request-Id: CE08:2D6071:D3ABB2:E23EC6:6AA9FA21
x-github-edge-region: iad
Accept-Ranges: bytes
Age: 0
Date: Wed, 16 Sep 2026 02:08:34 GMT
Via: 1.1 varnish
X-Served-By: cache-bog-skbo2340037-BOG
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1789524514.272044,VS0,VE98
Vary: Accept-Encoding
X-Fastly-Request-ID: 0f2d0052f1be5869a97c6d07e379b41e18596505
```

---

## 2. Desglose y análisis técnico de encabezados clave

| Encabezado (Header) | Valor Capturado | Significado Técnico |
| --- | --- | --- |
| **`HTTP/1.1 200 OK`** | `200 OK` | Línea de estado que indica que la petición fue procesada de manera exitosa. |
| **`Server`** | `GitHub.com` | Identifica el software o la infraestructura del servidor web de origen. |
| **`Content-Type`** | `text/html; charset=utf-8` | Indica el tipo MIME del archivo servido (`HTML`) y su codificación de caracteres (`UTF-8`). |
| **`Strict-Transport-Security`** | `max-age=31556952` | Encabezado HSTS que le ordena al navegador comunicarse **únicamente por HTTPS** durante el tiempo especificado (1 año). |
| **`Cache-Control`** | `max-age=600` | Le indica al navegador que guarde el recurso en caché por un máximo de 600 segundos (10 minutos). |
| **`ETag`** | `"6aa9f9bc-689"` | Identificador único de la versión del recurso servido; se usa en peticiones condicionales para validar si el archivo cambió (código 304). |
| **`X-Served-By`** | `cache-bog-skbo2340037-BOG` | Muestra la ubicación exacta del nodo CDN de Fastly que procesó la respuesta (en este caso, la caché local en Bogotá, Colombia: `BOG`). |
| **`Via`** | `1.1 varnish` | Revela que la petición atravesó un proxy/acelerador web de la CDN basado en el motor Varnish. |
| **`X-Fastly-Request-ID`** | `0f2d0...` | Identificador único asignado por la red de distribución de contenido Fastly para rastreo de solicitudes. |

---

## 3. Conclusión técnica

La respuesta obtenida demuestra cómo GitHub Pages delega la entrega de contenido a la infraestructura Edge CDN de Fastly. La cabecera `X-Served-By` confirma que la petición fue atendida directamente por un nodo intermedio ubicado en Bogotá (`cache-bog...-BOG`), reduciendo drásticamente la latencia de respuesta para usuarios locales en Colombia.