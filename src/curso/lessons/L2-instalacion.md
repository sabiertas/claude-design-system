# Lección 2: Descarga e instalación en WindPress

Ya entendemos la filosofía: queremos un centro de control unificado. Ahora vamos a instalar el motor que lo hace posible.

Para gestionar Tailwind CSS dentro de WordPress y Bricks, utilizaremos WindPress. Es la herramienta que nos permite compilar todo este sistema en tiempo real sin necesidad de servidores externos ni configuraciones complejas de Node.js.

## 1. ¿Qué vas a instalar? (Anatomía del Sistema)

No te voy a dar un archivo CSS gigante de 5.000 líneas imposible de leer y mantener. El Sistema Core sigue una arquitectura modular profesional, diseñada para que sepas dónde está cada cosa.

Si miras el archivo principal (main.css), verás que actúa como un índice. No contiene estilos, solo importa las piezas del sistema en un orden lógico:

```css
/* main.css - El cerebro de operaciones */
@layer theme, base, layouts, components, utilities;

/* 1. CONFIGURACIÓN (Tu Centro de Control) */
@import './theme/flowtitude.css'; /* <--- Aquí viven tus variables y decisiones */

/* 2. CIMIENTOS */
@import './base/base.css'; /* Resets y normalización */
@import './base/typography.css'; /* Estilos base para H1-H6 y Prose */

/* 3. ESTRUCTURA */
@import './layouts/section.css'; /* El sistema de secciones inteligentes */
@import './layouts/content-flex.css'; /* La utilidad mágica de alineación */

/* 4. ELEMENTOS UI */
@import './components/buttons.css'; /* Botones pre-diseñados */
@import './components/components.css'; /* Utilidades de interacción */

/* 5. UTILIDADES Y HERRAMIENTAS */
@import './utility/core/utilities.css'; /* Helpers generales */
@import './utility/animations/durations.css'; /* Control de tiempos de animación */
@import './utility/layout/grid-basic.css'; /* Sistemas de Grid extra */
```

¿Por qué esta estructura?

- **Orden Mental:** Si quieres cambiar la velocidad de una animación, vas a utility/animations. Si quieres cambiar el color de un botón, vas a components/buttons.css. Si quieres cambiar el espaciado global, vas a theme/flowtitude.css.
- **Seguridad:** Al separar la "Lógica" (base/, layouts/, utility/) de la «Configuración» (theme/), evitas romper el sistema accidentalmente. Tú solo necesitas tocar el archivo de configuración; el resto funciona solo.

## 2. Pasos de Instalación

El proceso en WindPress es increíblemente sencillo porque hemos empaquetado todo para que sea «Plug & Play».

### Paso 1: Descarga el Paquete Core

Descarga el archivo adjunto en esta lección. fds-core.windpress

### Paso 2: Importación en un Clic

1. Ve a tu panel de WordPress > WindPress.
2. Busca la opción de Importar (generalmente un icono de flecha hacia arriba o "Import Structure").
3. Selecciona el archivo que acabas de descargar.
4. Dale a Importar.

⚠️ **ADVERTENCIA CRÍTICA:** Esta acción recreará toda la estructura de archivos CSS en WindPress.

- **Web Nueva:** ¡Perfecto! Es la forma más rápida de empezar.
- **Web Existente:** Si ya tenías configuración en WindPress, este proceso la sobrescribirá. HAZ UNA COPIA DE SEGURIDAD (Exportar) de tu configuración actual antes de importar el sistema Flowtitude.

### Paso 3: Verificación Rápida

Guarda los cambios y abre una página cualquiera con Bricks Builder.

- Añade una Sección.
- Si ves que automáticamente tiene un padding generoso y el fondo de la web no es blanco puro (gracias a base.css), el sistema está vivo.
