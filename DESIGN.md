# Flowtitude Design System (FDS)

Sistema de diseño base de Soluciones Abiertas. Fluido, semántico y construido
sobre Tailwind v4 con OKLCH. Pensado para que las marcas propias y de cliente
hereden de aquí y solo sobreescriban los tokens necesarios.

---

## 1. Visual Theme & Atmosphere

**Palabras clave:** fluido, editorial, cálido-neutral, OKLCH, semántico,
fluid-responsive sin breakpoints.

FDS es un sistema **fluido, no responsive por breakpoints**. Tipografía y
espaciado escalan linealmente entre un viewport mínimo (`410px`) y máximo
(`1280px`) usando `clamp()`. Resultado: la misma composición lee bien en móvil
pequeño, tablet y desktop sin cortes bruscos. Nada de `md:`, `lg:`, `xl:`
salvo cuando el cambio realmente cambia el layout.

Tono visual: editorial, cálido-neutral, con grises de undertone marrón
(croma muy baja, hue ~18). Nada frío ni corporativo gris azulado. La paleta
permite contraste duro cuando hace falta usando neutrals nativos de Tailwind.

Los tokens viven en dos espacios:
- **Knobs** — valores editables (ej. `--ft-text-min`, `--ft-space-step-max`).
- **Derived values** — calculados a partir de los knobs (ej. `--text-base`,
  `--spacing-block`).

Tocar un knob en el override de proyecto propaga a toda la escala.

---

## 2. Color Palette & Roles

Todos los colores en **OKLCH** para interpolación perceptualmente uniforme.

### Primary (rojo cálido por defecto)

| Token | OKLCH | Rol |
|---|---|---|
| `--color-primary-50` | `oklch(0.97 0.0255 27.19)` | Fondos muy suaves |
| `--color-primary-100` | `oklch(0.94 0.0428 27.19)` | Fondos suaves |
| `--color-primary-500` | `oklch(0.5365 0.1984 27.19)` | Brand principal, CTAs |
| `--color-primary-700` | `oklch(0.4517 0.1884 27.19)` | Hover / active |
| `--color-primary-950` | `oklch(0.2505 0.1579 27.19)` | Sobre oscuro |

Atajo: `--color-primary` = `--color-primary-500`.

### Secondary (warm neutral)

Serie `--color-secondary-50` → `--color-secondary-950` con croma muy baja
(0.002–0.036) y hue ~18 (cálido). Para fondos, bordes y texto secundario sin
enfriar la paleta.

### Neutrals

`--color-neutral-*` nativa de Tailwind v4 para blancos/negros puros con
contraste duro.

### Roles semánticos

| Rol | Token |
|---|---|
| Brand / CTA | `--color-primary-500` |
| Brand hover | `--color-primary-700` |
| Texto principal | `--color-neutral-800` |
| Texto secundario | `--color-secondary-600` |
| Botón texto sobre primary | `--color-neutral-100` |
| Borde sutil | `--color-secondary-200` |
| Fondo sección suave | `--color-primary-50` |

---

## 3. Typography Rules

Familia por defecto: **Arial, system-ui, Helvetica Neue, sans-serif**.

Variables:
- `--font-body` — cuerpo (default Arial).
- `--font-display` — titulares (default = body; override para usar
  serif/display distinta).

### Escala fluida

Base entre `1rem` (mobile) y `1.125rem` (desktop). Step entre tamaños también
fluido: `1.125` → `1.2` conforme crece el viewport.

Tokens: `--text-xs`, `--text-sm`, `--text-base`, `--text-lg` … `--text-9xl`.
Nada en px. Uso con Tailwind: `text-base`, `text-3xl`, `text-5xl` — fluidos
sin añadir `md:` ni `lg:`.

### Line-height

| Token | Valor |
|---|---|
| `--leading-none` | `1em` |
| `--leading-tight` | `1.2em` |
| `--leading-snug` | `1.375em` |
| `--leading-normal` | `1.5em` |
| `--leading-relaxed` | `1.625em` |
| `--leading-loose` | `2em` |

### Reglas de uso

- Titulares: `font-display` + `leading-tight`.
- Cuerpo: `font-body` + `leading-normal`.
- Eyebrow / labels: `text-sm uppercase` con tracking sutil (clase
  `.eyebrow` en componentes).

---

## 4. Component Stylings

### Botones

- Padding fluido: `--btn-py: 0.6em` · `--btn-px: 1.75em`.
- Radius: `--radius-button = --radius-sm`.
- **Primary:** `bg-[--color-primary]` + texto `--color-neutral-100`.
- **Outline:** transparente, border `currentColor`, texto
  `--color-neutral-800`.
- **Estados:** hover → `--color-primary-700`, focus visible con outline
  accesible, disabled `opacity-50 cursor-not-allowed`.

Definidos en `src/components/buttons.css` con `@apply`.

### Cards

- Widths semánticos: `--ft-card-xs: 12rem` → `--ft-card-xl: 36rem`.
- Radius: `--radius-card = --radius-md`.
- Padding interno: `--spacing-content`.

Definidos en `src/components/cards.css`.

### Inputs

- Misma altura visual que botones (`--btn-py`).
- Border `--color-secondary-300`, focus `--color-primary-500`.
- Radius `--radius-sm`.

### Navegación

- Links sin underline por defecto, underline en hover.
- Active state con border-bottom de 2px en `--color-primary-500`.

### Typography components

`.eyebrow`, `.lead`, `.display` — clases utilitarias en
`src/components/typography.css`.

---

## 5. Layout Principles

### Espaciado semántico (preferido sobre numérico)

| Token | Uso típico |
|---|---|
| `--spacing-inner` | Padding componente pequeño (chip, badge) |
| `--spacing-content` | Padding contenido (card body, callout) |
| `--spacing-stack` | Gap vertical entre hijos en una pila |
| `--spacing-block` | Gap entre bloques de contenido |
| `--spacing-columns` | Gap horizontal entre columnas |
| `--spacing-section` | Padding top/bottom de section |
| `--spacing-hero` | Padding generoso de hero |

Todos fluidos. Escala neutra `--spacing-fluid-xs/sm/md/lg/xl/2xl` si se
necesita tamaño directo.

**Regla:** preferir `p-[--spacing-section]`, `gap-[--spacing-stack]` frente a
magnitudes (`p-12`, `gap-8`).

### Container y rejilla

- `--ft-container: min(--container-7xl, 90%)` — contenedor por defecto.
- `--ft-padding-content-x: 1rem`.
- `--ft-padding-content-y: --spacing-section`.
- `--ft-gap-content: --spacing-block`.

### Variantes Tailwind custom

- `parent:` — estiliza el padre que contiene este elemento como hijo directo.
- `parent-hover:` — estiliza un elemento cuando se hace hover sobre su padre.
- `parent-focus-within:` — cuando el padre tiene foco.

### Aspect ratios

| Token | Valor | Uso |
|---|---|---|
| `--aspect-rrss` | `1.91 / 1` | Open Graph, redes sociales |
| `--aspect-wide` | `18 / 8` | Hero banner |
| `--aspect-ultrawide` | `18 / 5` | Banner ancho |
| `--aspect-golden` | `1.618 / 1` | Composiciones editoriales |
| `--aspect-portrait` | `3 / 4` | Retrato |
| `--aspect-landscape` | `4 / 3` | Paisaje |

---

## 6. Depth & Elevation

Sombras suaves, nunca duras. Pensadas para superficies cálidas, no para
imitar Material.

| Token | Uso |
|---|---|
| `--shadow-xs` | Border sutil para inputs/botones outline |
| `--shadow-sm` | Card en reposo |
| `--shadow-md` | Card hover, dropdown |
| `--shadow-lg` | Modal, popover |
| `--shadow-xl` | Hero feature destacado |

Reglas:
- Nunca combinar más de 2 niveles de elevación en la misma vista.
- Hover de card: subir un nivel (`--shadow-sm` → `--shadow-md`).
- Fondos oscuros: bajar opacidad de la sombra al 50%.

Border radius:
- `--radius-sm` (botones, inputs).
- `--radius-md` (cards, paneles).
- `--radius-lg` (heros, contenedores grandes).
- `--radius-full` (avatares, badges circulares).

---

## 7. Do's and Don'ts

### Do

- Usa **tokens semánticos** (`--spacing-section`, `--color-primary`) en lugar
  de magnitudes/colores literales.
- Trabaja **fluido**: `text-3xl` ya escala, no añadas `md:text-4xl`.
- Importa el FDS y haz override solo de los **knobs** que cambien por proyecto.
- Componentes nuevos → `custom-{page}.css` con `@layer components` y `@apply`.
- Animaciones → **USAL.js** (atributos/hooks que el script espera).

### Don't

- **No** uses breakpoints de Tailwind (`md:`, `lg:`, `xl:`) salvo cambio real
  de layout.
- **No** uses colores hex/rgb literales — siempre vía token OKLCH.
- **No** edites el FDS fuente (`src/`) — override en proyecto.
- **No** uses `@keyframes` manuales ni otra librería de animación.
- **No** mezcles más de 2 elevaciones en la misma vista.
- **No** uses grises fríos — los neutrals secundarios tienen undertone cálido
  por diseño.

---

## 8. Responsive Behavior

FDS es **fluid-first**, no breakpoint-first.

### Comportamiento por defecto

- Tipografía: escala con `clamp()` entre 410px y 1280px de viewport.
- Espaciado: idem, vía `--ft-space-value`.
- Containers: `min(--container-7xl, 90%)` se adapta solo.

### Cuándo SÍ usar breakpoints

Solo cuando el cambio es estructural, no de tamaño:
- 1 columna → 3 columnas en grid de cards.
- Menú hamburguesa → menú horizontal.
- Sidebar oculto → sidebar fijo.

Breakpoints disponibles (Tailwind v4 default): `sm`, `md`, `lg`, `xl`, `2xl`.

### Touch targets

- Mínimo 44x44px en superficies táctiles (botones, links de nav).
- Padding generoso en links de menú móvil.
- Hover states siempre con fallback `:focus-visible` para accesibilidad.

---

## 9. Agent Prompt Guide

Prompts reutilizables al generar UI con este sistema en Claude Design.

### Para una landing nueva

> Usa el Flowtitude Design System. Aplica tokens semánticos
> (`--spacing-section`, `--color-primary`). Tipografía fluida sin breakpoints
> de tamaño. Paleta cálida con primary rojo OKLCH y secundarios warm-neutral.
> Botones primary con bg-primary y texto neutral-100. Sombras suaves
> (`--shadow-sm` en reposo, `--shadow-md` en hover). Animaciones con USAL.js.

### Para un componente aislado

> Genera el componente como HTML+Tailwind v4 usando solo tokens del FDS.
> Componente nuevo va en `custom-{page}.css` con `@layer components` y
> `@apply`. Nada de hex/rgb literales ni `@keyframes`.

### Para un override de marca

> Crea `theme/{marca}.css` que solo redefine knobs (colores primary, font
> display, viewport range si aplica). No tocar derived values salvo necesidad
> real. Importar después de `main.css` del FDS.

### Reglas para refinamiento

- Si Claude propone breakpoint para cambiar tamaño → recordar fluid scale.
- Si propone hex/rgb → reemplazar por token OKLCH equivalente.
- Si propone `@keyframes` → reemplazar por atributos USAL.
- Si propone gris frío → reemplazar por `--color-secondary-*`.

---

## Override por proyecto (workflow)

1. **Copiar** `src/theme/flowtitude.css` al proyecto (ej. `css/theme/project.css`).
2. **Redefinir** solo los knobs que cambien.
3. En `input-{page}.css` del proyecto:
   ```css
   @import "/ruta/al/FDS/main.css";   /* FDS intacto */
   @import "./theme/project.css";     /* override */
   @import "./custom-{page}.css";     /* clases nuevas @apply */
   @source "../path/to/page.html";    /* tailwind escanea HTML */
   ```
4. Compilar: `npx @tailwindcss/cli -i css/input-{page}.css -o css/output-{page}.css`.
5. En Bricks: subir el `output-{page}.css` compilado como Custom CSS del
   tema/página.

---

## Qué NO es FDS

- **No** es un tema WordPress. Es una capa CSS reutilizable.
- **No** fuerza componentes visuales concretos (no es Bootstrap).
- **No** usa breakpoints tradicionales para escalar tamaños — todo fluido.
- **No** incluye iconos ni ilustraciones — eso lo decide cada marca.
