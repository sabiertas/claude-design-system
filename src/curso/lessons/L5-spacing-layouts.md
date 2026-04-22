# Lección 5: Layout básico y estructural

En esta lección vamos a ver por qué este sistema te ahorra el 80% de los clics rutinarios. Normalmente, cada vez que creas una sección en Bricks, tienes que:

1. Ajustar el padding vertical.
2. Añadir un contenedor.
3. Configurar Flexbox para centrar el contenido.

En el Sistema core, estas decisiones están automatizadas en dos archivos clave: section.css y content-flex.css.

## 1. El patrón «sección Inteligente» (section.css)

El sistema detecta automáticamente cuando usas la etiqueta HTML `<section>` y aplica una lógica de ritmo vertical basada en el contexto.

### A. La lógica por defecto (medios paddings)

Al arrastrar una Sección normal (fondo blanco sobre fondo blanco), el sistema aplica:

- `py-[calc(var(--ft-padding-content-y)/2)]` (Medio padding arriba y abajo).

¿Por qué? Porque si apilas dos secciones normales, la suma del padding inferior de la primera (0.5) y el superior de la segunda (0.5) da como resultado 1 unidad completa (--spacing-section). El ritmo se mantiene perfecto sin duplicar espacios.

### B. La clase .has-background (El cambio de contexto)

Si añades un color de fondo a una sección, rompes la continuidad visual. Necesitas más aire para que el contenido no parezca "pegado" al borde del color.

Al añadir .has-background, ocurren tres cosas automáticamente:

1. **En la propia sección:** El padding pasa a ser completo (1x arriba y abajo).
2. **En la sección ANTERIOR:** Se le fuerza un padding-bottom completo (1x).
3. **En la sección SIGUIENTE:** Se le fuerza un padding-top completo (1x).

**Resultado:** El bloque de color queda perfectamente aislado con el espacio correcto por todos lados, sin que tengas que ir a las secciones vecinas a ajustarlo manualmente.

### C. Control manual (.half-top / .half-bottom)

A veces querrás romper esta lógica automática.

- **.half-top:** Fuerza medio padding arriba (útil si la sección anterior ya tiene mucho espacio vacío).
- **.half-bottom:** Fuerza medio padding abajo.
- **.block-bleed:** Hace que un elemento hijo rompa el ancho del contenedor y ocupe el 100% de la pantalla (100vw).

## 2. La Navaja Suiza: .content-flex (content-flex.css)

Esta es la utilidad que usarás el 90% del tiempo para tarjetas, cabeceras y bloques de contenido. Olvídate de configurar Flexbox manualmente cada vez.

**La Clase Base (.content-flex):** Aplica automáticamente:

- **flex-col:** Apila elementos (Título, Texto, Botón).
- **justify-center items-center:** Centra todo por defecto.
- **gap-content:** Aplica el espaciado semántico estándar.

### El Sistema de Coordenadas

No toques los controles de alineación de Bricks. Usa las clases modificadoras para mover el contenido:

| Clase | Efecto Visual | Qué hace el CSS |
|---|---|---|
| content-flex center | Centrado (Default) | text-center mx-auto |
| content-flex left | Izquierda | items-start text-left mr-auto |
| content-flex right | Derecha | items-end text-right ml-auto |
| content-flex top-left | Arriba Izquierda | justify-start items-start |
| content-flex bottom-right | Abajo Derecha | justify-end items-end |

¿Por qué usar esto? Porque gestiona tres cosas a la vez con una sola clase:

1. **Alineación Flex** (Ejes X/Y).
2. **Alineación de Texto** (text-center vs text-left).
3. **Márgenes Automáticos** (mx-auto vs mr-auto) para que el bloque ocupe solo el ancho necesario.

## Laboratorio: Práctica de layout

### Ejercicio: Hero Section en 30 segundos

1. Añade una Sección. (Automáticamente tiene padding y contenedor).
2. Añade un Div.
3. Ponle la clase `content-flex center`.
4. Dentro pon: H1, Párrafo y Botón.
5. **Resultado:** Todo está perfectamente centrado, con el espacio correcto entre elementos y tipografía alineada, sin haber tocado ni un solo ajuste de estilo en el panel.
