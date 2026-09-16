# Experimento X3 — Medición de Latencia (`ping`)

Documentación y análisis del tiempo de ida y vuelta (RTT - *Round Trip Time*) de paquetes
ICMP hacia 4 destinos distintos desde la red local en Colombia.

---

## 1. Salida real de los comandos

### Destino 1: `eltiempo.com` (servidor Azure)

```text
Haciendo ping a eltiempo.com [20.57.95.139] con 32 bytes de datos:
Respuesta desde 20.57.95.139: bytes=32 tiempo=290ms TTL=106
Respuesta desde 20.57.95.139: bytes=32 tiempo=316ms TTL=106
Respuesta desde 20.57.95.139: bytes=32 tiempo=83ms TTL=106
Respuesta desde 20.57.95.139: bytes=32 tiempo=147ms TTL=106

Estadísticas de ping para 20.57.95.139:
    Paquetes: enviados = 4, recibidos = 4, perdidos = 0
    (0% perdidos),
Tiempos aproximados de ida y vuelta en milisegundos:
    Mínimo = 83ms, Máximo = 316ms, Media = 209ms
```

### Destino 2: `www.gov.co` (portal del Estado colombiano / AWS CloudFront)

```text
Haciendo ping a www.gov.co [13.249.96.2] con 32 bytes de datos:
Respuesta desde 13.249.96.2: bytes=32 tiempo=88ms TTL=241
Respuesta desde 13.249.96.2: bytes=32 tiempo=80ms TTL=241
Respuesta desde 13.249.96.2: bytes=32 tiempo=83ms TTL=241
Respuesta desde 13.249.96.2: bytes=32 tiempo=92ms TTL=241

Estadísticas de ping para 13.249.96.2:
    Paquetes: enviados = 4, recibidos = 4, perdidos = 0
    (0% perdidos),
Tiempos aproximados de ida y vuelta en milisegundos:
    Mínimo = 80ms, Máximo = 92ms, Media = 85ms
```

### Destino 3: `github.com` (servidor global)

```text
Haciendo ping a github.com [140.82.113.4] con 32 bytes de datos:
Respuesta desde 140.82.113.4: bytes=32 tiempo=116ms TTL=39
Respuesta desde 140.82.113.4: bytes=32 tiempo=121ms TTL=39
Respuesta desde 140.82.113.4: bytes=32 tiempo=106ms TTL=39
Respuesta desde 140.82.113.4: bytes=32 tiempo=108ms TTL=39

Estadísticas de ping para 140.82.113.4:
    Paquetes: enviados = 4, recibidos = 4, perdidos = 0
    (0% perdidos),
Tiempos aproximados de ida y vuelta en milisegundos:
    Mínimo = 106ms, Máximo = 121ms, Media = 112ms
```

### Destino 4: `1.1.1.1` (DNS público de Cloudflare)

```text
Haciendo ping a 1.1.1.1 con 32 bytes de datos:
Respuesta desde 1.1.1.1: bytes=32 tiempo=27ms TTL=52
Respuesta desde 1.1.1.1: bytes=32 tiempo=31ms TTL=52
Respuesta desde 1.1.1.1: bytes=32 tiempo=29ms TTL=52
Respuesta desde 1.1.1.1: bytes=32 tiempo=26ms TTL=52

Estadísticas de ping para 1.1.1.1:
    Paquetes: enviados = 4, recibidos = 4, perdidos = 0
    (0% perdidos),
Tiempos aproximados de ida y vuelta en milisegundos:
    Mínimo = 26ms, Máximo = 31ms, Media = 28ms
```

---

## 2. Cuadro resumen de mediciones

| Destino | IP respuesta | Latencia mínima | Latencia máxima | Latencia promedio | Pérdida de paquetes |
|---|---|---|---|---|---|
| `1.1.1.1` (Cloudflare) | `1.1.1.1` | 26 ms | 31 ms | 28 ms | 0% |
| `www.gov.co` (AWS CloudFront) | `13.249.96.2` | 80 ms | 92 ms | 85 ms | 0% |
| `github.com` (global) | `140.82.113.4` | 106 ms | 121 ms | 112 ms | 0% |
| `eltiempo.com` (Azure) | `20.57.95.139` | 83 ms | 316 ms | 209 ms | 0% |

---

## 3. Análisis e interpretación técnica

1. **DNS público `1.1.1.1` (~28 ms promedio)**
   Es el destino con menor latencia y mayor estabilidad. Cloudflare usa enrutamiento
   **Anycast**, respondiendo desde un centro de datos (POP) cercano en la región, sin
   enviar el paquete hasta Estados Unidos.

2. **Diferencia entre `gov.co` y `www.gov.co` (~85 ms promedio):** Al intentar hacer `ping` al dominio raíz (`gov.co`), la solicitud falló. La verificación posterior con `nslookup gov.co` confirmó que el dominio raíz no posee registros de tipo `A` ni `AAAA` asignados. Al consultar el subdominio canónico `www.gov.co`, la consulta resolvió con éxito a la IP `13.249.96.2` (infraestructura CDN de Amazon CloudFront), logrando una respuesta veloz y estable de 85 ms.

3. **`github.com` (~112 ms promedio)**
   Latencia constante (~106-121 ms), correspondiente al tránsito por fibra óptica
   submarina hacia los centros de datos en Estados Unidos.

4. **`eltiempo.com` (~209 ms promedio)**
   La latencia más alta y con mayor variación (jitter de hasta 316 ms). Como se
   evidenció en el Experimento X2, la conexión atraviesa múltiples nodos de la red
   interna de Microsoft Azure en EE. UU. antes de llegar al destino.