# Lección 4: El sistema tipográfico integral

La tipografía en este sistema no es solo un conjunto de tamaños de fuente. Es un motor de reglas que separa la Semántica (qué etiqueta HTML usas) de la Estética (cómo se ve).

En esta lección entenderemos las tres capas del sistema tipográfico:

1. **Preflight Semántico:** Estilos base automáticos.
2. **El Componente .prose:** Para contenido editorial complejo.
3. **Configuración Fluida:** Cómo el sistema escala matemáticamente.

## 1. Preflight semántico (base/typography.css)

Lo primero que hace el sistema es «limpiar y preparar» las etiquetas HTML nativas. Si abres base/typography.css, verás que atacamos directamente a las etiquetas:

```css
h1, h2, h3, h4, h5, h6 {
  @apply break-words font-display font-bold text-balance tracking-tight;
}
```

Automatizaciones Clave:

- **font-display:** Asigna automáticamente tu fuente de titulares (definida en flowtitude.css) a todos los encabezados.
- **text-balance:** Una propiedad moderna vital. El navegador equilibra automáticamente la longitud de las líneas en los títulos para evitar que una sola palabra quede "huérfana" en la última línea.
- **Escala visual:**
  - h1: Se mapea a text-5xl con leading-none (sin interlineado extra).
  - h6: Se mapea a text-lg.

El beneficio: Solo tienes que arrastrar un elemento "Heading" en Bricks y elegir la etiqueta (H1, H2...). No necesitas añadir clases para que se vea profesional.

## 2. El componente .prose (independencia semántica)

¿Qué pasa cuando tienes un artículo de blog o un campo de «Texto Enriquecido» en Bricks? No puedes ir párrafo por párrafo añadiendo clases de Tailwind. El HTML viene plano desde WordPress.

Para esto existe el componente .prose.

**Cómo funciona:** Es un "wrapper" o contenedor inteligente. Al aplicar la clase .prose a un div contenedor, el sistema activa un conjunto de reglas descendentes que estilizan todo lo que hay dentro, independientemente de su origen.

```css
.prose h1 { @apply text-4xl leading-none mb-2 mt-4; }
.prose p { @apply my-4; }
.prose blockquote { @apply border-l-4 border-secondary-500 pl-4 italic; }
```

Poderes del Prose:

- **Ritmo vertical:** Gestiona los márgenes (my-4) entre párrafos automáticamente.
- **Selectores de adyacencia inteligente:**
  - Si tienes un H2 seguido de un H3, el sistema detecta que son familia y reduce el margen entre ellos (mt-0) para mantenerlos visualmente agrupados.
- **Elementos ricos:** Las listas (ul, ol), citas (blockquote) y tablas se estilizan automáticamente con los colores de tu marca (border-secondary-500) sin que tengas que tocar nada.

## 3. Desacoplando estilo y semántica (components/typography.css)

Aquí está la potencia real del diseño. A veces quieres un texto visualmente impactante, pero semánticamente es solo un párrafo. O quieres un H1 que visualmente sea pequeño.

El sistema incluye un set de clases semánticas divididas en 4 categorías:

### A. Display (.display-)

Para textos gigantes, decorativos o de impacto (Hero Sections).

**Uso:** Un número gigante en una tabla de estadísticas o la palabra clave de un Hero.
**Variantes:** .display-lg, .display-md, .display-sm.

### B. Heading (.heading-)

Replican la estética de los encabezados pero en forma de clase, ideal para cuando la semántica no coincide con el estilo deseado.

**Caso de uso:** Tienes un widget de "Testimonio" que es un p (párrafo) semánticamente, pero quieres que visualmente parezca un título. Le aplicas .heading-md.
**Variantes:** .heading-lg (aprox H2), .heading-md (aprox H3), .heading-sm (aprox H4/H5).

### C. Subheading (.subheading-)

Para ante-títulos (kickers) o etiquetas superiores.

**Estilo típico:** Suelen usar mayúsculas (uppercase), tracking amplio y colores de acento.
**Variantes:** .subheading-lg, .subheading-sm.

### D. Text (.text-)

Para variantes del cuerpo de texto que no son el estándar.

**Variantes:** .text-lead (intro de blog, más grande), .text-caption (pie de foto, más pequeño), .text-body (estándar).

## Resumen de la Estrategia

La filosofía aquí no es usar siempre los mismos valores, sino mantener la nomenclatura.

En cada proyecto, editas flowtitude.css para definir qué tamaño tiene un .display-lg o qué fuente usa un .heading-sm.

Pero en tu construcción en Bricks, siempre usas las mismas clases.

De esta forma, tu cerebro no tiene que aprender un sistema nuevo en cada web, solo ajustar la configuración inicial.
