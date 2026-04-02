# RECURSOS_DESIGN.md — Vertix Landing Page

## 1. UBICACIÓN RECOMENDADA

**Después de Planes (antes de Perfiles)**

### Por qué:
- El usuario acaba de ver los $149/mes y su reacción mental es "pero qué incluye exactamente?"
- Es el momento de máximo escepticismo sobre el precio — los recursos responden directamente
- Antes de FAQ (que es más defensivo) o del CTA (que es tarde), este es el puente perfecto entre "cuánto cuesta" y "qué gano"
- Flujo: **Planes → Recursos (valor percepción) → Perfiles (prueba social) → FAQ → CTA**

---

## 2. PRESENTACIÓN RECOMENDADA

**Banner destacado + Grid de beneficios con icons** (híbrido)

No cards sueltas porque se diluyen. Un banner hero de recursos que funcione como "shock de valor" — que el usuario vea que $149 = $243 de valor y piense "esto es un robo".

---

## 3. COPY EXACTO

### Header del Banner
```
TODO LO QUE INCLUYE TU SUSCRIPCIÓN
```

### Subheader
```
No solo señales. Todo un sistema para invertir mejor.
```

### Items del Grid (7 recursos)

| Recurso | Valor percibido | Copy |
|---------|-----------------|------|
| App VERTIX | Gratis | "App VERTIX — Tu centro de control 24/7" |
| Guía PDF | Gratis | "Guía: Cómo Invertir desde Cero — Sin experiencia previa" |
| Portfolio Tracker | Gratis | "Portfolio Tracker — Sigue cada activo en tiempo real" |
| Comunidad Privada | $19/mes | "Comunidad Privada — Inversionistas como tú" |
| Trading Bots | $97/mes | "Trading Bots — Automatiza tus estrategias" |
| Talleres | $49/mes | "Talleres Mensuales — Aprende haciendo" |
| Estrategias PDF | $29/mes | "Estrategias PDF — Plays concretas para cada escenario" |

### Value Stack Line (el gancho)
```
Valor total: $243 → Tu precio: $149/mes
```

### Microcopy de urgencia/social proof
```
✓ Incluido para siempre | ✓ Sin coste adicional | ✓ Cancela cuando quieras
```

---

## 4. DISEÑO VISUAL

### Estructura general
- **Contenedor:** max-width 1200px, centrado
- **Fondo:** gradiente sutil verde oscuro (#0A1A12 → #0D2318) para diferenciarse de la sección Planes
- **Padding vertical:** 80px top, 80px bottom

### Header
- **Eyebrow tag:** "INCLUIDO EN TUS $149/MES" — texto small caps, verde claro (#4ADE80), letraspaciado 3px
- **H2:** "Todo lo que incluye tu suscripción" — font-size 40px, font-weight 700, blanco
- **Subheader:** "No solo señales. Todo un sistema para invertir mejor." — 18px, gris claro (#9CA3AF)

### Grid de recursos (3 columnas desktop, 2 tablet, 1 móvil)
- **Gap:** 24px
- **Card:** fondo #111D14 (verde muy oscuro), border 1px #1F3A28, border-radius 16px
- **Hover:** border cambia a verde (#22C55E), box-shadow verde sutil
- **Icon:** 40x40px, fondo #1A3A1C, border-radius 10px, icono verde
- **Nombre recurso:** 16px, font-weight 600, blanco
- **Descripción:** 13px, gris (#9CA3AF)
- **Badge de valor:** posición absolute top-right, fondo #22C55E, texto negro, font-weight 700, font-size 11px, padding 4px 8px, border-radius 6px

### Value Stack Banner (prominente, debajo del grid)
- **Fondo:** #1A3A1C (verde oscuro)
- **Border:** 2px solid #22C55E
- **Border-radius:** 16px
- **Layout:** flex row, alineado centro
- **Texto izquierda:** "Valor total que recibirías" — label pequeño gris
- **Número tachado:** "$243" — gris, font-size 24px, text-decoration line-through
- **Fecha flecha SVG:** verde, 20px
- **Número grande:** "$149" — verde brillante #22C55E, font-size 48px, font-weight 800
- **Texto derecha:** "/mes" — gris, 18px, baseline alineado
- **Badge Right:** "Ahorras $94" — fondo verde sólido, texto negro, font-weight 700, padding 6px 16px, border-radius 999px

### Footer del módulo
- **3 checkmarks inline:** "✓ Incluido para siempre | ✓ Sin coste adicional | ✓ Cancela cuando quieras"
- **Color:** verde claro (#4ADE80), font-size 13px

---

## 5. CÓDIGO HTML/CSS

```html
<!-- SECCIÓN: RECURSOS INCLUIDOS -->
<section class="recursos-section">
  <div class="recursos-container">
    
    <!-- Header -->
    <div class="recursos-header">
      <span class="recursos-eyebrow">INCLUIDO EN TUS $149/MES</span>
      <h2 class="recursos-title">Todo lo que incluye tu suscripción</h2>
      <p class="recursos-subtitle">No solo señales. Todo un sistema para invertir mejor.</p>
    </div>

    <!-- Grid de recursos -->
    <div class="recursos-grid">
      
      <!-- Recurso 1: App VERTIX -->
      <div class="recurso-card">
        <div class="recurso-icon">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#22C55E" stroke-width="2">
            <rect x="5" y="2" width="14" height="20" rx="2" ry="2"/>
            <line x1="12" y1="18" x2="12" y2="18.01"/>
          </svg>
        </div>
        <div class="recurso-content">
          <h3 class="recurso-name">App VERTIX</h3>
          <p class="recurso-desc">Tu centro de control 24/7</p>
        </div>
        <span class="recurso-badge">Gratis</span>
      </div>

      <!-- Recurso 2: Guía PDF -->
      <div class="recurso-card">
        <div class="recurso-icon">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#22C55E" stroke-width="2">
            <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/>
            <polyline points="14 2 14 8 20 8"/>
            <line x1="16" y1="13" x2="8" y2="13"/>
            <line x1="16" y1="17" x2="8" y2="17"/>
          </svg>
        </div>
        <div class="recurso-content">
          <h3 class="recurso-name">Guía: Cómo Invertir desde Cero</h3>
          <p class="recurso-desc">Sin experiencia previa</p>
        </div>
        <span class="recurso-badge">Gratis</span>
      </div>

      <!-- Recurso 3: Portfolio Tracker -->
      <div class="recurso-card">
        <div class="recurso-icon">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#22C55E" stroke-width="2">
            <line x1="18" y1="20" x2="18" y2="10"/>
            <line x1="12" y1="20" x2="12" y2="4"/>
            <line x1="6" y1="20" x2="6" y2="14"/>
          </svg>
        </div>
        <div class="recurso-content">
          <h3 class="recurso-name">Portfolio Tracker</h3>
          <p class="recurso-desc">Sigue cada activo en tiempo real</p>
        </div>
        <span class="recurso-badge">Gratis</span>
      </div>

      <!-- Recurso 4: Comunidad Privada -->
      <div class="recurso-card">
        <div class="recurso-icon">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#22C55E" stroke-width="2">
            <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/>
            <circle cx="9" cy="7" r="4"/>
            <path d="M23 21v-2a4 4 0 0 0-3-3.87"/>
            <path d="M16 3.13a4 4 0 0 1 0 7.75"/>
          </svg>
        </div>
        <div class="recurso-content">
          <h3 class="recurso-name">Comunidad Privada</h3>
          <p class="recurso-desc">Inversionistas como tú, compartiendo ideas</p>
        </div>
        <span class="recurso-badge valor">$19/mes</span>
      </div>

      <!-- Recurso 5: Trading Bots -->
      <div class="recurso-card">
        <div class="recurso-icon">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#22C55E" stroke-width="2">
            <polyline points="22 12 18 12 15 21 9 3 6 12 2 12"/>
          </svg>
        </div>
        <div class="recurso-content">
          <h3 class="recurso-name">Trading Bots</h3>
          <p class="recurso-desc">Automatiza tus estrategias sin mirar pantallas</p>
        </div>
        <span class="recurso-badge valor">$97/mes</span>
      </div>

      <!-- Recurso 6: Talleres -->
      <div class="recurso-card">
        <div class="recurso-icon">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#22C55E" stroke-width="2">
            <polygon points="23 7 16 12 23 17 23 7"/>
            <rect x="1" y="5" width="15" height="14" rx="2" ry="2"/>
          </svg>
        </div>
        <div class="recurso-content">
          <h3 class="recurso-name">Talleres Mensuales</h3>
          <p class="recurso-desc">Aprende haciendo con casos reales</p>
        </div>
        <span class="recurso-badge valor">$49/mes</span>
      </div>

      <!-- Recurso 7: Estrategias PDF -->
      <div class="recurso-card">
        <div class="recurso-icon">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#22C55E" stroke-width="2">
            <path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/>
            <path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/>
          </svg>
        </div>
        <div class="recurso-content">
          <h3 class="recurso-name">Estrategias PDF</h3>
          <p class="recurso-desc">Plays concretas para cada escenario de mercado</p>
        </div>
        <span class="recurso-badge valor">$29/mes</span>
      </div>

    </div>

    <!-- Value Stack Banner -->
    <div class="value-stack">
      <div class="value-stack-left">
        <span class="value-label">Valor total que recibirías</span>
        <div class="value-prices">
          <span class="value-old">$243</span>
          <svg class="value-arrow" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#22C55E" stroke-width="2.5">
            <line x1="5" y1="12" x2="19" y2="12"/>
            <polyline points="12 5 19 12 12 19"/>
          </svg>
          <span class="value-new">$149</span>
          <span class="value-period">/mes</span>
        </div>
      </div>
      <div class="value-stack-right">
        <span class="value-savings">Ahorras $94</span>
      </div>
    </div>

    <!-- Footer trust line -->
    <div class="recursos-trust">
      <span>✓ Incluido para siempre</span>
      <span class="trust-divider">|</span>
      <span>✓ Sin coste adicional</span>
      <span class="trust-divider">|</span>
      <span>✓ Cancela cuando quieras</span>
    </div>

  </div>
</section>
```

```css
/* ========================================
   RECURSOS SECTION — CSS
   ======================================== */

.recursos-section {
  background: linear-gradient(180deg, #0A1A12 0%, #0D2318 100%);
  padding: 80px 24px;
  position: relative;
  overflow: hidden;
}

/* Noise texture overlay (opcional) */
.recursos-section::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.65' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%' height='100%' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
  pointer-events: none;
  opacity: 0.4;
}

.recursos-container {
  max-width: 1200px;
  margin: 0 auto;
  position: relative;
  z-index: 1;
}

/* ---- Header ---- */
.recursos-header {
  text-align: center;
  margin-bottom: 56px;
}

.recursos-eyebrow {
  display: inline-block;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: #4ADE80;
  margin-bottom: 16px;
  padding: 6px 16px;
  background: rgba(74, 222, 128, 0.1);
  border: 1px solid rgba(74, 222, 128, 0.2);
  border-radius: 999px;
}

.recursos-title {
  font-size: clamp(28px, 5vw, 44px);
  font-weight: 800;
  color: #FFFFFF;
  margin: 0 0 16px 0;
  line-height: 1.15;
}

.recursos-subtitle {
  font-size: 18px;
  color: #9CA3AF;
  margin: 0;
  font-weight: 400;
}

/* ---- Grid ---- */
.recursos-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  margin-bottom: 40px;
}

@media (max-width: 900px) {
  .recursos-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 580px) {
  .recursos-grid {
    grid-template-columns: 1fr;
  }
}

/* ---- Recurso Card ---- */
.recurso-card {
  position: relative;
  background: #111D14;
  border: 1px solid #1F3A28;
  border-radius: 16px;
  padding: 24px;
  display: flex;
  align-items: flex-start;
  gap: 16px;
  transition: border-color 0.25s ease, box-shadow 0.25s ease, transform 0.25s ease;
  cursor: default;
}

.recurso-card:hover {
  border-color: #22C55E;
  box-shadow: 0 0 24px rgba(34, 197, 94, 0.08);
  transform: translateY(-2px);
}

.recurso-icon {
  flex-shrink: 0;
  width: 48px;
  height: 48px;
  background: #1A3A1C;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.recurso-content {
  flex: 1;
  min-width: 0;
}

.recurso-name {
  font-size: 15px;
  font-weight: 600;
  color: #FFFFFF;
  margin: 0 0 6px 0;
  line-height: 1.3;
}

.recurso-desc {
  font-size: 13px;
  color: #9CA3AF;
  margin: 0;
  line-height: 1.4;
}

/* Badge */
.recurso-badge {
  position: absolute;
  top: 16px;
  right: 16px;
  font-size: 10px;
  font-weight: 700;
  padding: 4px 8px;
  border-radius: 6px;
  background: rgba(74, 222, 128, 0.12);
  color: #4ADE80;
  border: 1px solid rgba(74, 222, 128, 0.2);
  letter-spacing: 0.5px;
}

.recurso-badge.valor {
  background: #22C55E;
  color: #052E16;
  border-color: #22C55E;
}

/* ---- Value Stack Banner ---- */
.value-stack {
  background: #0F2418;
  border: 2px solid #22C55E;
  border-radius: 20px;
  padding: 32px 40px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 24px;
  margin-bottom: 32px;
  position: relative;
  overflow: hidden;
}

.value-stack::before {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(ellipse at center, rgba(34, 197, 94, 0.08) 0%, transparent 70%);
  pointer-events: none;
}

.value-stack-left {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.value-label {
  font-size: 13px;
  color: #9CA3AF;
  font-weight: 500;
}

.value-prices {
  display: flex;
  align-items: baseline;
  gap: 12px;
}

.value-old {
  font-size: 28px;
  color: #6B7280;
  text-decoration: line-through;
  font-weight: 600;
}

.value-arrow {
  flex-shrink: 0;
}

.value-new {
  font-size: 52px;
  font-weight: 800;
  color: #22C55E;
  line-height: 1;
}

.value-period {
  font-size: 18px;
  color: #9CA3AF;
  font-weight: 500;
}

.value-stack-right {
  display: flex;
  align-items: center;
}

.value-savings {
  background: #22C55E;
  color: #052E16;
  font-size: 14px;
  font-weight: 800;
  padding: 10px 24px;
  border-radius: 999px;
  white-space: nowrap;
  letter-spacing: 0.3px;
}

@media (max-width: 600px) {
  .value-stack {
    flex-direction: column;
    text-align: center;
    padding: 28px 24px;
  }
  
  .value-stack-left {
    align-items: center;
  }
  
  .value-new {
    font-size: 44px;
  }
  
  .value-savings {
    width: 100%;
    text-align: center;
  }
}

/* ---- Trust Line ---- */
.recursos-trust {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 12px;
  flex-wrap: wrap;
  font-size: 13px;
  font-weight: 500;
  color: #4ADE80;
}

.trust-divider {
  color: #1F3A28;
}

@media (max-width: 500px) {
  .recursos-section {
    padding: 60px 16px;
  }
  
  .recursos-trust {
    flex-direction: column;
    gap: 6px;
  }
  
  .trust-divider {
    display: none;
  }
}
```

---

## 6. NOTAS DE IMPLEMENTACIÓN

### Integración con sección existente
- La clase `.recurso-card` ya existe según el contexto — este CSS la reutiliza y extiende
- El badge verde con valor monetario (`$19/mes`, `$97/mes`, etc.) diferencia los recursos "gratis" de los que sonsticamente están "incluidos" en la suscripción — esto es clave para el cálculo mental del usuario
- El "Ahorras $94" al final funciona como anclaje de precio y reduce la fricción antes del CTA

### Props vs. problemas que resuelve
| Problema | Solución visual |
|----------|----------------|
| Usuario duda si vale $149 | Value stack $243 → $149 con "Ahorras $94" |
| No sabe qué incluye exactamente | Grid de 7 items con iconos + badges |
| Piensa que las cards sueltas son "extra" | Eyebrow "INCLUIDO EN TUS $149/MES" lo clarifica |
| Escepticismo post-precio | Posición post-Planes responde inmediatamente |
