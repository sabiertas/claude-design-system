# Pattern — Section Hero

Primer bloque de una landing/home. Objetivo: **en 3 segundos** el visitante entiende qué es, para quién, y puede hacer click.

## Anatomía

```
┌────────────────────────────────────────────────┐
│ [nav aquí o arriba, no duplicar en hero]       │
│                                                │
│  EYEBROW (pequeño, uppercase, accent color)    │
│                                                │
│  HEADLINE (H1, display font, peso 700,         │
│  1 línea ideal, 2 máx)                         │
│                                                │
│  Subtítulo en una frase clara que expande      │
│  la promesa. Body font, leading relaxed.       │
│                                                │
│  [CTA primario]  [CTA secundario / ghost]      │
│                                                │
│  [media: imagen, screenshot, vídeo, o          │
│   ilustración. Puede ir al lado (split) o      │
│   debajo (centered).]                          │
└────────────────────────────────────────────────┘
```

## Props

```yaml
hero:
  layout: "centered | split-left | split-right | full-bleed"
  eyebrow: "Mantenimiento WordPress"            # opcional, 2-4 palabras
  title: "Tu sitio WordPress, funcionando sin sustos"  # 1 línea ideal
  subtitle: "Mantenimiento proactivo con respuesta humana en horas, no en días."
  cta_primary:
    label: "Ver planes"
    href: "#pricing"
  cta_secondary:
    label: "Cómo trabajamos"
    href: "#process"
  media:
    type: "image | video | animation | none"
    src: "/img/hero-dashboard.png"
    alt: "Descripción accesible"
  background: "light | dark | gradient | image"
```

## Layouts

### `centered`
Todo centrado. Media debajo del CTA. Bueno para landing corta y producto visual.

### `split-left` / `split-right`
Texto un lado, media otro. 50/50 en desktop, apilado en mobile. Screenshots y dashboards funcionan mejor aquí.

### `full-bleed`
Imagen de fondo a sangre con overlay oscuro, texto superpuesto. Reservar para marcas con foto potente. En SA raramente.

## Tokens (FDS + marca)

- **Padding vertical:** `--spacing-hero` (el mayor del sistema).
- **Padding horizontal:** `--ft-padding-content-x` + container `--ft-container`.
- **Eyebrow:** `text-sm`, `font-semibold`, `uppercase`, `letter-spacing: 0.05em`, color de marca (`text-sa-primary` en SA).
- **H1:** `font-display`, `font-bold`, `text-5xl` → `text-7xl` (fluido), `leading-tight`, max-w 14–18em para evitar renglones largos.
- **Subtítulo:** `font-body`, `font-normal`, `text-lg` → `text-xl`, `leading-relaxed`, color texto secundario, max-w ~42em.
- **CTAs:** primary filled con color de marca, secondary ghost con border currentColor. Gap entre ellos 1rem.

## Reglas

- **Una sola H1 en toda la página.** El hero la tiene.
- **CTA primario visible sin scroll** en móvil 375×667 y en desktop 1280×720.
- **Media opcional.** Si no hay screenshot potente del producto, mejor sin imagen que con stock.
- **Eyebrow no es imprescindible.** Útil para contextualizar (categoría, sector) cuando el headline por sí solo no basta.
- **Contraste texto/fondo mínimo 4.5:1.**
- **Subtítulo ≤ 2 líneas en desktop**, ≤ 3 en mobile.

## Animación

- Entrada suave al cargar: eyebrow + H1 + subtítulo + CTAs en cascada (0ms, 80ms, 160ms, 240ms) con fade+slide-up de 8px. USAL o CSS directo con `animation-delay`.
- Media: aparece después con fade 400ms.
- **No** parallax ni efectos pesados en el hero. Prioridad: LCP rápido.

## Performance

- Imagen hero: formato moderno (WebP/AVIF), `<img loading="eager" fetchpriority="high">`.
- Si hay vídeo: preload metadata, poster frame obligatorio, `playsinline muted autoplay`.
- Fuentes display: `font-display: swap` + preload.

## Variantes por marca

- **SA:** fondo `#f9f9f9` o `gradient-dark` si es landing de producto. Eyebrow en `text-sa-primary`. H1 Space Grotesk weight 700.
- **Cliente con DESIGN.md propio:** leer tokens de su brand, respetar paleta y tipografía propia. Si no tiene brand definida, usa FDS puro.

## Qué evitar

- H1 de 3+ líneas. Si no cabe en 2, corta.
- CTA "Saber más" genérico. Sé concreto: "Ver planes", "Agenda llamada", "Empieza gratis".
- Stock de gente sonriendo con portátiles.
- Dos CTAs del mismo peso visual (si hay dos, uno primario + uno ghost).
- Auto-play de vídeo con sonido.
