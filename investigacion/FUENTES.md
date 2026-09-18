# Fuentes técnicas — index.html (las 9 etapas)

1. **RFC 9111 (IETF)** — "HTTP Caching" (etapa 1 — caché del navegador):
   https://www.rfc-editor.org/rfc/rfc9111.html
   > Define que una respuesta almacenada puede reutilizarse si está "fresh"; si está obsoleta, se revalida con el servidor de origen antes de usarla.

2. **RFC 1034 (IETF)** — "Domain Names — Concepts and Facilities" (etapa 2 — DNS):
   https://www.rfc-editor.org/rfc/rfc1034.html
   > Describe el DNS como sistema jerárquico de nombres y la interacción entre clientes y servidores DNS.

3. **RFC 9293 (IETF)** — "Transmission Control Protocol" (etapa 3 — conexión TCP):
   https://www.rfc-editor.org/rfc/rfc9293.html
   > Define el three-way handshake (SYN, SYN-ACK, ACK) para establecer una conexión y sincronizar números de secuencia.

4. **RFC 8446 (IETF)** — "TLS 1.3" (etapa 4 — handshake TLS):
   https://www.rfc-editor.org/rfc/rfc8446.html
   > Define el intercambio ClientHello/ServerHello y el mensaje Certificate para transmitir la cadena de certificados del servidor.

5. **RFC 9110 (IETF)** — "HTTP Semantics" (etapa 5 — request GET):
   https://www.rfc-editor.org/rfc/rfc9110.html
   > El método GET solicita la transferencia de una representación del recurso identificado por el destino de la solicitud.

6. **RFC 9110 (IETF)** — "HTTP Semantics" (etapa 6 — códigos de estado):
   https://www.rfc-editor.org/rfc/rfc9110.html
   > Los códigos de estado se agrupan por su primer dígito: 1xx informativo, 2xx éxito, 3xx redirección, 4xx error del cliente, 5xx error del servidor.

7. **WHATWG HTML Standard** — "Parsing HTML documents" (etapa 7 — parseo de HTML):
   https://html.spec.whatwg.org/multipage/parsing.html
   > Los navegadores deben tokenizar el flujo de caracteres del HTML y luego construir el árbol DOM a partir de esos tokens.

8. **WHATWG Fetch Standard** (etapa 8 — descarga de recursos):
   https://fetch.spec.whatwg.org/
   > Define el algoritmo general de obtención de recursos: una solicitud entra al proceso de fetch y produce una respuesta.

9. **web.dev (Google)** — "Rendering performance" (etapa 9 — renderizado):
   https://web.dev/articles/rendering-performance
   > El navegador calcula estilos, hace layout para tamaño/posición, pinta texto/colores/imágenes, y compone las capas en la imagen final.
