# Lección 3: El archivo de configuración flowtitude.css

Ya tenemos el sistema instalado. Ahora vamos a personalizarlo. El archivo theme/flowtitude.css es el centro de mando. Aquí defines la «personalidad» de tu web.

No te asustes por el código. Solo tienes que editar la sección KNOBS (Controles) al principio del archivo. El resto son cálculos automáticos que no necesitas tocar.

## 1. Los cimientos del diseño: viewport y texto base

Antes de nada, configuramos el lienzo.

```css
/* RANGES / KNOBS */
--viewport-min: 410px; /* El móvil más pequeño que soportamos */
--viewport-max: 1280px; /* El punto donde el diseño deja de crecer */
```

¿Qué hace esto? El sistema usa estos dos números para calcular todas las interpolaciones fluidas. Si quieres que tu tipografía deje de crecer en pantallas muy grandes (ej: 1440px), cambias el max aquí.

A continuación, definimos el Texto Base:

```css
--ft-text-min: 1rem; /* Tamaño base en móvil */
--ft-text-max: 1.125rem; /* Tamaño base en escritorio */
--ft-type-step-min: 1.125; /* Escala en móvil (Menor contraste) */
--ft-type-step-max: 1.2; /* Escala en escritorio (Mayor contraste) */
```

## 2. Configuración global: fondo y texto

Olvídate de configurar el color de fondo en cada página. Lo definimos una vez para todo el sitio.

```css
--ft-color-text: #000;
--ft-color-background: #fff;
```

- **Recomendación:** No uses blanco puro (#ffffff) ni negro puro (#000000). Usa tonos ligeramente apagados (ej: #f8fafc para fondo, #0f172a para texto) para reducir la fatiga visual y dar un toque más premium.
- **Ventaja:** Si mañana quieres cambiar el fondo de toda la web a un tono crema, solo cambias esta línea.

## 3. La estrategia de color: semántica + utilidad

En este sistema, no eliminamos la paleta estándar de Tailwind (puedes seguir usando bg-red-500 si lo necesitas), pero introducimos una capa semántica para garantizar la consistencia.

### A. Colores semánticos (tus variables maestras)

Definimos dos roles principales que usarás en el 90% de tu diseño:

- **--color-primary:** Tu color de marca principal.
- **--color-secondary:** Color de apoyo o acento.

Estos colores se definen usando OKLCH, el espacio de color moderno que garantiza tonos vibrantes y accesibles en cualquier pantalla.

### B. Definiendo tu paleta con tints.dev

No tienes que inventar los colores. Recomendamos usar la herramienta tints.dev para generar escalas profesionales.

El flujo de trabajo:

1. Elige tu color base en tints.dev.
2. Exporta la paleta en formato Tailwind.
3. Copia los valores y pégalos en la sección @theme de flowtitude.css.

Tabla de uso recomendado (simplificada): Aunque Tailwind te da 10 tonos (50-950), en la práctica solo necesitas mapear estos 4 roles clave para empezar:

| Tono | Uso Recomendado | Variable Sugerida |
|---|---|---|
| 50-100 | Fondos sutiles (tintes) | --color-primary-50 |
| 500 | Color Principal (Botones, Iconos) | --color-primary (Mapeado al 500) |
| 600 | Estados Hover | --color-primary-600 |
| 800 | Textos oscuros de marca | --color-primary-800 |

Nota Técnica: Puedes mezclar colores de diferentes espacios (HEX, RGB, OKLCH), pero recomendamos mantener todo en OKLCH para que las interpolaciones de color sean perfectas.

## 4. Layout General: Contenedor y Gutter

Aquí controlas la «respiración» estructural de tu web sin tener que ajustar cada sección manualmente.

```css
/* Layout defaults */
--ft-container: min(var(--container-7xl), 90%);
--ft-padding-content-x: 1rem; /* Padding lateral móvil */
--ft-padding-content-y: var(--spacing-section); /* Padding vertical fluido */
--ft-gap-content: var(--spacing-block);
```

- **--ft-container:** Define el ancho máximo de tu contenido. Usamos min() para asegurar que nunca toque los bordes en pantallas pequeñas.
- **--ft-padding-content-x:** El «Gutter» o margen de seguridad lateral. Evita que el texto se pegue al borde del móvil.

## 5. Valores de Ejemplo vs. Realidad

Recuerda: Los valores que ves en el archivo (1rem, 410px, etc.) son valores de ejemplo (defaults) sensatos. Esta es la sección que DEBES personalizar en cada proyecto.

Puedes usar:

- **Valores Fijos:** 20px, 5rem.
- **Valores Fluidos:** clamp(1rem, 5vw, 2rem).
- **Funciones CSS:** calc(), min(), max().

El sistema es agnóstico a la unidad que uses, siempre que sea CSS válido.
