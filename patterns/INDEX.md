# Patterns

Recetas reutilizables para enriquecer las generaciones de Claude Design.
Cada pattern asume que el FDS ya está cargado.

## Disponibles

- [landing-cro](./landing-cro.md) — landing optimizada para conversión
  (estructura, jerarquía, CTAs, prueba social).
- [section-hero](./section-hero.md) — sección hero con variantes
  (asymmetric, editorial, gradient).

## Cómo añadir uno nuevo

1. Crear `patterns/{nombre}.md` con: contexto, estructura, ejemplo HTML,
   variantes, errores comunes.
2. Añadir entrada en este INDEX.
3. Si es muy específico de marca, va en `src/` o en el repo del cliente,
   no aquí.
