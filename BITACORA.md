# Bitácora — Bayron Fuentes — Sprint 01

## Día 1 — 12 de septiembre de 2026

**Horas efectivas:** 4 h (práctica: 2.5 · teoría: 1 · coach: 0.5)

**Qué estudié**
- Lectura completa del Brief del Sprint 01
- Lectura de la Rúbrica Sprint 01
- Lectura de las Reglas del Juego
- Bloque A (computador): CPU, RAM, disco, SO
- Bloque C (terminal): comandos básicos

**Qué construí**
- Repo local inicializado con `git init`
- Estructura de carpetas: ejercicios/, investigacion/, estilos/
- 4 archivos HTML base (index, dns, http, https)
- CSS con variables personalizadas (colores: #010614, #c80606, #000000)
- GitHub Pages configurado y en vivo: https://bayronfc05.github.io/HU-S01-03-micrositio-enter/
- 3 commits realizados y subidos a GitHub

**En qué me atasqué y cómo salí**
- Problema: `touch` no funcionaba en PowerShell
- Solución: Cambié a Git Bash (herramienta de Git para terminal)
- Problema: `git push` fallaba por rama `master` vs `main`
- Solución: Usé `git branch -M main` para renombrar la rama
- Problema: Sitio no visible en GitHub Pages
- Solución: Esperé a que GitHub procesara el deployment (2-3 min)

**Uso de IA hoy**
| Qué pregunté | Qué hice con la respuesta | ¿Entendí? |
|---|---|---|
| CSS base con variables | Adapté los colores a mi identidad visual (#010614 es azul oscuro, #c80606 es rojo) | Sí — entiendo cómo funcionan las variables CSS |

**Lo que hoy no entendí y voy a llevar a mentoría**
- Diferencia entre `fetch` y `pull` en Git
- Cómo funcionan exactamente los media queries en CSS


**Mañana arranco por**
- Experimento E1: Reto de terminal sin mouse (crear árbol de carpetas, mover, renombrar, borrar)
- Bloque B: Internet (IP, DNS, HTTP, HTTPS)
- Bloque D: Git y GitHub
- Investigación: Experimentos X1 a X3 (DNS, traceroute, ping)

## Día 2 — 14 de septiembre de 2026

**Horas efectivas:** (4h)

**Qué estudié**
- Bloque C (terminal): navegación, archivos, lectura, búsqueda, encadenar, permisos

**Qué construí**
- Ejercicio E1 completo: reto de terminal sin mouse (árbol de 3 niveles, mover, renombrar, borrar), grabado con OBS y subido a drive con enlace de acceso publico
- Ejercicio E2 completo (cubierto dentro de X1)
- Experimento X1 completo: arqueología DNS de 6 dominios (mercadolibre.com.co, elespectador.com, google.com, github.com, bayronfc05.github.io, eltiempo.com) con IP, tipo de registro, TTL y servidor que respondió
- Commits y push de toda la evidencia

**En qué me atasqué y cómo salí**
- Problema: corrí `git init` sin querer en la carpeta raíz de mi usuario de Windows, Git empezó a escanear carpetas del sistema con warnings de "Permission denied"
- Solución: borré esa carpeta `.git` con `rm -rf .git`, ubiqué la carpeta correcta de mi proyecto con `cd`, y verifiqué con `git status` que era el repo correcto antes de seguir

**Uso de IA hoy**
| Qué pregunté | Qué hice con la respuesta | ¿Entendí? |
|---|---|---|
| Qué significan TTL y "no autoritativa" en nslookup | Los usé para llenar mi tabla de X1 con la columna correcta | Sí |

**Lo que hoy no entendí y voy a llevar a mentoría**
- Hoy no hubo dudas grandes que no pudiera resolver por mi mismo aplicando la regla 30/30

**Mañana arranco por**
- Bloque B: Internet (IP, DNS, HTTP, HTTPS)
- Ejercicio E3: cacería de códigos HTTP en DevTools
- Experimentos X2 (traceroute) y X3 (ping)

## Día 3 — 15 de septiembre de 2026

**Horas efectivas:** 4.5 h (práctica: 3.5 · teoría: 1)

**Qué estudié**
- Inspección detallada de protocolos de red y transporte (HTTP/HTTPS, TCP, TLS 1.3)
- Mecanismos de caché y aceleración web mediante CDN (Fastly) y proxy (Varnish)
- Cabeceras de respuesta HTTP y cadena de confianza de certificados TLS/SSL
- Interpretación de códigos de estado HTTP (2xx, 3xx, 4xx) y comportamiento HSTS del navegador

**Qué construí**
- Experimento X2 (ruta de red): `investigacion/ruta.md`, trazando nodos de salto con `tracert`
- Experimento X3 (latencia): `investigacion/latencia.md`, midiendo con `ping` y `nslookup`
- Ejercicio E3 (cacería HTTP): `ejercicios/http.md` con capturas en `ejercicios/img/`
- Experimento X4 (headers HTTP): `investigacion/headers.md` con `curl -I`
- Experimento X5 (certificado TLS): `investigacion/tls.md`, cadena de confianza y grupo criptográfico post-cuántico (`X25519MLKEM768`) verificado con `openssl s_client`
- Experimento X6 (códigos HTTP en DevTools): `investigacion/codigos.md`, 6 estados capturados (200, 301, 307 HSTS, 304, 404, 401)
- Historial de Git limpio, commits independientes por cada experimento, subidos al remoto

**En qué me atasqué y cómo salí**
- Problema: al navegar por `http://` en DevTools, veía `307` en vez del `301` esperado
- Solución: identifiqué que era la cabecera HSTS guardada en el navegador interceptando la petición localmente. Usé ventana de incógnito para forzar la respuesta real del servidor, y confirmé con `curl -I` que GitHub Pages sí responde 301

**Uso de IA hoy**
| Qué pregunté | Qué hice con la respuesta | ¿Entendí? |
|---|---|---|
| Análisis de headers HTTP (`X-Served-By`, `Via`) | Estructuré la explicación del rol de la CDN Fastly para X4 | Sí |
| Desglose de la salida de `openssl s_client` | Documenté la cadena de certificados y el grupo TLS1.3 para X5, verificando yo mismo el output real | Sí |
| Diferencia entre 301 de servidor y 307 por HSTS | Ajusté mi metodología de prueba (modo incógnito) para X6 | Sí |

**Lo que hoy no entendí y voy a llevar a mentoría**
- Cómo configurar directivas de caché avanzadas en un servidor sin depender del proxy por defecto de GitHub Pages

**Mañana arranco por**
- Escribir el contenido real de las 9 etapas en `index.html` (qué pasa, quién lo hace, analogía) con fuentes citadas
- Empezar a poblar `dns.html`, `http.html`, `https.html` con los datos ya recolectados en X1-X6