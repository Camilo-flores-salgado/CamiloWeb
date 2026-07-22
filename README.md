# camiloflores.cl

Sitio personal de Camilo Flores — desarrollador web en San Felipe, Valle de Aconcagua, Chile.

Es la herramienta de cierre de un negocio de sitios web para PyMEs locales: alguien con quien ya conversé entra, entiende qué hago y cuánto cuesta en menos de 40 segundos, y me escribe por WhatsApp.

**En vivo:** https://www.camiloflores.cl

---

## Por qué está hecho así

El sitio vende una promesa concreta: *sitios que cargan en menos de un segundo*. Un sitio lento, pesado o genérico refutaría el argumento en el primer scroll. Así que el sitio **es** la demostración, no la descripción.

De ahí salen casi todas las decisiones: sin frameworks de UI, sin librerías, sin banner de cookies, sin imágenes salvo una, y un presupuesto de rendimiento tratado como requisito y no como aspiración.

## Métricas

PageSpeed Insights, móvil, 20 de julio de 2026. Emulando un Moto G Power con 4G lenta — deliberadamente el peor caso, porque es el dispositivo real del cliente objetivo.

| | |
|---|---|
| Rendimiento | **100** |
| Accesibilidad | **100** |
| Prácticas recomendadas | **100** |
| SEO | **100** |
| Navegación agéntica | 3/3 |
| LCP | 1,5 s |
| CLS | **0** |
| TBT | **0 ms** |
| Peso de la home | ~56 KB comprimido |
| Requests | 8 |
| JS de cliente | ~1 KB |

El CLS en 0 y el TBT en 0 ms no son casualidad: son consecuencia directa de las decisiones de abajo.

## Stack

- **Astro 5** en `output: 'static'` — HTML pre-generado, cero runtime
- **TailwindCSS 4** vía `@tailwindcss/vite`, con el theme en `@theme` dentro de `global.css`
- **TypeScript** en modo `strict`
- **Cloudflare** para hosting y analítica sin cookies
- Sin React, Vue, Svelte ni ningún framework de UI
- Sin librerías de animación, íconos, fechas ni utilidades

`package.json` tiene menos de 10 dependencias, a propósito.

## Decisiones técnicas

**Cero frameworks de UI.** Un sitio de tres páginas no necesita 40 KB de runtime. Astro sin islas envía 0 KB de JavaScript, y ese cero es el argumento comercial hecho código.

**El único JavaScript es un medidor.** El hero muestra el tiempo de carga real de la propia página, medido en vivo con `performance.now()`. Son unas pocas líneas de vanilla inline: la tesis del negocio demostrada en vez de afirmada.

**CLS en 0 por construcción.** El número del medidor se llena por JS después del render, que es exactamente el escenario que genera saltos de layout. Se resuelve con `tabular-nums` más un placeholder (`0,00`) del mismo ancho que el valor final: al reemplazarse, nada se mueve. Toda tipografía va precargada y toda imagen lleva `width` y `height`.

**Tipografías self-hosted, subset latino.** Dos archivos `woff2`, sin CDN de terceros, precargados. Nada de Google Fonts por red.

**Sin banner de cookies.** La analítica de Cloudflare no usa cookies, así que no hay banner que mostrar. Es simultáneamente más rápido (30 KB de JS que no se cargan), más privado y menos fricción para el visitante.

**WhatsApp en vez de formulario.** El cliente objetivo no llena formularios. Un enlace `wa.me` con mensaje pre-cargado convierte mejor y no requiere backend.

**Contrastes calculados, no estimados.** Los pares de color están verificados contra WCAG y anotados en `CLAUDE.md`. El texto de cuerpo cumple AAA. Nada se atenúa con `opacity`: si un tono no alcanza el ratio, se cambia el color.

**Diseño con concepto propio.** La dirección visual es señalética comercial pintada del valle: letrero de esmalte sobre pared encalada. Bandas de color a sangre completa, textura de cal en un data URI de ~350 bytes, tipografía de letrero. La intención es no parecerse ni a una plantilla ni al gradiente violeta que produce cualquier generador.

## Estructura

```
src/
  pages/          index.astro, sobre-mi.astro, 404.astro
  components/     carpeta plana
  layouts/        Base.astro
  styles/         global.css — tokens, @font-face, escala tipográfica, textura
  assets/         imágenes procesadas por astro:assets
public/           robots.txt, llms.txt, favicon, og.png
```

## Comandos

```bash
npm install      # instalar dependencias
npm run dev      # servidor de desarrollo en localhost:4321
npm run build    # build de producción a ./dist/
npm run preview  # previsualizar el build
```

## Documentación del proyecto

- **`CLAUDE.md`** — fuente de verdad: objetivo, stack, presupuesto de rendimiento, dirección visual con tokens y contrastes, reglas de voz, alcance y datos de contenido aprobados.
- **`AGENTS.md`** — comandos y entorno para agentes de código; apunta a `CLAUDE.md` para todo lo demás.
- **`IDEAS.md`** — lo que queda deliberadamente fuera de alcance, con el porqué de cada descarte.

El proyecto se desarrolla con Claude Code. `CLAUDE.md` existe para que la herramienta respete el concepto y el presupuesto en vez de producir el sitio genérico de siempre.

## Proyecto relacionado

**Encuentro PyME Aconcagua** — sitio de demostración de un seminario ficticio, con formulario de inscripción real (Cloudflare Worker + Resend) que funciona sin JavaScript de cliente, mediante envío nativo del formulario. Repo, deploy y paleta independientes.

## Licencia

El código es de referencia; el contenido, la identidad visual y los textos son propios y no se reutilizan sin permiso.