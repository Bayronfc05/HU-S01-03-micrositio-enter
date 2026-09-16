# Experimento X5 — Inspección del Certificado TLS/SSL

**Dominio analizado:** `bayronfc05.github.io`
**Herramienta utilizada:** OpenSSL (`openssl s_client`)

## Resumen

Este experimento documenta el apretón de manos (*handshake*) criptográfico y la cadena de certificados devuelta por el servidor al establecer una conexión TLS con el micrositio alojado en GitHub Pages. Se analiza la jerarquía de confianza, los algoritmos de cifrado negociados y las propiedades de seguridad del canal.

---

## 1. Salida real del comando `openssl s_client`

```text
CONNECTED(000001F0)
depth=3 C=US, O=Internet Security Research Group, CN=ISRG Root X1
verify return:1
depth=2 C=US, O=ISRG, CN=Root YR
verify return:1
depth=1 C=US, O=Let's Encrypt, CN=YR1
verify return:1
depth=0 CN=*.github.io
verify return:1
---
Certificate chain
 0 s:CN=*.github.io
   i:C=US, O=Let's Encrypt, CN=YR1
   a:PKEY: RSA, 2048 (bit); sigalg: sha256WithRSAEncryption
   v:NotBefore: Aug  2 23:38:02 2026 GMT; NotAfter: Oct 31 23:38:01 2026 GMT
 1 s:C=US, O=Let's Encrypt, CN=YR1
   i:C=US, O=ISRG, CN=Root YR
   a:PKEY: RSA, 2048 (bit); sigalg: sha256WithRSAEncryption
   v:NotBefore: Sep  3 00:00:00 2025 GMT; NotAfter: Sep  2 23:59:59 2028 GMT
 2 s:C=US, O=ISRG, CN=Root YR
   i:C=US, O=Internet Security Research Group, CN=ISRG Root X1
   a:PKEY: RSA, 4096 (bit); sigalg: sha256WithRSAEncryption
   v:NotBefore: May 13 00:00:00 2026 GMT; NotAfter: Sep  2 23:59:59 2032 GMT
---
Server certificate
subject=CN=*.github.io
issuer=C=US, O=Let's Encrypt, CN=YR1
---
Peer signing digest: SHA256
Peer signature type: rsa_pss_rsae_sha256
Negotiated TLS1.3 group: X25519MLKEM768
---
SSL handshake has read 5771 bytes and written 1624 bytes
Verification: OK
---
New, TLSv1.3, Cipher is TLS_AES_128_GCM_SHA256
Protocol: TLSv1.3
Server public key is 2048 bit
Verify return code: 0 (ok)
```

---

## 2. Cadena de certificados

La cadena de confianza está compuesta por **3 niveles**, desde el certificado hoja del servidor hasta la raíz global:

| Nivel (depth) | Sujeto (Subject) | Emisor (Issuer) | Rol |
| --- | --- | --- | --- |
| 0 | `CN=*.github.io` | Let's Encrypt (`YR1`) | Certificado del servidor (*leaf*) |
| 1 | `O=Let's Encrypt, CN=YR1` | ISRG (`Root YR`) | CA intermedia |
| 2 | `O=ISRG, CN=Root YR` | ISRG Root X1 | CA raíz |

---

## 3. Desglose técnico de parámetros criptográficos

| Parámetro | Valor Capturado | Significado Técnico |
| --- | --- | --- |
| **Sujeto / Dominio (Subject)** | `CN=*.github.io` | Certificado comodín (*wildcard*) válido para todos los subdominios de `github.io`. |
| **Entidad Emisora (Issuer)** | `O=Let's Encrypt, CN=YR1` | Autoridad Certificadora (CA) intermedia encargada de firmar el certificado del servidor. |
| **Raíz de Confianza (Root CA)** | `ISRG Root X1` | Certificado raíz de la organización *Internet Security Research Group*. |
| **Periodo de Validez** | 2 ago 2026 → 31 oct 2026 | Ventana de validez estándar de 90 días propia de la automatización de Let's Encrypt. |
| **Algoritmo de Firma** | `sha256WithRSAEncryption` | Función hash SHA-256 combinada con cifrado asimétrico RSA. |
| **Tamaño de Llave Pública** | RSA 2048 bits | Longitud de la clave del servidor usada para autenticación y cifrado. |
| **Protocolo Negociado** | `TLSv1.3` | Última versión estándar del protocolo de seguridad de la capa de transporte. |
| **Cifrado Simétrico (Cipher)** | `TLS_AES_128_GCM_SHA256` | Cifrado por bloques AES de 128 bits en modo Galois/Counter (GCM). |
| **Grupo de Intercambio de Llaves** | `X25519MLKEM768` | Intercambio de llaves de curva elíptica con resistencia poscuántica (ML-KEM). |
| **Verificación de Cadena** | `Verify return code: 0 (ok)` | Confirma que la cadena de certificados es válida y confiable en su totalidad. |

---

## 4. Análisis e interpretación técnica

1. **Jerarquía de la cadena de confianza.** El certificado del servidor (`*.github.io`) está firmado por la CA intermedia `Let's Encrypt YR1`, respaldada a su vez por `Root YR`, hasta anclarse finalmente en la raíz mundial `ISRG Root X1`.
2. **Eficiencia del protocolo TLS 1.3.** El canal utiliza TLS 1.3, lo que reduce la negociación del *handshake* a un solo viaje de ida y vuelta (1-RTT) y elimina la posibilidad de renegociar hacia versiones antiguas e inseguras del protocolo.
3. **Resistencia poscuántica.** El uso del grupo híbrido `X25519MLKEM768` evidencia la adopción de algoritmos de intercambio de llaves resistentes a futuras capacidades de computación cuántica, combinando la curva elíptica X25519 con el mecanismo de encapsulamiento de llaves ML-KEM.
4. **Automatización de certificados.** El corto periodo de validez (90 días) es característico de la infraestructura de Let's Encrypt, que favorece la renovación automática frente a certificados de larga duración.

---

## 5. Glosario de términos

| Término | Definición breve |
| --- | --- |
| **CA (Certificate Authority)** | Entidad que emite y firma certificados digitales. |
| **CN (Common Name)** | Campo del certificado que identifica el dominio protegido. |
| **Handshake TLS** | Proceso de negociación inicial entre cliente y servidor para establecer una conexión cifrada. |
| **RTT (Round Trip Time)** | Tiempo de ida y vuelta de un mensaje entre cliente y servidor. |
| **ML-KEM** | Mecanismo de encapsulamiento de llaves basado en criptografía poscuántica (*Module-Lattice-based KEM*). |

---

## 6. Conclusión

El análisis confirma que el micrositio alojado en GitHub Pages implementa una configuración TLS moderna y robusta: cadena de confianza válida ancorada en ISRG Root X1, protocolo TLS 1.3, cifrado AES-128-GCM y un esquema híbrido de intercambio de llaves con resistencia poscuántica. La verificación (`Verify return code: 0`) certifica que no existen anomalías en la cadena de certificación al momento de la conexión.