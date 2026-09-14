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

**Horas efectivas:** (pon tu total real, ej. 4h)

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