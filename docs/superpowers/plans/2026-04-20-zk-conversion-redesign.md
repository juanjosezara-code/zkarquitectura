# ZK Conversion Redesign — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Aumentar conversión del sitio ZK reemplazando el hero split por un hero cinematográfico full-screen e incorporando 4 mejoras adicionales de conversión.

**Architecture:** Todo en `index.html` (CSS + HTML + JS embebidos). Sin dependencias nuevas. Las imágenes ya existen en `img/`. Cambios quirúrgicos: reemplazar hero, agregar 3 secciones/elementos nuevos, ajustar CSS testimonios.

**Tech Stack:** HTML5, CSS3 vanilla, JS vanilla. Google Fonts ya cargadas (Bebas Neue, Josefin Sans, Inter).

---

## Archivos a modificar

| Archivo | Sección | Tipo de cambio |
|---------|---------|----------------|
| `index.html` | CSS `.hero`, `.hero-left`, `.hero-right` | Reemplazar |
| `index.html` | HTML `<section class="hero">` | Reemplazar |
| `index.html` | CSS nuevo: `.hero-bg`, `.hero-overlay`, `.hero-content`, etc. | Agregar |
| `index.html` | HTML nuevo: franja proyectos destacados | Agregar (después del hero) |
| `index.html` | CSS nuevo: `.featured-strip` | Agregar |
| `index.html` | HTML nuevo: CTA post-portafolio | Agregar (después del portafolio) |
| `index.html` | CSS nuevo: `.portfolio-cta` | Agregar |
| `index.html` | HTML/CSS nuevo: tooltip WhatsApp flotante | Agregar |
| `index.html` | JS nuevo: tooltip con sessionStorage, franja con filtro | Agregar |
| `index.html` | CSS `.testimonio-card` | Modificar (agregar soporte bg-image) |
| `index.html` | HTML `.testimonio-card` | Modificar (agregar style bg-image) |

---

## Task 1: Hero Cinematográfico Full-Screen

**Files:**
- Modify: `index.html` — CSS sección HERO (líneas ~61–108), HTML `<section class="hero">` (líneas ~381–402)

- [ ] **Step 1: Reemplazar CSS del hero**

Localiza el bloque `/* HERO */` hasta el cierre `@media (max-width: 768px)` del hero y reemplázalo completamente por:

```css
/* HERO */
.hero {
  position: relative;
  min-height: 100svh;
  display: flex;
  align-items: center;
  padding-top: 85px;
  overflow: hidden;
}
.hero-bg {
  position: absolute;
  inset: 0;
  background: url('img/Quincho Av. Las condes.jpg') center 40% / cover no-repeat;
  z-index: 0;
}
.hero-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to right, rgba(26,26,26,0.88) 0%, rgba(26,26,26,0.50) 50%, rgba(26,26,26,0.08) 100%);
  z-index: 1;
}
.hero-content {
  position: relative;
  z-index: 2;
  padding: 60px 80px;
  max-width: 680px;
  color: #fff;
}
.hero-label {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 12px;
  letter-spacing: 4px;
  text-transform: uppercase;
  color: #2471C0;
  margin-bottom: 20px;
}
.hero-content h1 {
  font-family: 'Bebas Neue', sans-serif;
  font-size: clamp(52px, 7vw, 95px);
  line-height: 1;
  text-transform: uppercase;
  margin-bottom: 12px;
}
.hero-content h1 .accent {
  display: block;
  font-family: 'Josefin Sans', sans-serif;
  font-style: italic;
  font-size: clamp(28px, 3.5vw, 48px);
  font-weight: 600;
  color: #2471C0;
  text-transform: none;
  line-height: 1.2;
}
.hero-content .divider { width: 50px; height: 3px; background: #2471C0; margin: 28px 0; }
.hero-content p {
  font-size: 16px;
  color: rgba(255,255,255,0.72);
  line-height: 1.7;
  margin-bottom: 38px;
  max-width: 480px;
}
.hero-buttons { display: flex; align-items: center; gap: 28px; margin-bottom: 60px; flex-wrap: wrap; }
.btn-whatsapp-hero {
  display: inline-flex; align-items: center; gap: 10px;
  padding: 16px 32px; background: #25d366; color: #fff;
  font-family: 'Bebas Neue', sans-serif; font-size: 12px;
  letter-spacing: 3px; text-transform: uppercase;
  transition: background 0.3s; min-height: 44px;
}
.btn-whatsapp-hero:hover { background: #1da851; }
.btn-whatsapp-hero svg { width: 18px; height: 18px; fill: #fff; flex-shrink: 0; }
.btn-ver-proyectos {
  font-family: 'Bebas Neue', sans-serif; font-size: 12px;
  letter-spacing: 3px; text-transform: uppercase;
  color: rgba(255,255,255,0.65); transition: color 0.3s;
}
.btn-ver-proyectos:hover { color: #fff; }
.hero-stats-bar {
  display: flex; align-items: center; gap: 20px; flex-wrap: wrap;
}
.hero-stats-bar span {
  font-family: 'Bebas Neue', sans-serif; font-size: 12px;
  letter-spacing: 3px; text-transform: uppercase; color: rgba(255,255,255,0.45);
}
.hero-stats-bar .sep { color: #2471C0; font-size: 16px; }
@media (max-width: 768px) {
  .hero-content { padding: 50px 24px; text-align: center; max-width: 100%; }
  .hero-overlay { background: rgba(26,26,26,0.72); }
  .hero-buttons { flex-direction: column; align-items: center; gap: 16px; }
  .hero-stats-bar { justify-content: center; }
  .hero-content p { max-width: 100%; }
}
```

- [ ] **Step 2: Reemplazar HTML del hero**

Localiza `<!-- HERO -->` y reemplaza `<section class="hero">...</section>` por:

```html
<!-- HERO -->
<section class="hero">
  <div class="hero-bg"></div>
  <div class="hero-overlay"></div>
  <div class="hero-content">
    <div class="hero-label">SANTIAGO · CHILE · DESDE 2009</div>
    <h1>TRANSFORMA<br>TU ESPACIO<br><span class="accent">sin intermediarios.</span></h1>
    <div class="divider"></div>
    <p>Diseñamos y construimos tu proyecto completo. Remodelaciones, quinchos y locales comerciales en Santiago.</p>
    <div class="hero-buttons">
      <a href="https://wa.me/56966167206?text=Hola%20ZK%2C%20me%20interesa%20cotizar%20un%20proyecto" class="btn-whatsapp-hero" target="_blank" rel="noopener">
        <svg viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
        COTIZAR POR WHATSAPP →
      </a>
      <a href="#portafolio" class="btn-ver-proyectos">Ver proyectos ↓</a>
    </div>
    <div class="hero-stats-bar">
      <span>+15 AÑOS</span>
      <span class="sep">·</span>
      <span>+30 PROYECTOS</span>
      <span class="sep">·</span>
      <span>LLAVE EN MANO</span>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Verificar visualmente**

Abrir `index.html` en el navegador:
- Hero ocupa pantalla completa con foto de quincho
- Degradado oscuro a izquierda, foto visible a derecha
- Titular "TRANSFORMA TU ESPACIO" en blanco grande
- "sin intermediarios." en azul ZK italic debajo
- Botón verde WhatsApp visible y botón "Ver proyectos ↓" en blanco tenue
- En mobile (DevTools 375px): overlay oscuro uniforme, texto centrado, botones en columna

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: hero cinematografico full-screen con foto quincho ZK"
```

---

## Task 2: Franja de Proyectos Destacados

**Files:**
- Modify: `index.html` — agregar CSS `.featured-strip`, agregar HTML entre `</section>` del hero y `<!-- SERVICES BAR -->`, agregar JS al bloque `<script>`

- [ ] **Step 1: Agregar CSS de la franja**

Agregar después del bloque `/* SERVICES BAR */` en el CSS:

```css
/* FEATURED STRIP */
.featured-strip {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  height: 280px;
  overflow: hidden;
}
.featured-item {
  position: relative;
  overflow: hidden;
  cursor: pointer;
}
.featured-item img {
  width: 100%; height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}
.featured-item:hover img { transform: scale(1.05); }
.featured-item .featured-overlay {
  position: absolute;
  inset: 0;
  background: rgba(36,113,192,0.82);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
  color: #fff;
  text-align: center;
  padding: 20px;
}
.featured-item:hover .featured-overlay { opacity: 1; }
.featured-overlay .feat-label {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 11px;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: rgba(255,255,255,0.75);
  margin-bottom: 8px;
}
.featured-overlay .feat-title {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 22px;
  text-transform: uppercase;
  margin-bottom: 10px;
}
.featured-overlay .feat-arrow {
  font-size: 22px;
  color: rgba(255,255,255,0.8);
}
@media (max-width: 768px) {
  .featured-strip {
    display: flex;
    overflow-x: auto;
    scroll-snap-type: x mandatory;
    height: 220px;
    -webkit-overflow-scrolling: touch;
  }
  .featured-strip::-webkit-scrollbar { display: none; }
  .featured-item {
    min-width: 75vw;
    scroll-snap-align: start;
    flex-shrink: 0;
  }
  .featured-item .featured-overlay { opacity: 1; background: rgba(26,26,26,0.55); }
}
```

- [ ] **Step 2: Agregar HTML de la franja**

Insertar entre `</section>` del hero y el comentario `<!-- SERVICES BAR -->`:

```html
<!-- FEATURED STRIP -->
<div class="featured-strip">
  <div class="featured-item" data-filter-target="quincho">
    <img src="img/Quincho Lomas de la Dehesa.jpg" alt="Quincho Lomas de la Dehesa" loading="lazy">
    <div class="featured-overlay">
      <div class="feat-label">Quincho &amp; Terraza</div>
      <div class="feat-title">QUINCHOS</div>
      <div class="feat-arrow">→</div>
    </div>
  </div>
  <div class="featured-item" data-filter-target="remodelacion">
    <img src="img/Cocina_Av.Kennedy.jpg" alt="Cocina Av. Kennedy" loading="lazy">
    <div class="featured-overlay">
      <div class="feat-label">Remodelación</div>
      <div class="feat-title">REMODELACIONES</div>
      <div class="feat-arrow">→</div>
    </div>
  </div>
  <div class="featured-item" data-filter-target="comercial">
    <img src="img/Restaurant texas ribs.png" alt="Restaurant Texas Ribs" loading="lazy">
    <div class="featured-overlay">
      <div class="feat-label">Local Comercial</div>
      <div class="feat-title">LOCALES COMERCIALES</div>
      <div class="feat-arrow">→</div>
    </div>
  </div>
</div>
```

- [ ] **Step 3: Agregar JS para activar filtro al hacer clic**

Agregar dentro del bloque `<script>`, después del bloque de lightbox:

```js
// Featured strip → activa filtro en portafolio
document.querySelectorAll('.featured-item').forEach(item => {
  item.addEventListener('click', () => {
    const target = item.dataset.filterTarget;
    const btn = document.querySelector(`.filter-btn[data-filter="${target}"]`);
    if (btn) {
      btn.click();
      document.getElementById('portafolio').scrollIntoView({ behavior: 'smooth' });
    }
  });
});
```

- [ ] **Step 4: Verificar visualmente**

- Tres fotos en fila de igual altura (280px desktop)
- Hover: overlay azul ZK con nombre de categoría y flecha
- Clic en "QUINCHOS" → scroll a portafolio + filtro "QUINCHOS & TERRAZAS" activo
- Mobile (375px): scroll horizontal tipo carrusel, cada item 75% del ancho

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: franja proyectos destacados con activacion de filtro"
```

---

## Task 3: CTA Post-Portafolio

**Files:**
- Modify: `index.html` — agregar CSS `.portfolio-cta`, agregar HTML entre `</section>` del portafolio y `<!-- PROCESS -->`

- [ ] **Step 1: Agregar CSS**

Agregar después del bloque `/* PROCESS */` en el CSS:

```css
/* PORTFOLIO CTA */
.portfolio-cta {
  background: #1a1a1a;
  padding: 55px 50px;
  text-align: center;
}
.portfolio-cta .pcta-label {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 12px;
  letter-spacing: 4px;
  text-transform: uppercase;
  color: #2471C0;
  margin-bottom: 16px;
}
.portfolio-cta h3 {
  font-family: 'Bebas Neue', sans-serif;
  font-size: clamp(32px, 4vw, 52px);
  text-transform: uppercase;
  color: #fff;
  margin-bottom: 30px;
  line-height: 1.1;
}
@media (max-width: 768px) {
  .portfolio-cta { padding: 45px 24px; }
}
```

- [ ] **Step 2: Agregar HTML**

Insertar entre el `</section>` del portafolio (antes de `<!-- PROCESS -->`) y después del `<!-- LIGHTBOX -->`:

```html
<!-- CTA POST-PORTAFOLIO -->
<div class="portfolio-cta">
  <p class="pcta-label">¿TE GUSTÓ LO QUE VES?</p>
  <h3>COTIZA TU PROYECTO HOY</h3>
  <a href="https://wa.me/56966167206?text=Hola%20ZK%2C%20me%20interesa%20cotizar%20un%20proyecto" class="whatsapp-cta" target="_blank" rel="noopener">
    <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
    ESCRIBIR POR WHATSAPP
  </a>
</div>
```

- [ ] **Step 3: Verificar visualmente**

- Bloque oscuro entre portafolio y proceso
- Texto `¿TE GUSTÓ LO QUE VES?` en azul ZK pequeño
- `COTIZA TU PROYECTO HOY` en blanco grande
- Botón verde WhatsApp centrado

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: CTA post-portafolio con boton WhatsApp"
```

---

## Task 4: Tooltip WhatsApp Flotante

**Files:**
- Modify: `index.html` — agregar CSS para `.whatsapp-tooltip`, modificar HTML del `.whatsapp-btn`, agregar JS con sessionStorage

- [ ] **Step 1: Agregar CSS del tooltip**

Agregar después del bloque `/* WHATSAPP FLOTANTE */` en el CSS:

```css
.whatsapp-wrapper {
  position: fixed;
  bottom: 30px;
  right: 30px;
  z-index: 999;
  display: flex;
  align-items: center;
  gap: 10px;
}
.whatsapp-tooltip {
  background: #1a1a1a;
  color: #fff;
  font-family: 'Bebas Neue', sans-serif;
  font-size: 12px;
  letter-spacing: 2px;
  text-transform: uppercase;
  padding: 10px 16px;
  border-radius: 4px;
  white-space: nowrap;
  opacity: 0;
  transform: translateX(8px);
  transition: opacity 0.2s ease, transform 0.2s ease;
  pointer-events: none;
  position: relative;
}
.whatsapp-tooltip::after {
  content: '';
  position: absolute;
  right: -6px;
  top: 50%;
  transform: translateY(-50%);
  border: 6px solid transparent;
  border-left-color: #1a1a1a;
  border-right: 0;
}
.whatsapp-tooltip.visible {
  opacity: 1;
  transform: translateX(0);
  pointer-events: auto;
}
```

- [ ] **Step 2: Modificar HTML del botón flotante**

Reemplazar el `<a class="whatsapp-btn" ...>` actual por:

```html
<!-- WHATSAPP FLOTANTE -->
<div class="whatsapp-wrapper">
  <span class="whatsapp-tooltip" id="waTooltip">¿COTIZAR PROYECTO?</span>
  <a href="https://wa.me/56966167206?text=Hola%20ZK%2C%20me%20interesa%20cotizar%20un%20proyecto" class="whatsapp-btn" target="_blank" rel="noopener" aria-label="WhatsApp">
    <svg viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
  </a>
</div>
```

Nota: el CSS de `.whatsapp-btn` existente (`position: fixed; bottom: 30px; right: 30px`) debe **eliminarse** o anularse, ya que ahora el posicionamiento fijo lo maneja `.whatsapp-wrapper`.

Agregar al CSS existente de `.whatsapp-btn`:
```css
.whatsapp-btn {
  /* quitar position/bottom/right/z-index — ahora los maneja .whatsapp-wrapper */
  position: static;
  width: 60px; height: 60px; background: #25d366; border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  box-shadow: 0 4px 20px rgba(37,211,102,0.4); transition: transform 0.3s;
  flex-shrink: 0;
}
```

- [ ] **Step 3: Agregar JS del tooltip**

Agregar al final del bloque `<script>`, antes del `</script>`:

```js
// Tooltip WhatsApp flotante
(function() {
  if (sessionStorage.getItem('waTooltipShown')) return;
  const tooltip = document.getElementById('waTooltip');
  const waBtn = document.querySelector('.whatsapp-btn');
  let hideTimer;

  function showTooltip() {
    tooltip.classList.add('visible');
    hideTimer = setTimeout(hideTooltip, 6000);
  }
  function hideTooltip() {
    tooltip.classList.remove('visible');
    clearTimeout(hideTimer);
  }

  setTimeout(showTooltip, 8000);
  waBtn.addEventListener('mouseenter', hideTooltip);
  sessionStorage.setItem('waTooltipShown', '1');
})();
```

- [ ] **Step 4: Verificar visualmente**

- Botón verde flotante en bottom-right permanece igual
- Esperar 8 segundos: aparece tooltip "¿COTIZAR PROYECTO?" a la izquierda del botón con animación slide
- Tooltip desaparece solo a los 6 segundos
- Al hacer hover sobre el botón, tooltip se oculta
- Recargar página: tooltip NO aparece de nuevo (sessionStorage)
- En DevTools Application > Session Storage: clave `waTooltipShown` = `1`

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: tooltip WhatsApp flotante con sessionStorage"
```

---

## Task 5: Testimonios con Imagen de Fondo

**Files:**
- Modify: `index.html` — CSS `.testimonio-card`, HTML de las 3 tarjetas

- [ ] **Step 1: Actualizar CSS de las tarjetas**

Reemplazar el bloque `.testimonio-card` existente por:

```css
.testimonio-card {
  background: #f5f5f5;
  padding: 35px 30px;
  border-top: 3px solid #2471C0;
  position: relative;
  overflow: hidden;
}
.testimonio-card::before {
  content: '';
  position: absolute;
  inset: 0;
  background-size: cover;
  background-position: center;
  opacity: 0.055;
  z-index: 0;
}
.testimonio-card > * { position: relative; z-index: 1; }
.testimonio-card:nth-child(1)::before { background-image: url('img/Cocina Callao.png'); }
.testimonio-card:nth-child(2)::before { background-image: url('img/Quincho Vitacura.png'); }
.testimonio-card:nth-child(3)::before { background-image: url('img/Restaurant texas ribs.png'); }
```

- [ ] **Step 2: Verificar visualmente**

- Cada tarjeta muestra muy sutilmente la textura de un proyecto como fondo
- El texto sigue siendo perfectamente legible (opacity 0.055 es muy baja)
- Los 3 testimonios muestran fondos distintos (cocina, quincho, restaurante)

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: testimonios con imagen de fondo sutil por proyecto"
```

---

## Verificación Final

- [ ] Abrir en Chrome desktop: hero ocupa pantalla completa, flujo hero → franja → portafolio → CTA natural
- [ ] Abrir en Chrome mobile (375px): hero con overlay, texto centrado, franja en scroll horizontal
- [ ] Navegar todo el flujo: hero → franja clic en quincho → scroll portafolio con filtro activo → lightbox → CTA post-portafolio
- [ ] Esperar 8s: tooltip aparece junto al WhatsApp flotante
- [ ] Verificar que testimonios muestran fondo sutil sin afectar legibilidad
