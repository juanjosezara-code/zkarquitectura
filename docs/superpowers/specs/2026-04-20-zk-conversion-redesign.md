# ZK Arquitectura — Rediseño para Conversión

**Fecha:** 2026-04-20
**Tipo:** Mejora de sitio existente (index.html)
**Objetivo:** Aumentar conversión (visita → contacto WhatsApp) con impacto visual premium

---

## Contexto

Sitio actual: single-page HTML/CSS/JS, ya tiene estructura sólida, branding ZK (#2471C0 azul, Bebas Neue + Josefin Sans), portafolio con 12 proyectos reales y lightbox funcional.

**Problema identificado:** El hero no engancha en los primeros 3 segundos. El titular actual ("DISEÑO. OBRA. LLAVE.") es poderoso para quien ya conoce ZK, pero abstracto para un visitante nuevo.

**Público objetivo:** Familias en Santiago que quieren remodelar, construir un quincho o un local comercial. Buscadores visuales — deciden por imagen antes que por texto.

**Flujo de conversión deseado:** Hero impactante → ver proyectos → contactar por WhatsApp.

---

## 1. Hero Cinematográfico Full-Screen

### Descripción
Reemplaza el split-layout actual (45% oscuro + 55% imagen) por un hero de pantalla completa donde la foto de `Quincho Av. Las condes.jpg` ocupa el 100% del viewport.

### Overlay
Degradado horizontal: `linear-gradient(to right, rgba(26,26,26,0.85) 0%, rgba(26,26,26,0.45) 55%, rgba(26,26,26,0.1) 100%)`. La foto respira a la derecha, el texto se lee perfectamente a la izquierda.

### Contenido (alineado a la izquierda, verticalmente centrado)
1. **Etiqueta** (Bebas Neue, 12px, letter-spacing 4px, color #2471C0): `SANTIAGO · CHILE · DESDE 2009`
2. **Titular principal** (Bebas Neue, clamp(52px, 7vw, 95px), blanco): `TRANSFORMA TU ESPACIO`
3. **Titular secundario** (Josefin Sans italic, clamp(28px, 3.5vw, 48px), #2471C0): `sin intermediarios.`
4. **Subtítulo** (Inter 300, 16px, rgba(255,255,255,0.75), line-height 1.6): `Diseñamos y construimos tu proyecto completo. Remodelaciones, quinchos y locales comerciales en Santiago.`
5. **CTAs en fila**:
   - Primario: botón verde WhatsApp `COTIZAR POR WHATSAPP →` (background #25d366, icono SVG WhatsApp inline)
   - Secundario: link texto `Ver proyectos ↓` (blanco, hover azul ZK)
6. **Stats** (en la parte inferior izquierda del hero, con separadores ·): `+15 AÑOS · +30 PROYECTOS · LLAVE EN MANO`

### Imagen de fondo
- `object-fit: cover`, `object-position: center 40%` para preservar la parte más atractiva de la foto (estructura del quincho, no el cielo)

### Mobile
- Overlay más oscuro: `rgba(26,26,26,0.72)` uniforme
- Texto centrado
- CTAs en columna (WhatsApp arriba, Ver proyectos abajo)
- Height: `100svh` (usa svh para evitar el problema del 100vh en Safari mobile)

---

## 2. Franja de Proyectos Destacados

### Posición
Reemplaza la barra de servicios azul actual. Va inmediatamente después del hero.

### Descripción
Grid horizontal de 3 proyectos seleccionados (uno por categoría) que actúa como puente visual hacia el portafolio completo.

### Proyectos seleccionados
- `Quincho Lomas de la Dehesa.jpg` — categoría: quincho
- `Cocina_Av.Kennedy.jpg` — categoría: remodelacion
- `Restaurant texas ribs.png` — categoría: comercial

### Comportamiento
- Altura fija: `280px` en desktop
- Al hover: overlay azul ZK semitransparente (`rgba(36,113,192,0.8)`) con nombre del proyecto y `→`
- Al hacer clic: scroll suave a `#portafolio` + activa el filtro de esa categoría automáticamente
- Transición: `0.3s ease`

### Mobile
- Scroll horizontal con `overflow-x: auto`, cada item `min-width: 75vw`
- Indicador visual de que hay más items (sombra derecha)

### La barra de servicios azul
Se mantiene pero se mueve para quedar **después** de la franja de proyectos destacados, antes del portafolio completo.

---

## 3. CTA Post-Portafolio

### Posición
Bloque nuevo justo después del grid de portafolio, antes de la sección Proceso.

### Descripción
Franja oscura (`#1a1a1a`) con texto centrado y botón WhatsApp:
- Texto pequeño (Bebas Neue, 12px, azul ZK): `¿TE GUSTÓ LO QUE VES?`
- Titular (Bebas Neue, clamp(32px, 4vw, 52px), blanco): `COTIZA TU PROYECTO HOY`
- Botón WhatsApp verde (mismo estilo que `.whatsapp-cta` existente)

### Lógica de conversión
Captura al visitante en el momento de máximo interés — justo después de revisar los proyectos.

---

## 4. Tooltip WhatsApp Flotante

### Descripción
El botón flotante de WhatsApp (`.whatsapp-btn`) existente agrega un tooltip `"¿Cotizar proyecto?"` que:
- Aparece automáticamente a los 8 segundos del primer cargado de página
- Se anima con `fade-in + slide-left` (150ms ease-out)
- Desaparece si el usuario hace hover sobre el botón o después de 6 segundos
- No vuelve a aparecer en esa sesión (usa `sessionStorage`)

### Estilos
- Posición: a la izquierda del botón flotante
- Background: `#1a1a1a`, color blanco, border-radius 4px, padding 8px 14px
- Flecha pequeña apuntando hacia la derecha (pseudo-elemento `::after`)

---

## 5. Testimonios con Imagen de Fondo

### Descripción
Cada tarjeta de testimonio agrega una foto de proyecto como fondo muy sutil (`opacity: 0.06`) para romper la monotonía visual de las tarjetas grises planas.

- Testimonio 1 (remodelación): fondo `Cocina Callao.png`
- Testimonio 2 (quincho): fondo `Quincho Vitacura.png`
- Testimonio 3 (local): fondo `Restaurant texas ribs.png`

---

## Archivos a Modificar

| Archivo | Cambio |
|---------|--------|
| `index.html` | CSS: hero, franja proyectos, CTA post-portafolio, tooltip, testimonios |
| `index.html` | HTML: nueva estructura hero, franja proyectos, bloque CTA, tooltip |
| `index.html` | JS: clic en franja activa filtro, tooltip con sessionStorage, auto-hide |

Sin nuevos archivos. Todo embebido en `index.html`.

---

## Imágenes a Usar

Todas ya existen en `img/`:
- Hero bg: `Quincho Av. Las condes.jpg`
- Franja: `Quincho Lomas de la Dehesa.jpg`, `Cocina_Av.Kennedy.jpg`, `Restaurant texas ribs.png`
- Testimonios bg: `Cocina Callao.png`, `Quincho Vitacura.png`, `Restaurant texas ribs.png`
