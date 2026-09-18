# Fuentes técnicas — HU-S01-03

## index.html (las 9 etapas)

1. **RFC 9111 (IETF)** — "HTTP Caching" (etapa 1 — caché del navegador):
   https://www.rfc-editor.org/rfc/rfc9111.html
   > Una respuesta almacenada puede reutilizarse si está "fresh"; si está obsoleta, se revalida con el servidor de origen.

2. **RFC 1034 (IETF)** — "Domain Names — Concepts and Facilities" (etapa 2 — DNS):
   https://www.rfc-editor.org/rfc/rfc1034.html
   > Describe el DNS como sistema jerárquico de nombres y la interacción entre clientes y servidores.

3. **RFC 9293 (IETF)** — "Transmission Control Protocol" (etapa 3 — conexión TCP):
   https://www.rfc-editor.org/rfc/rfc9293.html
   > Define el three-way handshake (SYN, SYN-ACK, ACK) para establecer una conexión.

4. **RFC 8446 (IETF)** — "TLS 1.3" (etapa 4 — handshake TLS; también respalda https.html):
   https://www.rfc-editor.org/rfc/rfc8446.html
   > Define el intercambio ClientHello/ServerHello/Certificate, y en su sección 10.2.3 explica que TLS es susceptible a análisis de tráfico por longitud/tiempo de paquetes.

5. **RFC 9110 (IETF)** — "HTTP Semantics" (etapas 5 y 6 — request GET y códigos de estado):
   https://www.rfc-editor.org/rfc/rfc9110.html
   > GET solicita la transferencia de un recurso; los códigos de estado se agrupan por su primer dígito (1xx-5xx).

6. **WHATWG HTML Standard** — "Parsing HTML documents" (etapa 7):
   https://html.spec.whatwg.org/multipage/parsing.html
   > Los navegadores tokenizan el HTML y construyen el árbol DOM a partir de esos tokens.

7. **WHATWG Fetch Standard** (etapa 8 — descarga de recursos):
   https://fetch.spec.whatwg.org/
   > Define el algoritmo general de obtención de recursos.

8. **web.dev (Google)** — "Rendering performance" (etapa 9 — renderizado):
   https://web.dev/articles/rendering-performance
   > El navegador calcula estilos, hace layout, pinta y compone las capas en la imagen final.

## dns.html

9. **RFC 1035 (IETF)** — "Domain Names — Implementation and Specification":
   https://www.rfc-editor.org/rfc/rfc1035.html
   > El RDATA de un registro CNAME contiene el nombre canónico; el registro A apunta a una dirección.

10. **RFC 9499 (IETF)** — "DNS Terminology" (servidor autoritativo vs. resolver):
    https://www.rfc-editor.org/rfc/rfc9499.html
    > Un servidor autoritativo conoce localmente una zona; un resolver obtiene info de otros servidores.

## http.html

11. **RFC 9110 (IETF)**, secciones 15.5.2/15.5.4 (401 vs 403):
    https://www.rfc-editor.org/rfc/rfc9110.html
    > 401: falta autenticación válida. 403: el servidor entendió la solicitud pero se niega a cumplirla.

12. **RFC 9111 (IETF)** (directivas de Cache-Control):
    https://www.rfc-editor.org/rfc/rfc9111.html
    > Define max-age, s-maxage, no-cache, no-store, private, public, must-revalidate.

## https.html

13. **RFC 6797 (IETF)** — "HTTP Strict Transport Security (HSTS)":
    https://www.rfc-editor.org/rfc/rfc6797.html
    > Permite que un sitio declare que solo debe accederse por HTTPS.

14. **RFC 6066 (IETF)** — "TLS Extensions", sección 3 (SNI — qué NO protege HTTPS):
    https://www.rfc-editor.org/rfc/rfc6066.html
    > El cliente envía el nombre de dominio en texto claro en la extensión SNI del ClientHello.

15. **RFC 5280 (IETF)** — "Internet X.509 PKI Certificate Profile":
    https://www.rfc-editor.org/rfc/rfc5280.html
    > Define el perfil de certificados X.509: identidad, clave pública, emisor, validez y firma.