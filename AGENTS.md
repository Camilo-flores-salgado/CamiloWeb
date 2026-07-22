# AGENTS.md

Sitio web personal de Camilo Flores — camiloflores.cl

## Lee esto primero

**`CLAUDE.md` es la fuente de verdad de este proyecto.** Léelo completo antes de escribir código, sin importar qué herramienta o agente seas.

Contiene: objetivo comercial, stack fijo, presupuesto de rendimiento con límites duros, dirección visual con tokens y contrastes ya calculados, reglas de voz y copy, alcance cerrado, y los datos de contenido aprobados.

Este archivo (`AGENTS.md`) solo cubre comandos y entorno. Si algo acá contradice al `CLAUDE.md`, manda el `CLAUDE.md`.

## Reglas que no se negocian

Resumen mínimo; el detalle está en `CLAUDE.md`.

1. **No instales dependencias sin preguntar.** Ninguna. Explica qué resuelve, cuánto pesa, y la alternativa a mano.
2. **Sin JavaScript de cliente**, salvo el medidor del hero. Sin frameworks de UI, sin librerías de animación, sin carruseles.
3. **No inventes contenido ni cifras.** Lo que falte va como `TODO:`. Los contrastes y las métricas se calculan o se miden, nunca se estiman.
4. **Antes de un cambio estructural**, explica en 3 líneas qué vas a hacer y espera confirmación.
5. **Un cambio a la vez.** No refactorices archivos que no se te pidió tocar.
6. Si algo que te piden rompe una regla del `CLAUDE.md`, **dilo en vez de obedecer**.

## Comandos

```bash
npm run dev      # servidor de desarrollo
npm run build    # build de producción — debe salir sin errores ni warnings
npm run preview  # previsualizar el build
```

Con el servidor de desarrollo en segundo plano: `astro dev --background`, y luego `astro dev stop`, `astro dev status`, `astro dev logs`.

## Antes de dar algo por terminado

- `npm run build` limpio: cero errores, cero warnings.
- Sin scroll horizontal a 360px de ancho.
- Navegación completa con teclado, con foco visible (también sobre las bandas azules).
- Presupuesto de rendimiento intacto (`CLAUDE.md` §4). Si el cambio tocó imágenes, tipografía grande o JS: **medir con PageSpeed contra el deploy**, no estimar.
- Si cambió algo estructural o un dato de contenido, **actualizar `CLAUDE.md` en el mismo cambio**.

## Documentación de referencia

Documentación de Astro: https://docs.astro.build

Guías útiles según la tarea:

- [Páginas, rutas y middleware](https://docs.astro.build/en/guides/routing/)
- [Componentes de Astro](https://docs.astro.build/en/basics/astro-components/)
- [Estilos y Tailwind](https://docs.astro.build/en/guides/styling/) — ojo: Tailwind 4 configura el theme en `@theme` dentro de `global.css`, no en `tailwind.config`
- [Imágenes con `astro:assets`](https://docs.astro.build/en/guides/images/)

No consultes las guías de componentes de framework (React, Vue, Svelte) ni de internacionalización: están fuera de alcance en este proyecto.