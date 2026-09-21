# Micrositio "¿Qué pasa cuando presionás Enter?"

## 1. Perfil del cliente / público objetivo

Este micrositio está diseñado exclusivamente para **estudiantes interesados en tecnología de 16 años en adelante, sin experiencia previa en el área** — el mismo perfil que describe el brief del programa de Fundación CEPAV (último año de colegio, primeros semestres de técnico, o ingresantes a una próxima cohorte de *Impulso Digital*).

No es un producto genérico para "cualquiera": está dirigido a personas que usan internet todos los días pero nunca se han preguntado qué infraestructura hay detrás de ese uso. El contenido abstrae la complejidad técnica con lenguaje cercano y analogías del mundo real, para acompañar el primer contacto de alguien con la ingeniería de redes y el desarrollo web.

## 2. Problema de aprendizaje que resuelve

En la formación técnica tradicional se suele enseñar a programar (HTML/CSS/JS) sin explicar la capa de infraestructura sobre la que corren y viajan esos archivos. Eso genera desarrolladores que saben seguir un tutorial, pero que se quedan sin herramientas cuando algo falla fuera del guion: un recurso que no carga (`404`), un bloqueo de permisos (`401`/`403`), un error de servidor (`500`) o un certificado TLS vencido.

Este micrositio resuelve ese vacío con un enfoque **empírico**: explica el recorrido completo de una petición web apoyándose en mediciones y capturas reales que yo mismo ejecuté sobre mi propia infraestructura (`bayronfc05.github.io`) — DNS, headers HTTP, certificado TLS, códigos de estado — no en teoría copiada de un libro.

## 3. Métrica de éxito y validación de aprendizaje

Uso dos criterios concretos para saber si alguien realmente aprendió:

1. **Reconstrucción secuencial autónoma.** La persona debe poder explicar de memoria, en orden y con sus propias palabras, las 9 etapas del recorrido de la petición web — el mismo estándar que me van a exigir a mí en el Demo Day con la pregunta "escribo tu URL y presiono Enter, cuéntame todo lo que pasa".
2. **Mini-quiz sobre el glosario.** Elijo 5 términos al azar del glosario del sitio (por ejemplo: DNS, TLS, ETag, caché, response) y le pido a la persona que los defina sin consultar la documentación. Si acierta al menos **4 de 5**, el sitio cumplió su función.

## 4. Análisis de costos — dominio propio

El proyecto está desplegado gratis en GitHub Pages, bajo `bayronfc05.github.io`. Migrar a un dominio propio (por ejemplo `quepasacuandopresionas.com`) no cambia el costo de hosting — sigue en $0 — el único costo nuevo sería el registro y la renovación anual del dominio.

*Tasa de cambio de referencia: en la segunda quincena de septiembre de 2026 la TRM ha estado oscilando entre **$3.070 y $3.220 COP por dólar** (fuente: Superintendencia Financiera de Colombia / Portafolio). Para estas cifras uso **1 USD ≈ $3.100 COP** como valor redondo de referencia — la tasa cambia a diario, así que esto es solo una estimación.*

| Extensión | Registro 1er año (USD) | Renovación anual (USD) | Renovación estimada (COP) | Ventajas | Desventajas |
|---|---|---|---|---|---|
| **.com** | $8 – $15 | $15 – $20 | ~$46.500 – $62.000 | Máximo reconocimiento global; la mejor relación costo-beneficio; nadie duda de que sea "un sitio real" | Los nombres cortos u obvios ya están tomados |
| **.co** | $10 – $30 | $35 – $48 | ~$108.500 – $148.800 | Buena alternativa para el mercado hispanohablante y proyectos locales en Colombia | Renovación más cara que `.com` |
| **.io** | $15 – $50 | $30 – $60 | ~$93.000 – $186.000 | Dominio de referencia en el ecosistema de developers y startups tech | Renovación cara para un proyecto educativo/inicial; técnicamente es el ccTLD de un territorio, no un genérico |
| **.tech** | $7 – $53 | $40 – $55 | ~$124.000 – $170.500 | Comunica explícitamente la naturaleza técnica del proyecto | Poco reconocido fuera de círculos tech; renovación similar a `.io` |
| **.ai** | $70 – $100 | $85 – $120 | ~$263.500 – $372.000 | Orientado a proyectos específicamente de inteligencia artificial | El más caro de lejos; no aplica a este micrositio, que es de redes/HTTP, no de IA |

**Recomendación:** un dominio **`.com`** o **`.co`**. Son las opciones más baratas de mantener y las que un estudiante de 16 años reconoce sin explicación, que es exactamente el público al que le hablo.

## 5. Evaluación de infraestructura y hosting

Al ser un micrositio **estático** (HTML y CSS, sin backend ni base de datos), no necesita un servidor complejo:

| Plataforma de hosting | Costo mensual | HTTPS | Ventajas | Desventajas |
|---|---|---|---|---|
| **GitHub Pages** *(la que uso hoy)* | $0 | Incluido (Let's Encrypt) | Se despliega solo con cada `git push`; costo $0 permanente; distribución por CDN (Fastly/Varnish, con nodo en Bogotá) | Solo sirve archivos estáticos, sin backend |
| **Netlify / Vercel** (plan gratuito) | $0 | Incluido (Let's Encrypt) | Despliegues automáticos por rama (previews), gestión nativa de redirecciones | Límite mensual de ancho de banda y minutos de compilación |
| **Hosting compartido** (cPanel, etc.) | ~$3 – $8 USD (~$9.300 – $24.800 COP) | Variable, a veces con costo aparte | Permite backend (PHP, bases de datos) si algún día lo necesitara | Innecesario para un sitio sin backend; requiere subir archivos manualmente o configurar CI |

## 6. Conclusión y viabilidad financiera

Para la naturaleza estática y educativa de este micrositio, **GitHub Pages** cubre el 100% de las necesidades técnicas (rendimiento, HTTPS automático, disponibilidad regional vía CDN) a costo **$0**.

Si en algún momento decido pasar a un dominio propio, el presupuesto anual quedaría en aproximadamente **$15 – $20 USD (~$46.500 – $62.000 COP)** por el dominio `.com`, manteniendo el hosting en **$0**.