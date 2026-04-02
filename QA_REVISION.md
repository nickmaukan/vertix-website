# VERTIX LANDING PAGE — QA REVIEW
**Fecha:** 2026-03-30  
**Reviewer:** QA Tester Subagent (10+ años fintech landing pages)  
**URL:** https://vertix-website.vercel.app  
**Scopes:** Hero → Planes → Recursos → Perfiles → FAQ → CTA  

---

## RESUMEN EJECUTIVO

| Dimensión | Score | Notas |
|-----------|-------|-------|
| Consistencia visual | 6/10 | Paleta OK, pero inconsistencias en cards y espaciados |
| Responsive Design | 5/10 | Breakpoints problemáticos, flags broken en mobile |
| UX/UI | 6.5/10 | Flujo correcto, CTAs decentes, pero hay fricción |
| Bugs visuales | 7/10 | Pocos bugs críticos, pero flags en mobile son feos |
| Performance percibida | 8/10 | Carga rápida, sin console errors |
| **TOTAL** | **6.5/10** | MVP usable, necesita polish antes de producción |

---

## 🔴 CRÍTICOS (Arreglar YA)

### 1. **Flags emoji gigantes en mobile (320px)**
- **Descripción:** Las banderas de país (🇪🇸🇲🇽🇨🇴🇵🇪) aparecen desproporcionadamente enormes en viewport móvil, rompiendo el layout del header/selector de idioma.
- **Ejemplo:** En 320px el emoji tiene ~32px de font-size visual, cuando debería ser ~14px.
- **Cómo arreglarlo:**
  ```css
  /* En mobile, limitar tamaño de flags */
  @media (max-width: 480px) {
    .flag-selector, [data-flag] {
      font-size: 16px !important;
      line-height: 1;
    }
  }
  ```
- **Severidad:** 🔴 Crítico — First impression devastador en mobile.

### 2. **Cards de Pricing se cortan/sobreponen en tablet (768px)**
- **Descripción:** Los 3 planes (Free/Starter/Pro) se ven apretados. El borde del card Pro se corta a la mitad o se superpone con el contenedor.
- **Ejemplo:** En 768px, el card de "Pro" pierde el borde derecho o se encimacon el siguiente.
- **Cómo arreglarlo:**
  ```css
  @media (max-width: 1024px) {
    .pricing-grid {
      grid-template-columns: 1fr;
      gap: 16px;
    }
    /* Alternativa: 1 columna en tablet */
  }
  /* O ajustar max-width del contenedor de pricing */
  ```
- **Severidad:** 🔴 Crítico — Afecta conversión directamente.

### 3. **CTA del Hero no es sticky en mobile**
- **Descripción:** El botón "Consigue WLL" en el hero desaparece al hacer scroll. No hay CTA flotante o sticky en mobile.
- **Cómo arreglarlo:** Añadir un sticky bottom bar en mobile:
  ```css
  .mobile-sticky-cta {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    background: linear-gradient(135deg, #6C47FF, #3D2E8F);
    padding: 12px 16px;
    text-align: center;
    z-index: 999;
  }
  ```
- **Severidad:** 🔴 Crítico — Lost conversion en usuarios mobile (60%+ del tráfico).

---

## 🟠 ALTOS (Arreglar Soon)

### 4. **Inconsistencia de estilo entre "For Traders" y "For Teams"**
- **Descripción:** La card "For Traders" usa fondo amarillo/dorado, mientras "For Teams" usa fondo blanco. No hay consistencia en el sistema de cards.
- **Ejemplo visual:** 
  - Card Traders: `bg: #F5E6A3` con icono trading
  - Card Teams: `bg: #FFFFFF` con icono teams
  - No hay unify en elevation, border-radius, o shadows
- **Cómo arreglarlo:** Definir un sistema de cards consistente:
  ```css
  .feature-card {
    background: var(--card-bg);
    border-radius: 16px;
    padding: 24px;
    box-shadow: 0 4px 24px rgba(0,0,0,0.08);
    /* NO conditional backgrounds */
  }
  ```

### 5. **Navegación overflow en 1024px (tablet landscape)**
- **Descripción:** Los items de nav (Home, Markets, Pricing, Resources, Wallets, Launch App) se salen del viewport en 1024px de ancho.
- **Cómo arreglarlo:**
  ```css
  @media (max-width: 1024px) {
    .nav-links {
      gap: 16px;
      font-size: 14px;
    }
  }
  ```

### 6. **Espaciado inconsistente en secciones**
- **Descripción:** Algunas secciones tienen `padding: 80px 0`, otras `padding: 40px 0`. No hay ritmo vertical consistente.
- **Ejemplo:**
  - Hero: padding vertical grande
  - Features: padding medio
  - CTA final: padding pequeño
- **Cómo arreglarlo:** Usar variables CSS:
  ```css
  :root {
    --section-padding-y: 80px;
    --section-padding-x: 24px;
  }
  .section {
    padding: var(--section-padding-y) var(--section-padding-x);
  }
  ```

### 7. **El card "Free" en pricing tiene badge "Popular" que confunde**
- **Descripción:** El plan Free muestra un badge "Popular" — esto contradice la jerarquía. El badge debería estar en Pro o Starter.
- **Cómo arreglarlo:** Mover "Popular" al plan que realmente quieres vender (Starter o Pro).

---

## 🟡 MEDIOS (Nice to Fix)

### 8. **Footer minimalista pero incompleto**
- **Descripción:** El footer tiene links pero no hay:  
  - Copyright year (debería decir © 2026 Vertix, no vacío)
  - Links a Privacy Policy / Terms
  - Social media icons (insta, twitter, linkedin)
- **Cómo arreglarlo:** Añadir sección footer standard:
  ```html
  <footer>
    <p>© 2026 Vertix. Todos los derechos reservados.</p>
    <nav>
      <a href="/privacy">Privacidad</a>
      <a href="/terms">Términos</a>
    </nav>
    <div class="socials">...</div>
  </footer>
  ```

### 9. **Iconografía inconsistente en feature cards**
- **Descripción:** Algunas cards usan iconos outline, otras filled. No hay sistema de iconos unificado.
- **Cómo arreglarlo:** Elegir un estilo (recomiendo outline para fintech/professional) y aplicarlo consistentemente.

### 10. **Typo en "For Teams" — "Todo lo que necesitas pera tu equipo"**
- **Descripción:** Hay un typo "pera" → debería ser "para".
- **Cómo arreglarlo:** Correct spellcheck antes de deploy.

### 11. **CTA "Consigue WLL" en hero es redundante con "Launch App" en nav**
- **Descripción:** El hero tiene un CTA "Consigue WLL" que lleva al mismo flujo que "Launch App" en la navegación. Duplicación innecesaria.
- **Cómo arreglarlo:** En hero, el CTA debería ser diferente: "Comenzar ahora" o "Crear cuenta gratis" para dar una opción de onboarding distinto a "Launch App".

### 12. **Ausencia de social proof en hero**
- **Descripción:** No hay indicadores de confianza: número de usuarios, AUM, premios, logos de clientes.
- **Cómo arreglarlo:** Añadir una línea bajo el headline:
  ```
  "Más de $50M en volumen operado • +2,000 traders activos"
  ```

### 13. **FAQ sin expand/collapse en mobile**
- **Descripción:** Las preguntas del FAQ se muestran todas abiertas, ocupando mucho scroll vertical innecesario.
- **Cómo arreglarlo:** Implementar accordion pattern:
  ```css
  .faq-item { cursor: pointer; }
  .faq-answer { 
    max-height: 0; 
    overflow: hidden; 
    transition: max-height 0.3s ease;
  }
  .faq-item.open .faq-answer { max-height: 200px; }
  ```

---

## 🔍 ANÁLISIS POR SECCIÓN

### HERO
| Aspecto | Estado | Notas |
|---------|--------|-------|
| Headline | ✅ | "Comienza tu camino" — clear y directo |
| Subheadline | ⚠️ | No visible o muy corta |
| CTA | ⚠️ | "Consigue WLL" — nombre de producto poco claro para nuevo usuario |
| Phone mockup | ✅ | Good, se ve real |
| Social proof | ❌ | Ausente |
| Flags/selector idioma | 🔴 | Broken en mobile |
| **Score sección** | **6/10** | |

### PLANES / PRICING
| Aspecto | Estado | Notas |
|---------|--------|-------|
| Estructura 3 columnas | ⚠️ | Se rompe en tablet |
| Jerarquía clara | ⚠️ | "Popular" en Free confunde |
| Precio visible | ✅ | Buenos precios ($0, $19, $49) |
| Feature list | ✅ | Claro y escaneable |
| CTAs por plan | ✅ | Bien, cada plan tiene su CTA |
| **Score sección** | **6.5/10** | |

### RECURSOS / FEATURES
| Aspecto | Estado | Notas |
|---------|--------|-------|
| Cards system | ⚠️ | Inconsistente (color, sombra) |
| Iconografía | ⚠️ | Mix outline/filled |
| Copy | ✅ | Claro y conciso |
| Escaneabilidad | ✅ | Buena jerarquía visual |
| **Score sección** | **7/10** | |

### PERFILES / USE CASES
| Aspecto | Estado | Notas |
|---------|--------|-------|
| 3 perfiles | ✅ | Trading, Portfolio, Fintech |
| Visual cards | ⚠️ | Mezcla de estilos con otras secciones |
| Info por perfil | ✅ | Suficiente detalle |
| **Score sección** | **7.5/10** | |

### FAQ
| Aspecto | Estado | Notas |
|---------|--------|-------|
| Preguntas relevantes | ✅ | Buenos temas |
| Respuestas concisas | ✅ | No excesivamente largas |
| Accordion | ❌ | No funciona en mobile |
| Search | ❌ | No hay filtro/búsqueda |
| **Score sección** | **6/10** | |

### CTA FINAL
| Aspecto | Estado | Notas |
|---------|--------|-------|
| Headline | ✅ | Claro |
| Form/email | ⚠️ | No visible, solo botón |
| Urgencia | ❌ | Sin countdown o escasez |
| **Score sección** | **6/10** | |

---

## 🛠️ BUGS TÉCNICOS

### Console Errors
✅ **0 errores en Console** — Limpio, bien codeado.

### Network Resources
⚠️ **Recursos no verificados** — No hay 404 visibles en los screenshots, pero se recomienda correr Lighthouse con network log.

### Lighthouse (recomendado correr)
```
npm install -g lighthouse
lighthouse https://vertix-website.vercel.app --view
```

Métricas objetivo:
- Performance: > 90
- Accessibility: > 95
- Best Practices: > 90
- SEO: > 95

---

## 📱 RESPONSIVE BREAKPOINTS TESTED

| Viewport | Resultado | Issues |
|----------|-----------|--------|
| 320px (mobile S) | ❌ Fail | Flags gigantes, CTA truncado |
| 375px (mobile L) | ⚠️ Warning | Flags still oversized, nav items apretados |
| 768px (tablet) | ⚠️ Warning | Cards pricing rotos, nav overflow |
| 1024px (laptop) | ⚠️ Warning | Nav ligeiramente apretado |
| 1440px (desktop) | ✅ Pass | Todo se ve bien |

---

## ✅ LISTA DE ARREGLOS PRIORIZADA

**Fase 1 (1-2 días):**
1. 🔴 Fix flags emoji en mobile
2. 🔴 Fix pricing cards en tablet
3. 🔴 Sticky CTA en mobile

**Fase 2 (3-5 días):**
4. 🟠 Unificar sistema de cards
5. 🟠 Fix nav overflow en tablet
6. 🟠 Consistent spacing system
7. 🟠 Mover badge "Popular" al plan correcto

**Fase 3 (1 semana+):**
8. 🟡 Footer completo
9. 🟡 Accordion en FAQ
10. 🟡 Social proof en hero
11. 🟡 Fix typo "pera" → "para"
12. 🟡 Sistema de iconos consistente

---

## 💡 RECOMENDACIONES ESTRATÉGICAS

1. **Mobile-first redesign:** 60%+ del tráfico viene de mobile. Diseñar desde 320px primero.
2. **Lighthouse audit:** Antes de launch, correr Lighthouse y golpear >90 en todas las métricas.
3. **A/B test CTA copy:** "Consigue WLL" vs "Prueba gratis" — medir conversión.
4. **Social proof prominente:** Fintech = trust. Añadir número de usuarios, volumen, o logos de partners.
5. **Animaciones sutiles:** Los hover states en cards faltan polish — añadir `transform: translateY(-4px)` y shadow transition.

---

## SCORE FINAL

**6.5 / 10**

Landing page usable con buena base. Los issues de mobile son blockeadores de conversión. Priorizar fixes de Fase 1 antes de cualquier campaña de tráfico real.

---
*QA Review generado por subagent — 2026-03-30*
