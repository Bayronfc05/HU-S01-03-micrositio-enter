# X1 — Arqueología DNS

| Dominio | IP(s) | Tipo de registro | TTL | Servidor que respondió |
|---|---|---|---|---|
| mercadolibre.com.co | 54.230.144.60 / .4 / .84 / .91 | A | 55 seg | Resolver local (192.168.10.1) — no autoritativo |
| elespectador.com | 2a04:fa87:fffd::c000:425b / 192.0.66.91 | AAAA + A | 185 seg | Resolver local (192.168.10.1) — no autoritativo |
| google.com | 2800:3f0:4005:41c::200e / 172.217.162.142 | AAAA + A | 205 seg | Resolver local (192.168.10.1) — no autoritativo |
| github.com | 140.82.114.4 | A | 41 seg | Resolver local (192.168.10.1) — no autoritativo |
| bayronfc05.github.io | 185.199.108.153 / .109 / .110 / .111 (+ 4 IPv6) | A + AAAA | 3281 seg (~54 min) | Resolver local (192.168.10.1) — no autoritativo |
| eltiempo.com *(extra)* | 20.57.95.139 | A | 32 seg | Resolver local (192.168.10.1) — no autoritativo |

**Servidor que respondió — nota importante:** en los 6 casos fue mi propio resolver local/router (`192.168.10.1`), no el servidor autoritativo del dominio. Por eso todas las respuestas dicen "no autoritativa": mi router pregunta primero a un DNS más arriba en la cadena (el de mi ISP) y guarda la respuesta en caché por el tiempo que indica el TTL, para no tener que volver a preguntar cada vez.

**Conclusión (TTL corto vs. largo):** el TTL no depende de si el sitio es colombiano o global, sino de su infraestructura. Sitios con balanceo de carga dinámico (eltiempo.com: 32s, github.com: 41s, mercadolibre.com.co: 55s) fuerzan revalidación constante porque sus IPs pueden cambiar en cualquier momento. Mi sitio en GitHub Pages tiene TTL de ~54 minutos porque su infraestructura es estática y las 4 IPs casi nunca cambian.