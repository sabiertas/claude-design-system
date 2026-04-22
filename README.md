# Flowtitude Design System — Claude Design package

Versión del Flowtitude Design System (FDS) preparada para importarse en
[Claude Design](https://claude.ai/design).

## Qué contiene

- `DESIGN.md` — sistema de diseño en formato estándar de 9 secciones que Claude
  Design parsea para generar tokens, componentes y previews.
- `src/` — código fuente real del FDS (Tailwind v4 + OKLCH). Es la fuente de
  verdad: tokens, componentes, layouts y utilidades CSS.
- `patterns/` — recetas reutilizables (landing CRO, hero, etc.) para enriquecer
  las generaciones.

## Cómo importarlo en Claude Design

1. Conectar el repo `sabiertas/<repo>` desde la cuenta Claude (Pro/Max/Team).
2. Durante el onboarding del proyecto, seleccionar este repositorio como
   design system base.
3. Claude lee `DESIGN.md` + `src/` y construye el sistema (paleta, tipografía,
   componentes) que aplicará a cada generación.

Para refinar: editar `DESIGN.md` o añadir más patterns en `patterns/`.

## Origen

Sincronizado desde `clientes/flowtitude/flowtitude-design-system/` (fuente
canónica). Patterns adaptados de `tooling/design-md/patterns/`.

No editar `src/` directamente — esos cambios deben hacerse en la fuente
canónica y volver a sincronizarse aquí.
