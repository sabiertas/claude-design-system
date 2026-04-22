# Lección 6: Utilidades de grid avanzadas y la variación parent

Ya dominas el layout básico. Ahora vamos a ver las herramientas de potencia industrial que incluye el sistema en utility/layout/grid-basic.css.

Estas utilidades te permiten crear estructuras complejas y responsivas sin escribir CSS manual ni calcular porcentajes.

## 1. Grids automáticos (auto-fit y auto-fill)

El sistema incluye 10 utilidades para crear rejillas que se adaptan al contenido automáticamente. No tienes que decidir "cuántas columnas" quieres, solo decides "cuánto debe medir como mínimo cada tarjeta".

La fórmula mágica que usan es: `repeat(auto-fit, minmax(min(var(--ft-card-{size}), 100%), 1fr))`.

Las utilidades disponibles:

| Clase | Tamaño Min. Tarjeta | Uso Recomendado |
|---|---|---|
| .grid-auto-fit-xs | 12rem (aprox 192px) | Iconos, logos, stats pequeñas. |
| .grid-auto-fit-sm | 14rem (aprox 224px) | Tarjetas de perfil, listados densos. |
| .grid-auto-fit-md | 18rem (aprox 288px) | El estándar. Blog posts, productos. |
| .grid-auto-fit-lg | 24rem (aprox 384px) | Tarjetas destacadas, servicios. |
| .grid-auto-fit-xl | 36rem (aprox 576px) | Layouts de 2 columnas grandes. |

Nota: También tienes las variantes auto-fill (ej: .grid-auto-fill-md) si prefieres que no se estiren las tarjetas si sobran huecos.

## 2. Grids asimétricos (layouts de revista)

Normalmente, para hacer un diseño de «Texto a la izquierda (1/3) e Imagen a la derecha (2/3)», tendrías que usar grid-cols-3 y luego ir al hijo y ponerle col-span-2.

Con este sistema, defines la asimetría en el padre. Los hijos se colocan solos.

**Nomenclatura:** `grid-cols-{proporción}`.

### A. Layouts de 2 zonas (3 fracciones totales)

- **.grid-cols-1-2:** Columna estrecha izq (1fr) + Columna ancha der (2fr). Ideal Sidebar Izq.
- **.grid-cols-2-1:** Columna ancha izq (2fr) + Columna estrecha der (1fr). Ideal Sidebar Der.

### B. Layouts de proporción áurea (4 fracciones totales)

- **.grid-cols-1-3:** 25% / 75%. Ideal para menús laterales.
- **.grid-cols-3-1:** 75% / 25%. Ideal para contenido principal y publicidad.

### C. Layouts complejos (Bento)

- **.grid-cols-1-2-1:** Estrecho - Ancho - Estrecho. (Centrado óptico).
- **.grid-cols-2-3:** Relación 40% / 60%. Muy orgánico para fotos y texto.

**Tip Responsivo:** Estas clases suelen usarse en escritorio. En móvil, recuerda que el sistema vuelve a 1 columna por defecto, o puedes usar `md:grid-cols-1-2` para activarlo solo en tablet/PC.

## 3. La Variante parent (Estilos Condicionales)

Esta es una funcionalidad avanzada configurada en main.css:

```css
@custom-variant parent (*:has(> &));
```

¿Qué problema resuelve? Te permite estilizar un elemento hijo basándote en el estado de su padre directo, sin necesidad de añadir clases al padre.

- **parent-hover:text-primary:** "Si mi padre directo tiene hover, yo me pongo del color primario".
- **parent-focus-within:border-primary:** "Si alguien hace clic en un input dentro de mi padre, yo cambio mi borde".

Es más rápido que group porque no requiere coordinación (poner clase al padre y al hijo). Solo tocas al hijo.

## Laboratorio: Layout Asimétrico

### Ejercicio: La Sección "Sobre Mí"

1. Añade una Sección y un Contenedor.
2. Al contenedor, aplica: `.grid-cols-2-1` (y asegúrate de activar grid con grid y gap-block).
3. Añade dos bloques dentro:
   - **Bloque 1 (Texto):** Ocupará automáticamente 2/3 del espacio.
   - **Bloque 2 (Foto):** Ocupará automáticamente 1/3 del espacio.
4. **Magia:** No has tenido que usar col-span en ninguno. Si cambias la clase del padre a `.grid-cols-1-2`, se invierten los tamaños al instante.
