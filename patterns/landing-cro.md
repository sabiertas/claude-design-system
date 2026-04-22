# Pattern — Landing CRO

Landing de conversión (one-page) optimizada para captar lead o venta directa. Estructura probada, orden deliberado, cada bloque con un job to be done claro.

## Objetivo

Mover al visitante del primer scroll al CTA en el menor número de dudas posible. Cada sección responde a una objeción típica.

## Estructura (orden fijo)

1. **Nav** — logo + 3-4 links máx + CTA secundario derecha. Sticky opcional.
2. **Hero** — ver `patterns/section-hero/PATTERN.md`. Incluye CTA primario.
3. **Social proof inmediato** — logos de clientes, estrellas, "X empresas confían en…". Refuerza el hero.
4. **Problema / promesa** — qué duele hoy al visitante. Frase corta, 1 imagen o icono por punto (3 puntos).
5. **Solución (features)** — 3–6 features con icono + titular + 1 línea. No listas largas, sí jerarquía. Alternar texto-imagen a la izquierda/derecha si hay espacio.
6. **Cómo funciona** — 3 pasos numerados. Visual con screenshot o ilustración por paso.
7. **Caso de uso / testimonial detallado** — cita + foto + rol + resultado cuantitativo ("reducimos el tiempo de onboarding de 2 semanas a 3 días").
8. **Pricing** (si aplica) — 3 planes máx, plan recomendado destacado (`.plan-popular` en SA). Precio mensual + anual toggle si hay descuento.
9. **FAQ** — 6–10 preguntas reales. Accordion. Aborda objeciones frecuentes (precio, tiempo de setup, compatibilidad, soporte, reembolso).
10. **CTA final** — fondo contrastado (oscuro o burdeos en SA). Titular + subtítulo + botón primario grande.
11. **Footer** — logo + links legales + redes + copyright.

## Props de datos

Una landing se parametriza con este shape (orientativo, no todas las secciones usan todo):

```yaml
landing:
  meta:
    title: "SEO title"
    description: "SEO description"
  hero:
    eyebrow: "Qué categoría es"
    title: "Headline principal"
    subtitle: "1-2 frases que expanden la promesa"
    cta_primary: { label: "...", href: "#pricing" }
    cta_secondary: { label: "...", href: "#demo" }
    media: { type: "image|video|animation", src: "..." }
  social_proof:
    stat: "+500 empresas usan X"
    logos: ["/img/logo-1.svg", ...]
  problems: [{ icon, title, body }, ...]        # máx 3
  features: [{ icon, title, body, image? }, ...] # 3-6
  steps: [{ number, title, body, image }, ...]   # 3
  testimonial: { quote, author, role, company, avatar, result }
  pricing:
    plans: [{ name, price, period, features: [], cta, popular: bool }]
  faq: [{ question, answer }, ...]              # 6-10
  cta_final: { title, subtitle, cta }
```

## Reglas de diseño

- **Una idea por sección.** Si hay que explicar dos cosas, son dos secciones.
- **CTA siempre visible arriba del fold** en el hero.
- **Contraste entre secciones.** Alternar fondo claro y fondo tinted/oscuro para marcar ritmo. En SA: blanco, `#f9f9f9`, sección oscura con `gradient-dark`, burdeos sólido para CTA final.
- **Jerarquía tipográfica.** Una única H1 (hero), H2 por sección, H3 dentro de features/pasos. Nunca dos H1 en la misma página.
- **Imágenes con propósito.** Fotos tenenciosas → fuera. Screenshots reales del producto > ilustraciones genéricas.
- **Mobile primero.** El fluido del FDS cubre el ancho, pero verificar que el hero no requiera scroll para ver el CTA en móvil 375×667.
- **A11y WCAG AA** mínimo: contraste ≥ 4.5:1 en texto, botones con aria-label si sólo icono, navegación por teclado.

## Variantes

### A) Landing de servicio SaaS
- Sección **Integrations** opcional entre features y pricing (grid de logos clicables).
- Pricing con toggle mensual/anual.
- CTA final: "Prueba gratis 14 días".

### B) Landing de servicio consultor (SA típica)
- Sin pricing público → sustituir por **"Cómo trabajamos"** con 3 pasos (descubrimiento → propuesta → ejecución).
- CTA final: "Agenda una llamada" con Cal.com o form.
- Añadir sección **Quién somos / por qué nosotros** (2-3 bullets diferenciadores).

### C) Landing de producto digital (plugin, curso)
- Hero con vídeo corto (60s) autoplay muted.
- Sección **Lo que incluye** con lista checkable.
- Garantía de devolución destacada cerca del CTA final.

## Animación

- Scroll reveal con **USAL.js** en features, pasos y testimonial (stagger 100ms).
- Hero: NO animar entrada masiva. Fade-in suave a 300ms del primer bloque, o ninguna.
- Botones: hover 150ms, transform scale(1.02) + cambio de color sutil.

## Qué evitar

- Nav con 8+ links. Si no caben, replantea.
- Hero con H1 en 3 líneas. Una línea, máx dos.
- Pricing con 4+ planes (parálisis de decisión).
- FAQ con menos de 5 o más de 12 preguntas.
- Carruseles de testimonios que auto-rotan (nadie los lee).
- Stock genérico de consultoría.

## Ejemplos internos

- Soluciones Abiertas landing: `/Volumes/Disco SSD/Desarrollo/soluciones-abiertas/one-page/`
