# Especificación de componentes — Design System La Nación (Core)

Fuente: archivo de Figma "C – Core" (estructura y variantes) + exports de variables de Figma.

## Archivos de tokens (no modificar: se generan desde Figma)

Orden de carga en el HTML:
1. `global-primitives.css`: [BASE] Primitive (Global).
2. `foodit.css`: foundations de la marca (--foo-*).
3. `core-semantic.css`: tokens de Core. **Los componentes usan SOLO estas variables.**

Marca y modo se definen en `<html>`: `<html data-brand="foodit">` y, para modo oscuro, `data-mode="dark"`.

Reglas:
- No usar valores fijos (hex, px) en componentes. Si falta un token, dejar `/* TODO: token no definido en Figma */`.
- No usar variables `--foo-*` directamente en componentes: siempre pasar por Core.
- Tipografía: `font-family: var(--font-secondary), sans-serif;` en UI y `var(--font-primary), serif` en títulos editoriales. Interlineados: 1 (labels), 1.2 (títulos, small), 1.5 (body).

## Convención de color de Core

Intenciones: `primary`, `secondary`, `accent`, `subscription`, `error`, `black`, `white`, `base`, `info`, `success`, `warning`.
Para cada una existen, en tres capas:
- Fondo: `--bg-{intención}-default | -dark | -light | -lighten | -foreground`
- Texto: `--text-{intención}-...`
- Borde: `--border-{intención}-...`
- Transparencias: `--bg-{intención}-default-opacity-15` y `-opacity-60`.

Neutros: `--bg-neutral-{1…999}`, `--text-neutral-{…}`, `--border-neutral-{…}`. Otros: `--bg-muted`, `--bg-skeleton`, `--text-muted`, `--border-muted`.

Tamaños de texto: `--text-display-{lg,md,sm}`, `--text-heading-*`, `--text-subheading-*`, `--text-body-*`, `--text-label-{lg,md,sm}`, `--text-small-{lg,md,sm}` (responsivos por breakpoint).
Radios: `--radius-sm | -md | -lg` y por componente `--components-{componente}-radius`.
Espaciados: los de Global (`--p-*`, `--gap-*`, `--size-*`) y responsivos `--p-responsive`, `--gap-responsive`.

---

## Button

**Propiedades**: `variant` solid | outline | ghost · `color` primary | secondary | accent | subscription | error | black | white · `size` 48 | 40 | 32 · `state` default | hover | loading | disabled · `isOnlyIcon` · ícono opcional a izquierda y derecha.

**Medidas**
- Radio `--components-button-radius`. Borde (outline) `--components-button-weigth`.
- Padding horizontal: 48 → `--p-20`, 40 → `--p-12`, 32 → `--p-8`. Gap: `--gap-8` (32 → `--gap-4`).
- Ícono: 48 → `--size-20`, 40 → `--size-16`, 32 → `--size-12`.
- Texto en mayúsculas, bold, interlineado 1: 48 → `--text-label-lg`, 40 → `--text-label-md`, 32 → `--text-label-sm`.
- `isOnlyIcon`: ancho = alto.

**Colores**
- Solid: fondo `--bg-{color}-default`, texto `--text-{color}-foreground`. Hover `--bg-{color}-light`. Disabled `--bg-{color}-lighten`.
- Outline: borde `--border-{color}-default`, texto `--text-{color}-default`. Hover `-light`. Disabled `-lighten`.
- Ghost: texto `--text-{color}-default`. Hover fondo `--bg-{color}-default-opacity-15` (excepciones de nombre en Figma: black → `--bg-black-999-opacity-15`, white → `--bg-white-1-15`). Disabled texto `--text-{color}-lighten`.
- White: pensado para fondos oscuros.
- Loading: spinner en lugar del contenido, manteniendo el ancho.

---

## Input

**Propiedades**: `labelType` floating | fixed · `color` default | gray | error · `size` 56 | 48 · `state` enabled | hover | focus | disabled (error sin disabled) · ícono opcional izquierda/derecha con separador vertical · supporting text con ícono opcional.

**Medidas**: radio `--components-input-radius`, borde `--border-sm`, padding horizontal `--p-12`, gap `--gap-8`. Texto del campo `--text-label-lg` (56) / `--text-label-md` (48). Label y supporting text `--text-label-sm`.
Floating label: en focus o con valor, sube sobre el borde superior con fondo `--bg-neutral-1`. Fixed label: arriba del campo, a `--gap-4`.

**Colores**
- Default: borde `--border-base-light`; hover `--border-base-default`; focus `--border-base-dark` (2px).
- Gray: fondo `--bg-neutral-50`.
- Error: borde y texto `--border-error-default` / `--text-error-default`; hover `-light`; focus `-dark`.
- Disabled: borde `--border-base-lighten`, texto `--text-base-lighten`.
- Placeholder: `--text-base-light`.

---

## Chip

**Propiedades**: `type` informative | clickable | closable · `variant` solid | outline | ghost · `color` primary | secondary | accent | error | black | white · `size` 30 | 24 · `state` default | hover | disabled (informative solo default) · ícono opcional; closable agrega separador y "×".

**Medidas**: radio `--components-chip-radius`, padding 30 → `--p-8` / 24 → `--p-6`, gap `--gap-4`. Texto bold: 30 → `--text-label-md`, 24 → `--text-label-sm`. Ícono 30 → `--size-14`, 24 → `--size-12`.

**Colores**: misma lógica que Button. Ghost hover: fondo `--bg-{color}-light` con texto `--text-{color}-foreground`.

---

## Badge (validar contra la página Badge de Core)

`color` primary | secondary | accent | subscription | error | black | white · `variant` solid | outline. Radio `--components-Badge-radius`. Padding `--p-4` a `--p-8`, gap `--gap-2`/`--gap-4`. Texto bold en mayúsculas: `--text-label-md`, `--text-label-sm` o `--text-small-md`. Sobre imágenes: fondo `--bg-neutral-1-60` o `--bg-neutral-999-60`.

---

## Alert

`type` success | info | warning | error | skeleton · `style` light | solid. Estructura: ícono circular (`--size-24`) + título + descripción + slot opcional.
Radio `--components-alert-radius`, padding `--p-16`, gap `--gap-8`. Título bold `--text-body-lg`; descripción `--text-body-sm`.
- Light: fondo `--bg-{type}-lighten`, borde `--border-{type}-default`, título `--text-{type}-default`, descripción `--text-base-default`.
- Solid: fondo `--bg-{type}-default`, texto `--text-{type}-foreground`.
- Títulos de ejemplo: "¡Listo!", "Información", "¡Atención!", "¡Uppps!".
- Skeleton: bloques `--bg-skeleton`, borde `--border-skeleton`.

## Toast
Radio `--components-toast-radius`. Mismos tipos que Alert. Sombra: `/* TODO: token de sombra no definido en Figma */`.

## Card
Fondo `--bg-neutral-1`, borde `--border-sm` color `--border-muted`, radio `--radius-md`. Título bold `--text-body-lg`, texto `--text-body-md` color `--text-base-light`. Imagen superior con placeholder `--bg-skeleton`.
