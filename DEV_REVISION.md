# DEV_REVISION.md — Vertix Landing Page

**Auditor:** QA Developer (Subagent)  
**Fecha:** 2026-03-30  
**Archivo:** `index.html` (1047 líneas, ~30KB)

---

## SCORES

| Categoría | Score | Notas |
|-----------|-------|-------|
| **Performance** | **6.5 / 10** | Fonts bloqueantes, sin lazy load, CSS inline enorme |
| **Accesibilidad** | **6 / 10** | Faltan alt texts, focus states, skip links |
| **SEO** | **7.5 / 10** | Meta tags completos, falta schema.org y headings estrictos |
| **Calidad HTML** | **4 / 10** | HTML roto: orphan divs, elementos huérfanos, duplicate keyframes |
| **Calidad CSS** | **5 / 10** | Variables indefinidas, duplicados, specificity Issues |

---

## TOP 5 ISSUES CRÍTICOS

### 🔴 ISSUE #1 — HTML Roto: Orphan closing tags + estructura inválida

**Ubicación:** Líneas ~977-979, y dentro de `<section class="faq">` (líneas 698-815)

**Descripción:**
1. Dentro de `section.faq` hay `div.recursos-grid`, `div.app-features` y `div.recursos-cta` que **NO deberían estar ahí**. Son contenido de la sección Recursos, no del FAQ.
2. Después de `</main>` hay dos `</div></div>` huérfanas que no cierran ningún contenedor abierto.
3. La estructura de divs está rota: el FAQ tiene un `div.container` que envuelve contenido mixto (FAQ items + Recursos cards + App features).

**W3C Impact:** Esto causa que el parser del browser "adivine" cómo cerrar los tags, generando un DOM impredecible.

**Fix:**
```html
<!-- QUITAR de dentro de section.faq (líneas ~698-815) todo esto:
    <div class="recursos-grid">...</div>
    <div class="app-features">...</div>
    <div class="recursos-cta">...</div>
  y el cierre </section> del FAQ debe llegar INMEDIATAMENTE después de la faq-grid -->
```

Estructura correcta para el FAQ:
```html
<section class="faq" id="faq">
  <div class="container">
    <div class="section-header">
      <div class="section-label">FAQ</div>
      <h2 class="section-title">Preguntas Frecuentes</h2>
    </div>
    <div class="faq-grid">
      <!-- TODOS los <details> FAQ items aquí -->
    </div>
  </div>
</section>
<!-- Aqui YA NO va nada más dentro de section.faq -->
```

Y eliminar las líneas huérfanas `</div></div>` antes de `<section id="privacidad">`:
```html
  </main>
  <!-- ELIMINAR ESTAS DOS LÍNEAS: -->
  <!-- </div> -->
  <!-- </div> -->
  
  <section id="privacidad" class="legal-section">
```

---

### 🔴 ISSUE #2 — CSS Variables INDEFINIDAS (fallback silencioso)

**Ubicación:** `:root` define 12 variables, pero se usan 4 que NO existen:

| Variable usada | ¿Definida? | Valor efectivo |
|---|---|---|
| `--surface` | ❌ NO | hereda del body |
| `--text-secondary` | ❌ NO | hereda del body |
| `--primary-dark` | ❌ NO | hereda del body |
| `--secondary` | ❌ NO | hereda del body |

**Líneas afectadas:** 152, 155-157, 160, 162, 165, 168, 242, 244, 251

**Impacto:** Los elementos que usan `--surface` (background de `.recursos`, `.recurso-tag`, `.app-screenshot-placeholder`) reciben `undefined` y heredan del body. El diseño oscuro de la sección Recursos NO se ve como se esperaba.

**Fix — Agregar en `:root`:**
```css
:root {
  /* ... variables existentes ... */
  --surface: #F3F4F6;
  --text-secondary: #4B5563;
  --primary-dark: #0A1E33;
  --secondary: #10B981; /* verde que coincide con los badges de recurso */
}
```

---

### 🔴 ISSUE #3 — Duplicados en CSS + Keyframes vacíos

**Ubicación:** Líneas 147-148

```css
@keyframes faqFadeIn
@keyframes faqFadeIn
```

**Problema:** 
1. `@keyframes faqFadeIn` está DEFINIDO DOS VECES consecutivas (y ambas están vacías — no tienen ninguna propiedad `from/to`)
2. La animación `.faq-a { animation: faqFadeIn 0.3s ease forwards; }` nunca se aplica
3. Los `@keyframes` vacíos son inválidos según la spec CSS

**Fix — Eliminar las líneas 147-148 y agregar el keyframe correcto:**
```css
@keyframes faqFadeIn {
  from { opacity: 0; transform: translateY(-4px); }
  to   { opacity: 1; transform: translateY(0); }
}
```

Además, mover este keyframe al bloque de animación del `.faq-a`:
```css
.faq-a {
  font-size: 14px;
  color: var(--text-light);
  line-height: 1.6;
  padding: 0 24px 20px;
}
details.faq-item[open] .faq-a {
  animation: faqFadeIn 0.3s ease forwards;
}
```

---

### 🟡 ISSUE #4 — Google Fonts bloquea renderizado

**Ubicación:** `<head>` líneas ~27-28

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
```

**Problema:** La fuente se carga de forma síncrona y bloquea el render. El texto se ve sin estilo (FOIT) hasta que carga.

**Fix — Cargar fonts de forma asíncrona:**
```html
<!-- preconnect sí, pero font como preload + display=swap -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="preload" as="style" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap">
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" media="print" onload="this.media='all'">
<noscript>
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap">
</noscript>
```

O mejor aún — usar solo `display=swap` y considerar system fonts como fallback:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet" media="print" onload="this.media='all'">
<noscript>
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap">
</noscript>
```

---

### 🟡 ISSUE #5 — `onclick` inline en lugar de JS Event Delegation

**Ubicación:** Todas los botones "Elegir Plan →" dentro de `.plan-card`

```html
<button class="plan-cta" onclick="window.open('https://t.me/Maukanx', '_blank')">
```

**Problemas:**
1. Mezcla de Concerns — HTML no debería tener lógica de negocio
2. No hay `rel="noopener"` equivalente en `onclick`
3. No hay fallback si JS falla
4. Accessibility: `<button>` sin `type="button"` envía form si está dentro de un form

**Fix — Eliminar todos los `onclick` inline y usar event delegation:**
```javascript
// En el <script> existente, AMPLIAR:
const navToggle = document.querySelector('.nav-toggle');
const navLinks = document.querySelector('.nav-links');
navToggle.addEventListener('click', () => navLinks.classList.toggle('open'));
navLinks.querySelectorAll('a').forEach(link => {
  link.addEventListener('click', () => navLinks.classList.remove('open'));
});

// NUEVO — Delegation para botones de plan
document.addEventListener('click', (e) => {
  const btn = e.target.closest('.plan-cta');
  if (!btn) return;
  e.preventDefault();
  window.open('https://t.me/Maukanx', '_blank', 'noopener,noreferrer');
});
```

Y cambiar los HTML:
```html
<!-- ANTES -->
<button class="plan-cta" onclick="window.open(...)">Elegir Plan →</button>

<!-- DESPUÉS -->
<a href="https://t.me/Maukanx" target="_blank" rel="noopener noreferrer" class="plan-cta">Elegir Plan →</a>
```

---

## LISTA COMPLETA DE FIXES

### HTML Semántico / W3C

| # | Issue | Severidad | Fix |
|---|-------|-----------|-----|
| H1 | Orphan `</div></div>` antes de `<section id="privacidad">` | 🔴 CRÍTICA | Eliminar líneas 978-979 |
| H2 | `div.recursos-grid` + `div.app-features` dentro de `section.faq` | 🔴 CRÍTICA | Mover fuera del FAQ, crear `<section class="recursos">` propio |
| H3 | `<button>` sin `type="button"` | 🟡 MEDIA | Agregar `type="button"` a todos los `<button>` |
| H4 | `footer` fuera de `<main>` (OK semánticamente pero verificar) | 🟢 INFO | Correcto — `footer` fuera de `main` es válido |
| H5 | SVG inline sin `title` o `aria-label` | 🟡 MEDIA | Agregar `<title>` dentro de cada SVG decorativo |
| H6 | `div.hero-content` no tiene contenedor semántico — es solo un `div` | 🟢 BAJA | Cambiar a `<div>` con role o usar `<article>` |

### CSS

| # | Issue | Severidad | Fix |
|---|-------|-----------|-----|
| C1 | `@keyframes faqFadeIn` duplicado y vacío (líneas 147-148) | 🔴 CRÍTICA | Eliminar duplicados, agregar keyframe válido |
| C2 | Variables `--surface`, `--text-secondary`, `--primary-dark`, `--secondary` indefinidas | 🔴 CRÍTICA | Definirlas en `:root` |
| C3 | `.btn-secondary` definido 2 veces con propiedades conflictivas | 🟡 MEDIA | Unificar en una sola regla |
| C4 | `.cta-btn-primary` duplicado (nav + cta-section) con mismos estilos | 🟢 BAJA | Considerar consolidar |
| C5 | `.plan-card:hover` specificity override competitivo | 🟡 MEDIA | Simplificar con transform compositing |
| C6 | CSS enorme (~300 líneas inline en `<head>`) | 🟡 MEDIA | Extraer a archivo `.css` externo |
| C7 | Media queries dispersas sin un orden consistente | 🟢 BAJA | Agrupar todas las `@media` al final del CSS |

### Performance

| # | Issue | Severidad | Fix |
|---|-------|-----------|-----|
| P1 | Google Fonts síncrono (bloquea render) | 🔴 CRÍTICA | `media="print" onload="this.media='all'"` |
| P2 | Sin lazy loading en imágenes | 🟡 MEDIA | Agregar `loading="lazy"` a `<img>` |
| P3 | Sin `preconnect` para recursos externos (Vercel, Telegram) | 🟢 BAJA | Agregar preconnect a dominios de third-party |
| P4 | Inline SVG en lugar de icon fonts o sprite | 🟢 BAJA | SVGs inline están bien para critical icons — no prioritario |
| P5 | ~30KB de HTML con CSS inline | 🟡 MEDIA | Extraer CSS a archivo externo para cacheo de navegador |

### Accesibilidad

| # | Issue | Severidad | Fix |
|---|-------|-----------|-----|
| A1 | Imágenes sin `alt` attribute | 🔴 CRÍTICA | Agregar `alt=""` a emojis decorativos, `alt="..."` a informative |
| A2 | Sin `skip to content` link | 🟡 MEDIA | Agregar link oculto que salte al `<main>` |
| A3 | Sin `focus-visible` custom styles | 🟡 MEDIA | Agregar `outline` custom en `:focus-visible` |
| A4 | `details/summary` sin `aria-expanded` | 🟡 MEDIA | JS para sincronizar `aria-expanded` con estado open |
| A5 | Color contrast: `rgba(255,255,255,0.8)` sobre `var(--primary)` #0F2A4A | 🟢 BAJA | OK — ratio ~7:1 > 4.5:1 ✓ |
| A6 | Color contrast: `var(--text-light)` #6B7280 sobre blanco — ratio ~5.2:1 | 🟢 BAJA | OK — supera 4.5:1 ✓ |
| A7 | `<button>` dentro de `<a>` (plan cards) | 🔴 CRÍTICA | Ver Issue #5 — cambiar a `<a>` |
| A8 | Nav mobile menu sin `aria-expanded` ni `aria-controls` | 🟡 MEDIA | Agregar al botón hamburger |
| A9 | `<section>` sin `<h2>` headings (legal sections) | 🟡 MEDIA | Ya tienen `<h2>` — OK |

### SEO

| # | Issue | Severidad | Fix |
|---|-------|-----------|-----|
| S1 | Sin Schema.org structured data | 🟡 MEDIA | Agregar `LocalBusiness` o `FinancialService` JSON-LD |
| S2 | `<h1>` duplicado — solo 1 por página ✓ | 🟢 INFO | OK — solo 1 h1 |
| S3 | Heading hierarchy: `h1` → `h2` → `h3` (OK) | 🟢 INFO | Verificar que no haya saltos `h2` → `h4` |
| S4 | Canonical y OG tags completos ✓ | 🟢 INFO | Bien implementado |
| S5 | Falta `lang="es"` en `<html>` — ya está ✓ | 🟢 INFO | Bien |
| S6 | Sin `meta name="theme-color"` | 🟢 BAJA | Agregar para mobile browsers |
| S7 | Falta `hreflang` para variantes de idioma | 🟢 BAJA | Solo español — no necesario |

### JavaScript

| # | Issue | Severidad | Fix |
|---|-------|-----------|-----|
| J1 | `onclick` inline en 4 botones de plan | 🔴 CRÍTICA | Reemplazar con event delegation (ver Issue #5) |
| J2 | Mobile nav: `navLinks.querySelectorAll('a')` se ejecuta en cada click | 🟢 BAJA | Cachear el resultado |
| J3 | Sin `e.preventDefault()` en nav links cuando abierto | 🟡 MEDIA | Cuando mobile menu está open, evitar scroll del body |
| J4 | No hay error handling si `navToggle` o `navLinks` son null | 🟢 BAJA | Aunque el HTML siempre los tiene, defensivo sería mejor |
| J5 | Sin `passive` event listener para scroll | 🟢 BAJA | Scroll listeners deberían ser `{ passive: true }` si se agregan |

---

## RECURSOS EXTRAÍDOS DEL FAQ (FIX Estructural)

El contenido que está INCORRECTAMENTE dentro de `section.faq` y debe moverse a su propia sección:

```
<section class="recursos" id="recursos">
  <div class="container">
    <div class="recursos-grid">
      <!-- 7 recurso-cards -->
    </div>
    <div class="app-features">
      <!-- 3 app-features -->
    </div>
    <div class="recursos-cta">
      <!-- CTA text + botón -->
    </div>
  </div>
</section>
```

**Ubicación actual:** Líneas 698-815 (dentro de `<section class="faq">`)  
**Ubicación correcta:** Crear `<section class="recursos" id="recursos">` después de `</section>` del FAQ y antes de `section.cta-section`

---

## RESUMEN DE PRIORIDADES

| Prioridad | Issues | Tiempo estimado |
|-----------|--------|-----------------|
| 🔴 INMEDIATA | H1 (orphan divs), H2 (recursos dentro de faq), C1 (keyframes vacíos), C2 (variables undefined), P1 (font blocking), J1 (onclick inline), A7 (button in anchor) | 1-2 horas |
| 🟡 ESTA SEMANA | P2 (lazy load), A1 (alt texts), A2 (skip link), A8 (aria labels nav), S1 (schema.org), C3 (CSS duplicados) | 2-3 horas |
| 🟢 OPCIONAL | P5 (CSS extraction), C7 (media queries grouping), J2-J5 (JS cleanup) | 1 hora |

---

*Generado por QA Developer Subagent — 2026-03-30*
