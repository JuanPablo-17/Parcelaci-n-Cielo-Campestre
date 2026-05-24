# Registro de cambios — Bucle de renderización del PDF

## v0 — Baseline (estado de entrada al bucle)

Archivo: `propuesta_v0.pdf` (39 563 bytes, 5 páginas).

**Errores de renderización identificados:**

1. **Colisión en pie de página** (págs. 2–5)
   El pie izquierdo (`Juan Pablo Palacio Villa • C.C. 1.035.833.895`) se solapa con el pie central (`Mayo de 2026`). Texto ilegible: `…833.895Mayo de 2026`.

2. **Banda azul superior ausente** en págs. 2–5
   El overlay TikZ del encabezado no se dibuja. Como el texto del encabezado (`Propuesta Económica | Sistema de Control de Acceso Vehicular`) está coloreado en blanco esperando esa banda, queda invisible sobre fondo blanco. Sólo se aprecia un débil `|` en azul claro.

3. **Asimetría en bloque "Presentado a"** (pág. 1)
   Tras retirar la referencia PCC en la fase previa, el bloque derecho del marco gris contiene sólo una línea. Visual desbalanceado pero no es error tipográfico — información fiel al `.md`. **No se intervino** (fidelidad al `.md` prevalece).

---

## v1 — Iteración 1

Archivo: `propuesta_v1.pdf` (39 301 bytes).

**Cambios en `.tex`:**
- `\fancyfoot[C]{Mayo de 2026}` → `\fancyfoot[C]{}` (eliminada redundancia que causaba colisión; la fecha ya aparece en portada y al cierre).

**Resultado:**
- ✅ Colisión del pie resuelta.
- ❌ Banda azul sigue ausente. Las 3 pasadas de compilación no la activaron, lo que descarta que el problema fuese de pases TikZ + `remember picture`.

---

## v2 — Iteración 2

Archivo: `propuesta_v2.pdf` (39 077 bytes).

**Cambios en `.tex`:**
- Añadido `\usepackage{eso-pic}`.
- Removido el overlay TikZ dentro de `\fancyhead[L]`.
- Añadido bloque `\AddToShipoutPictureBG{ \ifnum\value{page}>1 \AtPageUpperLeft{ \put(0,-39.84){\color{azulprincipal}\rule{\paperwidth}{1.4cm}} } \fi }` para dibujar banda full-bleed por hook de shipout.

**Resultado:**
- ❌ Banda azul sigue sin aparecer. El `\put`+`\rule` dentro de `\AddToShipoutPictureBG` no produce salida visible. Log sin errores.

---

## v3 — Iteración 3

Archivo: `propuesta_v3.pdf` (39 296 bytes).

**Cambios en `.tex`:**
- Reemplazado el `\put`+`\rule` por TikZ con `remember picture, overlay` dentro de `\AddToShipoutPictureBG` (mismo patrón que la portada de pág. 1, donde sí funciona).

**Resultado:**
- ❌ Banda azul sigue sin renderizar. Se confirma que TikZ con `remember picture`+`overlay` no funciona desde hooks de shipout en esta configuración (XeLaTeX TeX Live 2023). Sí funciona desde el cuerpo del documento (portada pág. 1).

---

## v4 — Iteración 4 (estado final)

Archivo: `propuesta_v4.pdf` (39 092 bytes) — también copiado a `propuesta.pdf`.

**Cambios en `.tex`:**
- Abandonado el enfoque full-bleed. Eliminado el bloque `\AddToShipoutPictureBG{...}`.
- Reemplazado el encabezado por `\colorbox` que abarca `\headwidth`:
  ```latex
  \fancyhead[L]{%
    \makebox[\headwidth][l]{%
      \colorbox{azulprincipal}{%
        \parbox[c][0.9cm][c]{\dimexpr\headwidth-2\fboxsep\relax}{%
          \color{white}\sffamily\small\textbf{Propuesta Económica}\ \textcolor{azulclaro}{|}\ Sistema de Control de Acceso Vehicular%
        }%
      }%
    }%
  }
  \fancyhead[C]{}
  \fancyhead[R]{}
  ```

**Resultado:**
- ✅ Banda azul superior visible y legible en págs. 2–5.
- ✅ Pie de página sin colisiones.
- ✅ Información del cuerpo del documento exactamente igual a la del `.md` (verificación posterior).
- ⚠️ Trade-off aceptado: la banda no es full-bleed (tiene los márgenes laterales blancos del documento — ~3 cm izq. y ~2,8 cm der.). Esto se debe a que `\headwidth = \textwidth`. Para full-bleed habría que recurrir a manipulaciones de coordenadas absolutas que probaron ser inestables en esta versión de TeX Live.

### Verificación de fidelidad de información (v4 vs `propuesta.md`)

Script ejecutado: búsqueda de cifras y términos clave (cédula, modelos de equipos, longitudes, todos los valores monetarios, fechas, porcentajes, plazos). **Todos presentes en el PDF**.

Búsqueda inversa de elementos retirados del `.md` que NO deben aparecer:
`PCC`, `Válida hasta`, `Junio de 2026`, `Valores expresados`, `IVA incluido`, `Consideraciones y Exclusiones`, `Incluye`, `No incluye`, `Aceptación`, `Firma`, `Sello`, `juanpablopalaciovilla`, `Contacto`. **Ninguno aparece**. Fidelidad confirmada.

### Imperfecciones cosméticas remanentes (no son errores de renderización)

1. **Banda no full-bleed** — trade-off elegido frente a fragilidad del overlay TikZ en shipout.
2. **Nota "Los precios están sujetos…" queda al inicio de pág. 5** — separada visualmente de la tabla de Resumen Económico (pág. 4). Es una decisión automática de paginación de LaTeX; el texto es correcto y legible.
3. **Bloque "Presentado a" de la portada con menos contenido que "Presentado por"** — heredado de la eliminación de PCC, fiel al `.md`. No se rellena para preservar fidelidad.

---

## Resumen de archivos del bucle

| Versión | Archivo | Tamaño | Estado |
|---------|---------|-------:|--------|
| v0 | `propuesta_v0.pdf` | 39 563 B | baseline (con errores) |
| v1 | `propuesta_v1.pdf` | 39 301 B | pie ✅, banda ❌ |
| v2 | `propuesta_v2.pdf` | 39 077 B | banda ❌ (eso-pic+`\put`) |
| v3 | `propuesta_v3.pdf` | 39 296 B | banda ❌ (eso-pic+TikZ) |
| v4 | `propuesta_v4.pdf` | 39 092 B | **final ✅** (colorbox) |
| — | `propuesta.pdf`    | 39 092 B | copia de v4 |
