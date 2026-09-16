# Experimento X2 — Trazar la Ruta (`tracert`)

Documentación y análisis del recorrido de los paquetes de red a través de routers
intermedios (saltos) desde la red local en Colombia hasta dos servidores en internet.

---

## 1. Traza a `eltiempo.com` (servidor alojado en Microsoft Azure)

* **Dirección IP destino:** `20.57.95.139`
* **Saltos totales:** 24

```text
Traza a la dirección eltiempo.com [20.57.95.139]
sobre un máximo de 30 saltos:

  1    <1 ms    <1 ms    <1 ms  10.27.124.235
  2    14 ms     6 ms     6 ms  192.168.10.1
  3   201 ms    98 ms    27 ms  192.168.1.254
  4    37 ms    38 ms   152 ms  10.141.109.1
  5    47 ms    37 ms    32 ms  10.166.90.225
  6    45 ms    43 ms    43 ms  10.166.12.26
  7    64 ms    34 ms    25 ms  10.166.12.25
  8    92 ms    20 ms    24 ms  10.44.11.23
  9    28 ms   104 ms    21 ms  10.44.11.0
 10    36 ms   136 ms    45 ms  static-adsl200-24-33-192.epm.net.co [200.24.33.192]
 11   121 ms    27 ms    38 ms  ae67-0.ier02.bog30.ntwk.msn.net [104.44.196.131]
 12   108 ms    97 ms     *     ae30-0.ear04.mia.ntwk.msn.net [104.44.230.216]
 13    90 ms   106 ms   107 ms  be24.ibr01.mia.ntwk.msn.net [104.44.33.169]
 14   260 ms   102 ms   123 ms  be6.ibr01.fll30.ntwk.msn.net [104.44.19.15]
 15   191 ms   308 ms   306 ms  be8.ibr01.atl31.ntwk.msn.net [104.44.16.47]
 16     *      129 ms     *     be3.owr01.atl31.ntwk.msn.net [51.10.3.248]
 17    97 ms    91 ms   117 ms  be5.owr01.atl30.ntwk.msn.net [104.44.55.237]
 18     *        *      266 ms  be1.owr01.lvl01.ntwk.msn.net [104.44.51.190]
 19     *      208 ms     *     po1012.rwa03.lvl01.ntwk.msn.net [104.44.50.122]
 20     *        *        *     Tiempo de espera agotado para esta solicitud.
 21     *        *        *     Tiempo de espera agotado para esta solicitud.
 22     *        *        *     Tiempo de espera agotado para esta solicitud.
 23     *        *        *     Tiempo de espera agotado para esta solicitud.
 24   327 ms    95 ms    86 ms  20.57.95.139

Traza completa.
```

**Dónde sale de Colombia:** el salto 10 (`epm.net.co`, un ISP colombiano — EPM es la
empresa de servicios públicos de Medellín) es el último nodo claramente nacional. El
salto 11 (`bog30`, Bogotá) ya pertenece a la red de Microsoft (`ntwk.msn.net`), y de ahí
en adelante la ruta salta entre ciudades de EE. UU. (Miami → Atlanta → varios nodos más)
antes de llegar al servidor final.

---

## 2. Traza a `bayronfc05.github.io` (GitHub Pages / CDN Fastly)

* **Dirección IP destino:** `185.199.108.153`
* **Saltos totales:** 12

```text
Traza a la dirección bayronfc05.github.io [185.199.108.153]
sobre un máximo de 30 saltos:

  1     1 ms    <1 ms    <1 ms  10.27.124.235
  2    11 ms    12 ms    13 ms  192.168.10.1
  3    16 ms    31 ms    14 ms  192.168.1.254
  4    21 ms    16 ms    13 ms  10.141.109.1
  5    22 ms    29 ms    28 ms  10.166.90.225
  6    33 ms   607 ms    29 ms  10.166.12.26
  7    59 ms    25 ms    28 ms  10.166.12.25
  8    58 ms    27 ms    41 ms  10.44.11.23
  9    34 ms   144 ms    26 ms  10.44.11.0
 10    52 ms    26 ms    31 ms  static-adsl200-24-33-192.epm.net.co [200.24.33.192]
 11     *        *        *     Tiempo de espera agotado para esta solicitud.
 12    60 ms   130 ms    26 ms  cdn-185-199-108-153.github.com [185.199.108.153]

Traza completa.
```

**Dónde sale de Colombia:** igual que en la traza anterior, el salto 10 (`epm.net.co`)
es el último nodo identificable en Colombia. El salto 11 no responde (probablemente un
router que bloquea ICMP, no un error real — los saltos con `*` no siempre significan que
la ruta falló, solo que ese nodo no contesta el ping de diagnóstico). El salto 12 llega
directo al CDN de GitHub (Fastly), sin nodos intermedios visibles en Estados Unidos.

---

## 3. Análisis comparativo

| | eltiempo.com (Azure) | bayronfc05.github.io (GitHub Pages) |
|---|---|---|
| Saltos totales | 24 | 12 |
| Últimos saltos con timeout | 4 (saltos 20-23) | 1 (salto 11) |
| Latencia máxima observada | 327 ms | 130 ms |
| Primeros 9 saltos (red local/ISP) | Idénticos en ambas trazas | Idénticos en ambas trazas |

**Conclusión:** los primeros 9 saltos son exactamente iguales en ambas trazas porque
corresponden a mi propia red local y a la infraestructura de mi ISP en Colombia — el
camino diverge recién en el salto 10, que es donde cada dominio empieza a usar rutas
distintas según dónde esté alojado su servidor.

Mi sitio en GitHub Pages tarda muchos menos saltos (12 vs 24) en llegar a destino que
eltiempo.com. Esto tiene sentido: GitHub Pages se sirve desde una red de distribución de
contenido (CDN) con nodos repartidos globalmente (Fastly), así que probablemente hay un
nodo relativamente cerca de Colombia que responde rápido. eltiempo.com, en cambio, está
alojado en Azure y su tráfico viaja explícitamente a través de la red interna de Microsoft
(`ntwk.msn.net`) saltando por varias ciudades de EE. UU. (Miami, Atlanta, etc.) antes de
llegar al datacenter final — una ruta mucho más larga.