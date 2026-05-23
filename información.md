# Información del Proyecto — Control de Acceso Vehicular

## Parcelación Cielo Campestre

---

## 1. Descripción de la Solución

Sistema de control de acceso vehicular remoto para ~30 propietarios. El residente puede ver la cámara desde su celular, verificar quién solicita ingreso y accionar la apertura del motor de la puerta vehicular desde cualquier lugar con internet. La puerta se cierra automáticamente mediante temporizador interno del relay.

### Diagrama de la Solución

```
[INTERNET]
    │
    └── [CABLE UTP Cat6 · 15 m subterráneo en tubo conduit PVC ½"]
              │
         [ROUTER TP-Link AX12 · WiFi 6]
              │  (LAN)
         [SHELLY PRO 2 · relay WiFi/LAN · riel DIN]
              │                │
         CH1: Abrir        CH2: Cerrar (auto-timer)
              └──────┬──────────┘
                     │
              [MOTOR PUERTA VEHICULAR]

         [CÁMARA EZVIZ HB8C · WiFi 6 + 4G backup · panel solar]
              └── app EZVIZ → residente visualiza antes de abrir

Todo alojado en GABINETE ESTANCO IP66 (300×400×200 mm)
con riel DIN, breaker 10 A, relay Shelly, borneras y prensaestopas.
Alimentado por cable encauchetado 3×12 AWG · 12 m · circuito 15 A · 110 V.
```

**Flujo de uso:**

1. Visitante llega a la puerta → residente recibe notificación en app EZVIZ
2. Residente visualiza cámara en tiempo real (audio bidireccional incluido)
3. Residente decide abrir → envía comando vía app Shelly (internet o WiFi local)
4. Relay CH1 activa motor → puerta abre
5. Temporizador Shelly envía comando a CH2 → puerta cierra automáticamente
6. Sin datos móviles: el residente se conecta al WiFi de portería y abre localmente

---

## 2. Equipos Principales

### 2.1 Relay Inteligente — Shelly Pro 2

| Atributo | Detalle |
|---|---|
| Modelo | Shelly Pro 2 (Wi-Fi / LAN / 2-Channel Smart Relay) |
| Ref. MercadoLibre | MCO1869002607 / producto MCO2057389778 |
| Canales | 2 (CH1 = apertura, CH2 = cierre con timer) |
| Corriente máx. | 16 A por canal / 25 A total |
| Voltaje | 110–240 V CA, 50/60 Hz |
| Conectividad | Wi-Fi 802.11 b/g/n + Ethernet/LAN + Bluetooth |
| Montaje | Riel DIN |
| Salida | Contactos secos (libre de potencial) |
| Temp. operación | -20 °C a +40 °C |
| Consumo propio | < 3 W |
| App | Shelly Cloud (iOS / Android) |
| Funciones clave | Timer autoclose, acceso multiusuario (30 residentes), webhooks, programación horaria |
| Precio Colombia | **A confirmar** en MercadoLibre (acceso bloqueado para scraping) |
| Referencia precio | ~USD $50–60 ≈ COP $200.000–$245.000 |

---

### 2.2 Gabinete Estanco — Precision PST-3040-20A

| Atributo | Detalle |
|---|---|
| Modelo | PST-3040-20A PRECISION |
| Distribuidor | SYSCOM Colombia |
| URL | syscomcolombia.com/producto/PST-3040-20A-PRECISION-154656.html |
| Dimensiones | 300 × 400 × 200 mm (An × Al × Pr) |
| Material | Acero con pintura poliéster en polvo |
| Protección | IP66 / IK10 |
| Peso | 7,07 kg |
| Incluye | Placa trasera galvanizada, cerradura con llave, compuerta inferior atornillable |
| Stock | 337 unidades disponibles |
| Precio | **A confirmar** (requiere login SYSCOM Colombia) |

---

### 2.3 Riel DIN 35 mm × 1 m

| Atributo | Detalle |
|---|---|
| Modelo | PST-RD-1M-PRECISION |
| Distribuidor | SYSCOM Colombia / MercadoLibre (ref. MCOU2426869974) |
| Dimensiones | 35 × 7,5 × 1,0 mm · longitud 1 m |
| Material | Acero cold-rolled, recubrimiento zinc-cromo |
| Uso | Se corta a ≈ 30 cm según ancho del gabinete |
| Precio | **A confirmar** |

---

### 2.4 Breaker / Taco Riel DIN 1 Polo — 10 A (confirmado)

| Atributo | Detalle |
|---|---|
| Función | Protección circuito de alimentación del gabinete |
| Tipo | Breaker unipolar, montaje riel DIN |
| Amperaje | **10 A** |
| Ref. MercadoLibre | MCOU3201225777 |
| Marca referencia | LUMEK (6 kA ruptura, curva C, 110/240 V) |
| Precio referencia | ~COP $13.000 por unidad |

---

### 2.5 Cámara EZVIZ HB8C Lite 4G + Panel Solar 5 W

| Atributo | Detalle |
|---|---|
| Modelo | EZVIZ HB8C Lite (CS-HB8c-SP-R100) |
| Ref. MercadoLibre | MCO1861929101 / producto MCO66707828 |
| Resolución | 4 MP / 2K+ (2560 × 1440) |
| Conectividad | Wi-Fi 6 (2,4 GHz) + 4G LTE backup automático |
| Cobertura | 360° panorámica (340° pan + 80° tilt) |
| Visión nocturna | Color hasta 15 m / IR 15 m |
| Batería | 5.200 mAh recargable |
| Panel solar | Incluido — 5 W (2 h sol = 5 días batería) |
| Autonomía | Hasta 210 días |
| Detección IA | Humanos y vehículos |
| Seguimiento | Automático (auto-tracking) |
| Audio | Bidireccional (micrófono + parlante integrados) |
| App | EZVIZ (iOS / Android) |
| Disuasión activa | Sirena + luz estroboscópica |
| Protección | Apta para intemperie |
| Conectividad activa | **Solo WiFi** (sin SIM por el momento) |
| Precio Colombia | **A confirmar** en MercadoLibre (acceso bloqueado) |
| Referencia precio | ~USD $90–120 ≈ COP $370.000–$490.000 |

---

### 2.6 Router TP-Link Archer AX12 — Wi-Fi 6 AX1500

| Atributo | Detalle |
|---|---|
| Modelo | Archer AX12 AX1500 |
| Ref. MercadoLibre | MCO2840634708 / producto MCO27818723 |
| Velocidad | 1.5 Gbps (1201 Mbps 5 GHz + 300 Mbps 2,4 GHz) |
| Estándar | Wi-Fi 6 (802.11ax), dual band |
| Antenas | 4 fijas con beamforming |
| Puertos | 1× WAN Gigabit + 3× LAN Gigabit |
| Seguridad | WPA3 |
| Modos | Router / Access Point |
| App | TP-Link Tether |
| Garantía | 1 año fabricante |
| **Precio** | **COP $128.000** (oferta Tecnoplaza) / $300.000 regular |
| Envío | Gratis, 1–3 días hábiles (Tecnoplaza Colombia) |

---

### 2.7 Tubos Conduit PVC ½" × 3 m

| Atributo | Detalle |
|---|---|
| Referencia | Homecenter SKU 04651 (Pavco Wavin) |
| Diámetro | ½ pulgada |
| Longitud por tubo | 3 metros |
| Material | PVC, no conductor, autoextinguible |
| Cantidad requerida | 5 tubos (para cubrir 15 m subterráneos) |
| **Precio unitario** | **~COP $4.690** |
| **Precio 5 unidades** | **~COP $23.450** |
| Disponible en | Homecenter Colombia |

---

### 2.8 Borneras de Paso Riel DIN — 8 AWG (41 A)

| Atributo | Detalle |
|---|---|
| Ref. MercadoLibre | MCO1498994935 / MCOU2619747919 |
| Tipo | Bornera atornillable, tipo riel DIN |
| Corriente máx. | 41 A (variante de 57 A también disponible) |
| Calibre | 8 AWG / 6,0 mm² |
| Voltaje | 750 V CA |
| Cuerpo | Poliamida PA6.6V2 |
| **Precio unitario** | **~COP $3.700** |
| **Pack x3** | **~COP $11.100** |

---

## 3. Consumibles (especificaciones confirmadas)

| # | Ítem | Especificación | Cant. | Precio unit. | Subtotal COP |
|---|------|---------------|-------|-------------|--------------|
| 1 | Cable UTP Cat6 100% cobre | Interior, por metro | 15 m | $2.600 | **$39.000** |
| 2 | Conectores RJ45 Cat6 ponchables | Pack × 50 unidades | 1 pack | $16.800 | **$16.800** |
| 3 | Cable encauchetado 3×12 AWG | 110 V, cert. RETIE, por metro | 12 m | $10.600 | **$127.200** |
| 4 | Cable THHN #14 AWG (cableado interno rack) | Por metro, varios colores | 8 m | $2.203 | **$17.624** |
| 5 | Cable THHN #14 AWG (control motor: 5 conductores × 3 m) | Por metro (5 colores × 3 m = 15 m) | 15 m | $2.203 | **$33.045** |
| 6 | Correas plásticas negras × 100 | Dexson 20 cm, nylon negro UV | 1 pack | $9.200 | **$9.200** |
| 7 | Prensaestopas PG16 | Dexson 5/8", con tuerca, IP68 | 4 und | $2.741 | **$10.964** |
| 8 | Tubos conduit PVC ½" × 3 m | Pavco Wavin, Homecenter | 5 und | $4.690 | **$23.450** |
| | | | | **SUBTOTAL** | **$277.283** |

> **Notas consumibles:**
> - Cable THHN #14 AWG control motor: 5 conductores × 3 m para llevar señales del relay Shelly (CH1 COM/NO, CH2 COM/NO + común) a la tarjeta del motor. Ajustar distancia si el motor queda más lejos.
> - Cable THHN #14 AWG rack: mínimo 3 colores para identificación (rojo/negro/verde).
> - Conectores RJ45: el pack × 50 cubre los 2 extremos del tramo + repuestos.
> - 4 prensaestopas: alimentación eléctrica + cable UTP + cable hacia motor + 1 adicional para cámara.

---

## 4. Datos técnicos confirmados

| Pregunta | Respuesta confirmada |
|---|---|
| Tipo de cable UTP | Cat6, 100% cobre |
| Longitud cable UTP subterráneo | 15 metros |
| Cable exterior alimentación | Encauchetado 3×12 AWG, 12 metros |
| Voltaje alimentación | 110 V |
| Breaker circuito de alimentación | 15 A (desde tablero de la casa) |
| Cable interno rack | THHN #14 AWG |
| Correas de amarre | Negras × 100 und (incluir en presupuesto) |
| Prensaestopas gabinete | 4 unidades PG16 |
| Conectores RJ45 | Incluir (pack × 50 Cat6) |
| Conectividad cámara | Solo WiFi (sin SIM 4G por el momento) |
| Amperaje breaker interno rack | **10 A** |
| Mano de obra | Listado de actividades con costos a definir |

---

## 5. Resumen de Precios de Equipos

| Ítem | Precio COP | Fuente | Estado |
|------|-----------|--------|--------|
| Shelly Pro 2 (relay 2CH DIN) | A confirmar | MercadoLibre CO | Est. $200k–$245k |
| Gabinete IP66 PST-3040-20A | A confirmar | SYSCOM Colombia | Requiere login |
| Riel DIN 35 mm × 1 m | A confirmar | SYSCOM / MercadoLibre | — |
| Breaker 1P 10 A riel DIN | ~$13.000 | Interelectricos.com.co | Referencia |
| Cámara EZVIZ HB8C + solar | A confirmar | MercadoLibre CO | Est. $370k–$490k |
| Router TP-Link AX12 | **$128.000** | Tecnoplaza Colombia | Confirmado |
| Borneras DIN 8AWG (pack × 3) | **$11.100** | MercadoLibre | Confirmado |
| Tubos conduit ½" (× 5 und) | **$23.450** | Homecenter | Confirmado |
| Consumibles varios | **$244.238** | Varios | Confirmado |

---

## 6. Actividades de Instalación (Mano de Obra)

Lista para asignación de costos por el cliente:

| # | Actividad | Unidad |
|---|-----------|--------|
| 1 | Replanteo y trazado de ruta subterránea (15 m) | 25.000 |
| 2 | Excavación de zanja para tubería conduit (15 m × 40 cm prof.) | 100.000 |
| 3 | Instalación de tubería conduit PVC ½" subterránea (15 m) | 25.000 |
| 4 | Tendido de cable UTP Cat6 por tubería (15 m) | 25.000 |
| 5 | Ponchado y certificación de conectores RJ45 (2 extremos) | 25.000 |
| 6 | Relleno, compactación y acabado de zanja | 50.000 |
| 7 | Instalación y fijación del gabinete estanco IP66 en muro o poste | 70.000 |
| 8 | Montaje de riel DIN y componentes dentro del gabinete (breaker, relay, borneras, prensaestopas) | 250.000 |
| 9 | Tendido de cable encauchetado 3×12 AWG (12 m, desde tablero hasta gabinete) | 25.000 |
| 10 | Conexión al tablero eléctrico principal (breaker 15 A) | 50.000 |
| 11 | Instalación y configuración del router TP-Link AX12 | 50.000 |
| 12 | Configuración del relay Shelly Pro 2 (WiFi, modo roller shutter, timer autoclose, 30 usuarios) | 150.000 |
| 13 | Conexión del relay Shelly al motor de la puerta vehicular | 30.000 |
| 14 | Instalación y montaje de la cámara EZVIZ HB8C + panel solar | 50.000 |
| 15 | Configuración de la cámara EZVIZ (WiFi, app, compartir acceso a residentes) | 50.000 |
| 16 | Pruebas generales del sistema (apertura, cierre, timer, video, notificaciones) | 25.000 |
| 17 | Video-Capacitación a administración y residentes (uso apps Shelly + EZVIZ) | 60.000 |

---

ToDo: Hay que considerar el cable de control de 5 lineas calibre 14 para la conexion de la ectronica a la targeta del motor

*Documento borrador — versión 2.0 — Mayo 2026*
*Elaborado por: Juan Pablo Palacio Villa — C.C. 1.035.833.895*
