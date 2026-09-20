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

## Día 4 — 16 de septiembre de 2026

**Horas efectivas:** 4 h (práctica: 3 h · teoría: 30 min · coach: 30 min)

**Qué estudié**
- Bloque D (parte final): ramas (`branch`, `switch -c`, `merge`), qué es un conflicto
  y cómo se resuelve, buenos mensajes de commit, cómo GitHub Pages publica desde una rama

**Qué construí**
- Ejercicio E5 completo: provoqué un conflicto de merge real entre `main` y una rama de
  prueba, lo resolví editando el archivo a mano, documentado en `ejercicios/merge.md`
- Estructura HTML de la línea de tiempo de las 9 etapas en `index.html`, con `id`s para
  que el ancla `#paso-1` funcione, usando `<ol>` semántico y clases para maquetar después
- Contenido completo de las 9 etapas (qué pasa, quién lo hace, analogía) para `index.html`
- `FUENTES.md`: 9 fuentes técnicas diversificadas para las 9 etapas de index.html (RFC
  9111, RFC 1034, RFC 9293, RFC 8446, RFC 9110, WHATWG HTML spec, WHATWG Fetch spec,
  web.dev)

**En qué me atasqué y cómo salí**
- Problema: al "resolver" el conflicto de E5 la primera vez, dejé sin querer una marca de
  conflicto suelta sin borrar. Git no valida que el archivo quede coherente, solo que yo
  haya marcado el archivo como resuelto con `git add`
- Solución: lo detecté revisando `git log --oneline --graph` (vi un commit extra con
  mensaje confuso) y confirmé con `git --no-pager show <hash> -- index.html`. Corregí el
  archivo y arreglé el mensaje del commit con `git commit --amend` antes de hacer push
- Problema: quise recuperar el historial de comandos de la terminal con `tail`, pero
  estaba en PowerShell, no en Git Bash, y `tail` no existe ahí
- Solución: usé el equivalente de PowerShell (`Select-Object -Last`) para lo que hiciera
  falta, y confirmé que no era crítico porque `git log`/`git show` ya daban la evidencia, 
  ademas como ya habia cerrado la sesion de mi terminal en mi editor de codigo pues no pude
  recuperar los comandos por los cual hice el video solo con los logs.

**Uso de IA hoy**
| Qué pregunté | Qué hice con la respuesta | ¿Entendí? |
|---|---|---|
| Estructura HTML semántica para la línea de tiempo de 9 etapas | La usé tal cual, ajustando CSS para quitar la doble numeración que generó | Sí |


**Lo que hoy no entendí y voy a llevar a mentoría**
- (nada bloqueante hoy)

**Mañana arranco por**
- Empezar a poblar `dns.html`, `http.html`, `https.html` con las tablas de X1-X6 y las
  fuentes específicas de cada página


  ## Día 5 — 17 de septiembre de 2026

**Horas efectivas:** 4 h (práctica: 3 h · teoría: 30 min · coach: 30 min)

**Qué estudié**
- Headers HTTP comunes (Cache-Control, ETag, Strict-Transport-Security) aplicados a mis propias capturas
- Qué información específica no protege HTTPS/TLS (SNI, momento de conexión, análisis de tráfico)

**Qué construí**
- `dns.html`: tabla real de resolución DNS de 6 dominios (experimento X1), con IP, tipo
  de registro, TTL y análisis de por qué mi sitio tiene TTL mucho más alto que sitios con
  balanceo dinámico
- `http.html`: tabla de códigos de estado (8, con "de quién es la culpa" y ejemplo real
  o nota explícita de "no lo he visto en vivo" cuando aplica) + tabla de 9 headers reales
  capturados con `curl -I` (experimento X4), incluyendo el hallazgo de que mi sitio lo
  sirve un nodo de Fastly en Bogotá (`X-Served-By: cache-bog...`)
- `https.html`: tabla del certificado TLS real (Let's Encrypt, TLS 1.3,
  X25519MLKEM768) + sección de 3 cosas que HTTPS no protege, con fuente RFC 6066/8446
- 3 commits independientes, uno por página, subidos al remoto

**En qué me atasqué y cómo salí**
- (nada bloqueante hoy)

**Uso de IA hoy**
| Qué pregunté | Qué hice con la respuesta | ¿Entendí? |
|---|---|---|
| Cómo estructurar las tablas HTML con datos ya recolectados en X1/X4/X5/X6 | Usé la estructura semántica (caption, scope) y pegué mis propios datos reales, sin inventar valores | Sí |

**Lo que hoy no entendí y voy a llevar a mentoría**
- (nada bloqueante hoy)

**Mañana arranco por**
- CSS: sistema visual del sitio y línea de tiempo de las 9 etapas con CSS puro

## Día 6 — 18 de septiembre de 2026 (avance de Días 6, 7 y 8 del plan)

**Horas efectivas:** 5 horas y 40 min (práctica: 4:20 · teoría: 50 min · coach: 30 min)

**Qué estudié**
- Bloque E (CSS): selectores y especificidad, box model, box-sizing: border-box, Flexbox
  (display: flex, justify-content, align-items, gap)

**Qué construí**

*Día 6 — Maquetación:*
- Sistema de variables CSS consolidado en un solo archivo (`style.css`), eliminando un
  conflicto que tenía con un segundo archivo `variables.css` con nombres y valores
  distintos que se pisaban entre sí
- Línea de tiempo de las 9 etapas maquetada con CSS puro (línea vertical + círculos con
  `::before`, sin imágenes ni JavaScript) — CA-3
- Navegación del header con Flexbox, con foco visible (`:focus-visible`) para teclado
- **Bug importante encontrado y corregido:** `dns.html`, `http.html` y `https.html`
  solo tenían el fragmento de `<main>`, sin `<!DOCTYPE>`, `<head>`, `<link>` al CSS,
  `<header>` ni `<footer>`. Reconstruí las 3 con la estructura completa, agregué el contenido faltante (explicación de DNS
  que había quedado como comentario vacío) y la tabla de códigos de estado que faltaba
  en `http.html`

*Día 7 — Responsive (adelantado hoy mismo):*
- Verificado de 320px a 1440px: tablas con scroll horizontal propio (no de la página),
  nav se vuelve vertical en pantallas chicas, línea de tiempo estable — sin necesitar
  media queries adicionales (RC-7)

*Día 8 — Accesibilidad (adelantado hoy mismo):*
- Navegación completa por teclado (Tab/Enter/flechas) con foco visible
- Contraste de color verificado: 5.52:1 en todas las combinaciones (supera AA)
- Jerarquía de headings correcta, un solo h1 por página (RC-5, RC-9)
- Confirmé que RC-6 (alt en imágenes) no aplica por ahora: el sitio no tiene imágenes,
  y no es un requisito obligatorio de la rúbrica tenerlas

*Fuentes y organización:*
- `FUENTES.md` consolidado a 15 fuentes técnicas de alta calidad (RFC, WHATWG, web.dev),
  cubriendo las 4 páginas del sitio, fusionando entradas que repetían el mismo RFC
- Publiqué el link de mi repositorio y del sitio en vivo como comentario en mi Issue de
  la fundación 
- Ubiqué el repo de mi compañera de peer review (Estudiante 4) en el Issue de la fundación

**En qué me atasqué y cómo salí**

- Problema: el sitio en vivo no mostraba los cambios aunque el editor sí los veía
- Solución: confirmé con `git status` que el archivo tenía cambios sin commitear/pushear;
  aprendí a distinguir la vista previa local del estado real del sitio publicado
- Problema: las tablas se desbordaban horizontalmente en móvil, pensé que era un bug
- Solución: confirmé que era el comportamiento correcto (scroll contenido dentro de la
  tabla, no de toda la página), tal como exige CA-12 para bloques de código

**Uso de IA hoy**
| Qué pregunté | Qué hice con la respuesta | ¿Entendí? |
|---|---|---|
| Por qué el CSS de la línea de tiempo no se veía | Diagnostiqué el conflicto de dos archivos de variables y consolidé en uno | Sí |
| Si el "desborde" de las tablas en móvil era un error | Confirmé que era el comportamiento esperado según mi propia rúbrica (CA-12) | Sí |


**Lo que hoy no entendí y voy a llevar a mentoría**
- (nada bloqueante hoy)

**Mañana arranco por**
- Peer review al Estudiante 4: 5 comentarios útiles en su repo + resumen en su Issue
- Validador W3C y Lighthouse (Día 9 del plan)


## Día 9 — 19 de septiembre de 2026

**Horas efectivas:** 5 h 30 min (práctica: 4:20 · teoría: 30 min · coach: 40 min)

**Qué estudié**
- Criterios del validador W3C para HTML semántico y cómo interpretar sus reportes de errores
- Métricas de Lighthouse (móvil): qué evalúan las categorías de Accesibilidad y Buenas prácticas

**Qué construí**
- Validación de las 4 páginas del sitio en el validador del W3C: **sin errores**
- Corrida de Lighthouse (móvil) en las 4 páginas: **Accesibilidad y Buenas prácticas, ambas > 90** (RC-11 cumplido)
- Mejoras de estilo en `style.css`:
  - Nueva tipografía (`Space Grotesk`) aplicada al header y a los títulos
  - Rediseño de la línea de tiempo: cada paso ahora es una tarjeta individual (`.paso`), con círculo en el eje vertical, borde lateral de color y el número de etapa como marca de agua de fondo
  - Resaltado de fila al pasar el mouse (`tbody tr:hover`) en las tablas de `dns.html`, `http.html` y `https.html`
  - Nueva sección de glosario (`.glosario-lista`, `.glosario-item`) en grid responsive, con estilo dinámico: elevación y sombra al hacer hover sobre cada término
- Redacción de la agenda de la Mentoría 2, con los bloqueos y temas a llevar

**En qué me atasqué y cómo salí**
- Problema: intenté hacer el peer review al Estudiante 4 (HU-S01-04), pero su repositorio está **vacío** — no hay nada que revisar ni comentar
- Solución: dejé un comentario en su Issue documentando que revisé su repo en la fecha correspondiente y que no encontré contenido para dejar los 5 comentarios que pide la plantilla de Peer Review; quedo pendiente de volver a intentarlo si él sube avances antes del cierre del sprint, ademas lo agregue como bloqueo de la mentoria para tener claridad al respecto.

**Uso de IA hoy**
- No usé IA para tareas nuevas hoy

**Lo que hoy no entendí y voy a llevar a mentoría**
- (nada bloqueante hoy)

**Mañana arranco por**
- **Mentoría 2** (según mi plan de ataque: 1 h técnica + 1 h de ensayo de demo), con la agenda que preparé hoy
- Empezar a adelantar las correcciones de `README.md` y `NEGOCIO.md`.