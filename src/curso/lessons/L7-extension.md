# Lección 7: Extendiendo el sistema

El Sistema Core no es una jaula cerrada; es un cimiento sólido sobre el que construir. La filosofía de Flowtitude es: «Usa los defaults para ir rápido, personaliza para ser único».

En esta lección aprenderemos a modificar los valores globales y, lo más importante, a crear tus propios componentes CSS integrados en la arquitectura del sistema.

## 1. Modificar los Defaults (flowtitude.css)

¿El espaciado te parece muy grande? ¿La tipografía muy pequeña? No luches contra el sistema sobrescribiendo clases. Ve a la fuente.

En theme/flowtitude.css, tienes los controles maestros.

- **Cambio Global de Escala:** Si quieres que toda la web sea más compacta, cambia --ft-space-factor de 1 a 0.8. Todas las variables de espacio (--spacing-section, --spacing-block) se reducirán proporcionalmente al instante.
- **Tipografía:** Ajusta --ft-text-min si sientes que el texto base en móvil es ilegible.

## 2. Añadir tus Propios Componentes

Seguramente en tu proyecto necesites algo que el Core no trae, por ejemplo: una tarjeta de producto específica o un estilo de acordeón.

**La Mala Práctica:** Escribir CSS suelto en el panel de «CSS Personalizado» de Bricks o en el ID del elemento. Eso se vuelve inmanejable.

**La Buena Práctica (Arquitectura):**

1. **Crea el archivo:** Ve a la carpeta components/ y crea un archivo nuevo, por ejemplo product-card.css.

2. **Define tu clase:** Usa @apply para componer utilidades de Tailwind.

```css
/* components/product-card.css */
.card-product {
  @apply border rounded-xl p-4 transition-shadow hover:shadow-lg;
  background-color: var(--color-neutral-100);
}
```

3. **Conéctalo al Cerebro:** Abre main.css y añade la importación en la sección de componentes:

```css
@import './components/buttons.css';
@import './components/custom.css';
@import './components/product-card.css'; /* <-- Tu nuevo archivo */
```

Al hacer esto, tu nueva clase .card-product estará disponible en el autocompletado de Bricks y se compilará optimizada junto con el resto del sistema.

## 3. El Archivo custom.css (Para cosas rápidas)

Si solo vas a añadir una clase pequeña (como .tag o .badge) y no merece la pena crear un archivo nuevo, usa components/custom.css. Este archivo está pensado como un "cajón de sastre" ordenado para estilos específicos del proyecto actual.

## 4. Actualizaciones del Sistema

Si en el futuro lanzamos una versión v1.2 del Core con mejoras en layout/grid-basic.css, podrás reemplazar ese archivo sin miedo a perder tus estilos personalizados, porque tus cambios viven en custom.css o en tus propios archivos de componentes, y tu configuración vive en flowtitude.css.
