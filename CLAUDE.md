# CLAUDE.md

Instrucciones permanentes para este repositorio. Léelas completas antes de escribir código.

Este archivo es la **fuente de verdad** del proyecto. Si `AGENTS.md` u otro archivo dice algo distinto, manda este.

---

## 0. Estado actual — léelo primero

**Última actualización:** julio 2026.

El sitio **está publicado y andando** en camiloflores.cl. v1 se cerró; ahora estamos en v1.1 (mejoras estéticas y prueba social).

Hecho y funcionando:
- Home y Sobre mí completas, con el sistema visual de bandas (§5).
- Medido con PageSpeed en móvil (20 jul 2026): **Rendimiento 100, Accesibilidad 100, Prácticas 100, SEO 100**, Navegación agéntica 3/3. LCP 1,5 s · CLS **0** · TBT **0 ms** (emulando Moto G Power con 4G lenta). Datos de campo (CrUX) todavía sin volumen: normal en un sitio nuevo.
- Cloudflare Web Analytics activo. Imagen OG generada.
- Testimonio real de cliente publicado (§12).
- Sección "Ejemplo" enlazando el sitio de demostración (§12).

**El sitio ya no es el cuello de botella.** Lo que falta es comercial, no técnico (§13).

---

## 1. Qué es esto

Sitio web personal de Camilo, desarrollador web en San Felipe, Región de Valparaíso, Chile.

**Objetivo comercial único:** que un dueño de PyME del Valle de Aconcagua que ya habló conmigo (o que recibió una auditoría mía) entre al sitio, confíe, y me escriba por WhatsApp.

**El sitio no es un canal de captación.** Es el cierre. Nadie llega acá por Google. Llega porque le hablé antes. Su trabajo es convertir una conversación tibia en un mensaje.

**Audiencia real:** dueño o dueña de un negocio local — viña, clínica dental, ferretería, turismo, agro. 35-60 años. Entra desde un Android de gama media con datos móviles. No sabe qué es un framework. No le importa. Tiene 40 segundos.

**Audiencia que NO es:** otros desarrolladores, reclutadores, Hacker News.

### Estado honesto del proyecto (actualizado)

Hay **un** caso con cliente real: el sitio de GVE Sistemas, con testimonio publicado de Gonzalo Toro, CEO de ITQ Internacional (permiso explícito concedido). Ese sitio ya no está en línea porque la empresa cerró: **no se enlaza ni se insinúa que siga vivo**. Si alguien pregunta, se dice la verdad de frente.

Hay además un antecedente laboral: trabajo como desarrollador en una empresa de tecnología chilena con presencia internacional. Eso es **credencial**, no portafolio. Va en "Sobre mí", nunca como caso de éxito propio. No se nombra la empresa hasta tener permiso explícito, ni se dan detalles que la identifiquen 1:1.

Y hay **un sitio de demostración** propio (§12), claramente rotulado como demostración.

La postura pública es: *recién estoy por mi cuenta, tengo un cliente real, y mis primeros 3 proyectos van a precio de lanzamiento.* **No se infla nada:** hay un cliente, no una cartera. Sin testimonios falsos, sin logos de "clientes", sin "+50 proyectos".

---

## 2. Regla de oro

> Ante cualquier decisión, pregunta: **¿esto ayuda al dueño de la viña a decidir, o me hace ver inteligente a mí?**

Si es lo segundo, no va.

Corolario: **la excelencia técnica de este sitio debe ser invisible.** Se percibe como velocidad y claridad, nunca se menciona. El sitio no habla de sí mismo.

### Honestidad — el pilar que sostiene todo

Es el diferenciador real, no un adorno. Reglas duras:

- No se afirma nada que no sea verdad, ni por omisión ni por encuadre.
- Nada de prueba social inventada, cifras sin medir, ni promesas que no se pueden cumplir (por eso no existe el "24/7", §12).
- Todo contenido ficticio (demos) va **rotulado como demostración**, visible, sin letra chica.
- **Nunca** se atribuye una identidad falsa a una persona real: prohibido usar fotos de personas reales (de bancos de imágenes o generadas) para representar clientes, testimonios o relatores inventados.
- Antes de publicar el nombre, cargo o empresa de alguien, se pide permiso explícito.
- Si una cifra no está medida, no se publica. Ver §11 punto 1.

---

## 3. Stack — fijo, no negociable

| Capa | Decisión |
|---|---|
| Framework | Astro 5, `output: 'static'` |
| Estilos | TailwindCSS 4 vía `@tailwindcss/vite` |
| Lenguaje | TypeScript, `strict: true` |
| Islas / UI framework | **Ninguno.** Sin React, Vue, Svelte, Solid |
| JS de cliente | Vanilla, inline, mínimo |
| Imágenes | `astro:assets` → AVIF, con `width`/`height` y `loading="lazy"` |
| Tipografías | Self-hosted vía `@fontsource-variable`, subset latino, `woff2` |
| Íconos | SVG inline pegado a mano. Sin librerías de íconos |
| Analítica | Cloudflare Web Analytics (sin cookies) |
| Hosting | Cloudflare, deploy automático desde la rama de producción del repo |
| Dominio | camiloflores.cl |
| Contacto | Link `wa.me` con `?text=` pre-cargado. Sin formularios |
| CMS | Ninguno |

`TODO:` confirmar si el proyecto en Cloudflare es **Pages** o **Worker con assets estáticos**, y anotarlo acá. No es cosmético: define dónde iría cualquier endpoint futuro (`/functions` solo existe en Pages) y si se pueden agregar variables de entorno. El proyecto del demo resultó ser un Worker con assets.

### Prohibiciones de dependencias

**No instales nada sin preguntar primero.** Ni una. Si crees que hace falta un paquete, detente, explica qué problema resuelve, cuánto pesa, y propón la alternativa a mano. Yo decido.

Prohibido explícitamente: librerías de animación (GSAP, Framer Motion, AOS), carruseles, librerías de íconos, librerías de fechas, lodash, jQuery, cualquier UI kit, cualquier cosa que agregue JS al cliente.

`package.json` debería tener menos de 10 dependencias. Si tiene más, algo salió mal.

### Proyectos relacionados (NO tocar desde acá)

El sitio de demostración "Encuentro PyME Aconcagua" vive en **otro repo, con otro deploy, otra paleta y su propio CLAUDE.md**. No comparten código ni estilos. Desde este repo solo se lo enlaza.

---

## 4. Presupuesto de rendimiento — límites duros

Requisitos, no aspiraciones. Un cambio que los rompe no se mergea.

- **JS enviado al cliente: < 2 KB** (comprimido), sin contar el beacon de Cloudflare Web Analytics. El objetivo es 0. El único JS propio del sitio es el medidor del hero.
- **Peso total de la home: < 120 KB** comprimido, incluyendo tipografías e imágenes. Referencia medida: ~56 KB antes de sumar la captura del ejemplo.
- **Imágenes:** el sitio es casi sin imágenes a propósito. Cada imagen nueva debe justificarse y pesar **< 50 KB** en AVIF. Todas van bajo el pliegue, con `loading="lazy"` y tamaño declarado. Ninguna imagen puede convertirse en el elemento LCP.
- **LCP: < 1,0 s** ideal. Aceptable hasta 1,5 s en la simulación de PageSpeed (Moto G Power + 4G lenta), que es deliberadamente el peor caso.
- **CLS: < 0,01.** Hoy está en 0 y ahí se queda. Toda imagen con `width`/`height`; toda tipografía precargada; todo número que se llene por JS con ancho reservado (`tabular-nums` + placeholder del mismo ancho).
- **INP: < 100 ms.** Hoy TBT 0 ms.
- **Requests en la home: < 12.** Referencia medida: 8.
- Lighthouse 100/100/100/100 en móvil es el **piso**, no la meta.

Reglas derivadas:
- Sin banner de cookies. Nunca. Si algo exige uno, ese algo no entra.
- Sin fuentes de terceros. Sin Google Fonts por CDN.
- Sin embeds de terceros (YouTube, Maps, widgets). Si hace falta un mapa, es un link.
- Máximo **3 archivos de tipografía**.
- Todo el CSS crítico inline; Astro ya lo hace, no lo desarmes.
- **Medir, no estimar.** Tras cualquier cambio que toque imágenes, tipografía a gran tamaño o JS, correr PageSpeed contra el deploy y comparar con los números de §0.

---

## 5. Dirección visual

**Concepto:** señalética comercial pintada del Valle de Aconcagua. Letrero de esmalte sobre pared encalada. Sobrio, alto contraste, plano, hecho para leerse desde lejos y bajo sol.

El concepto se ejecuta **en positivo**, no solo prohibiendo cosas. Un error pasado fue construir solo las prohibiciones: el resultado quedó correcto pero plano y sin carácter. El material (cal, esmalte), la escala tipográfica y el ritmo de color son el diseño.

**Prohibido** (esto es el look genérico de sitio generado con IA, y usarlo refuta el argumento comercial completo del sitio):
- Fondo oscuro con gradiente violeta/azul
- Cards con `blur`, `glow`, bordes luminosos, glassmorphism
- Inter, Poppins, Montserrat
- Modo oscuro
- Gradientes de cualquier tipo
- Animaciones al hacer scroll, parallax, scroll-jacking, fondos fijos
- Patrones de grilla / papel milimetrado de fondo (el default de todo clon de SaaS)
- Blobs, mallas, patrones de puntos, ruido decorativo
- Emojis como íconos
- Marcadores numerados 01 / 02 / 03 salvo que el contenido sea realmente una secuencia
- Carruseles y sliders: si hay pocos elementos, van en grilla

### Tokens

```css
--cal:      #EFF0EC;  /* fondo — encalado, gris-verdoso frío */
--tinta:    #171A17;  /* texto — casi negro con fondo verde */
--azul:     #0E3FA8;  /* acento único — esmalte de letrero */
--parra:    #4C6B3C;  /* verde parra — etiquetas, cifras buenas */
--rojo:     #C8322D;  /* solo para señalar el problema del cliente */
--borde:    #D5D8D0;  /* líneas hairline */
```

Un solo acento: `--azul`. `--rojo` aparece **únicamente** cuando se muestra el dolor (un sitio lento, una cifra mala). El color codifica verdad, no decora.

Sin sombras — la regla es sobre la propiedad `box-shadow`, no solo sobre el efecto visual. Bordes `1px solid var(--borde)`. `border-radius: 2px` máximo — es un letrero pintado, no una app.

### Sistema de bandas (estructural)

El ritmo del sitio lo da el color, no las líneas. Cada sección va **a sangre completa**:

```html
<section class="w-full bg-{color}">
  <div class="mx-auto max-w-2xl px-6 py-16">…</div>
</section>
```

El color sangra de borde a borde del viewport; el texto queda centrado en la columna.

- **Regla de separación:** donde cambia el color de banda **no va hairline** (el cambio ya separa). El hairline `border-t border-borde` solo entre dos bandas del mismo color.
- **Textura de cal:** la clase `.bg-textura-cal` (ruido `feTurbulence` desaturado como data URI, ~350 bytes, opacidad ~0,045) va en **todas** las bandas cal y en **ninguna** banda azul. La textura es de la cal, no del esmalte.
- La banda del problema abre con una regla gruesa `border-t-[6px] border-tinta` — borde pintado de letrero.

### Contrastes ya calculados (no re-estimar)

- `cal` sobre `azul`: **7,99:1** → pasa AAA. Es el par para texto de cuerpo en bandas azules.
- `tinta` sobre `azul`: **1,92:1** → inutilizable. Por eso el botón invertido usa `outline-cal` para el foco.
- Prohibido atenuar con `opacity` para lograr jerarquía: se elige un color que cumpla el ratio.

### Tipografía

- **Display:** Archivo Expanded — titulares y cifras. **Ojo:** el archivo self-hosted es una **instancia estática en peso 700 / ancho Expanded**, no una variable con eje `wdth`. Pedir 600 o mover `font-stretch` no cambia nada. Usar `font-bold`.
- **Cuerpo:** Source Serif 4 — 400 y 600. Un serif proyecta seriedad ante este cliente y ningún portafolio de dev usa uno.
- Cifras (`0,38 s`, `5 UF`) van siempre en display, con `tabular-nums`. Son el protagonista.
- Escala tipográfica explícita en el bloque **`@theme` de `src/styles/global.css`** (Tailwind 4 no usa `tailwind.config`). Nada de tamaños arbitrarios: si falta un paso, se agrega al theme.
- **Coma decimal**, no punto. Es Chile.

### Elemento firma

El hero muestra **el tiempo de carga real de esta misma página**, medido en vivo con `performance.now()`. Es la tesis del negocio demostrada, no afirmada.

Se presenta como **lectura de instrumento**: etiqueta corta en `font-display` chica sobre `--parra`, una regla vertical de 2px en tinta, y el número grande en esmalte con `tabular-nums`. El placeholder inicial es `0,00` (mismo ancho que el valor final ⇒ CLS 0).

Ese patrón —etiqueta + regla vertical + cifra— es el lenguaje del sitio para **cualquier dato medido** (por ejemplo las métricas de la sección Ejemplo). Reutilizarlo, no inventar otro.

**No agregues un segundo elemento llamativo.** La audacia se gasta una sola vez.

### Piso de calidad
Responsive hasta 360px de ancho. Foco de teclado visible sobre cal y sobre azul. `prefers-reduced-motion` respetado. Contraste AA mínimo, AAA en cuerpo. Enlaces que abren pestaña nueva lo avisan con texto `sr-only`.

---

## 6. Voz y copy

Español de Chile. Trato de "tú", respetuoso, sin jerga, sin diminutivos, sin humor forzado.

**Palabras prohibidas en todo el sitio:**
apasionado, soluciones digitales, a medida, transformar ideas en realidad, full stack, stack, framework, landing, deploy, responsive, performance, optimizar, escalable, robusto, innovador, sinergia, potenciar, llevar tu negocio al siguiente nivel, Astro, Tailwind, JavaScript, 24/7.

Los nombres de tecnologías **no aparecen en el home**. Al cliente no le importa. Puede haber una mención sobria en Sobre mí.

**Reglas de escritura:**
- Toda afirmación lleva un número, o se borra. Y el número tiene que estar medido.
- Frases cortas. Verbos activos. Sentence case.
- Traduce siempre lo técnico al resultado del cliente: no "SSG con hidratación parcial" sino "carga en menos de un segundo, incluso con señal mala en terreno".
- Los botones dicen qué pasa: "Escríbeme por WhatsApp", no "Contacto" ni "Enviar".
- Precios visibles, en UF. No se ocultan tras "cotiza con nosotros".

---

## 7. Alcance — v1.1

**Páginas. Solo estas:**
1. `/` — Home
2. `/sobre-mi`
3. `/404`

**Secciones de la home, en este orden (con su banda de color):**
1. Hero — cal + textura · promesa + medidor en vivo + CTA WhatsApp
2. El problema — cal + textura, regla gruesa arriba
3. Qué hago / Precios — cal + textura, hairline arriba · tabla comparativa única (fusionadas: no volver a separarlas ni duplicar precios)
4. Ejemplo — cal + textura, hairline arriba · captura + métricas + enlace al demo
5. Honestidad — **azul** · recién por mi cuenta + primeros 3 proyectos + remite al testimonio
6. Testimonio — cal + textura · Gonzalo Toro, `<figure>`/`<blockquote>`/`<figcaption>`
7. Dudas frecuentes — cal + textura, hairline arriba · marcadas con `FAQPage`
8. Cierre — **azul** · CTA WhatsApp

**Sobre mí:** portada con ficha técnica (`<dl>`) en cal, "Mi respaldo" en cal, "Cómo trabajo" en **azul**, honestidad en cal (sin contradecir el testimonio), cierre en **azul**.

**Fuera de alcance. No lo construyas ni lo propongas:**
blog, más páginas, auditoría automatizada, i18n, modo oscuro, newsletter, CMS, buscador, animaciones, formulario de contacto, calculadora de precios, sección de "tecnologías", foto personal (decidido: sin foto por ahora).

Si se te ocurre algo bueno, escríbelo en `IDEAS.md` y sigue. **El mayor riesgo de este proyecto sigue siendo que crezca el alcance:** hay 5-10 horas por semana y todavía cero clientes pagando. El sitio ya está bueno; el tiempo va a conseguir clientes (§13).

---

## 8. SEO y GEO — línea base, sin obsesión

Nadie busca "desarrollo web San Felipe". No optimizamos para tráfico frío. Solo lo barato y correcto:

- Un `<h1>` por página. Jerarquía real de encabezados.
- `<title>` y `meta description` únicos y escritos a mano.
- JSON-LD: `Person` + `ProfessionalService` (con `areaServed`) en el home, `FAQPage` en las dudas frecuentes. Validado por Lighthouse.
- Consistencia de entidad: mismo nombre, misma URL, misma descripción que en LinkedIn, GitHub y Google Business Profile. **Esto importa más que el schema** para que un LLM me cite. Pendiente (§13).
- `sitemap.xml`, `robots.txt`, `llms.txt`.
- OG image estática, generada una vez.
- HTML semántico y parseable sin JS. Un modelo que no puede leer la página no la puede citar.
- URLs en español, en minúscula, con guiones.
- Páginas que no deben indexarse (ej. agradecimientos) llevan `<meta name="robots" content="noindex">`.

---

## 9. Estructura del repo

```
src/
  pages/          index.astro, sobre-mi.astro, 404.astro
  components/     carpeta plana, sin anidar (Nav, Ejemplo, …)
  layouts/        Base.astro
  styles/         global.css (@theme: tokens, fuentes, escala; @font-face; .bg-textura-cal)
  assets/         imágenes procesadas por astro:assets
public/           robots.txt, llms.txt, favicon, og.png
CLAUDE.md         fuente de verdad
AGENTS.md         apunta acá + comandos de entorno
IDEAS.md          todo lo que queda fuera de alcance
```

Sin `utils/`, sin `lib/`, sin `helpers/` hasta que exista un problema real que los justifique.

---

## 10. Cómo trabajar conmigo

- **Un cambio a la vez.** No refactorices de paso. No "mejores" archivos que no te pedí tocar.
- **Antes de escribir código**, dime en 3 líneas qué vas a hacer y espera. Aplica siempre a cambios estructurales.
- **No instales dependencias sin preguntar.** Repetido a propósito.
- **No inventes contenido.** Si falta un precio, un dato o un texto, déjalo como `TODO:` y avísame. Nunca rellenes con lorem ipsum ni copy inventado.
- **No inventes números.** Contrastes, pesos y métricas se calculan o se miden. Si dijiste una cifra de memoria y luego la calculaste distinta, corrígeme explícitamente.
- **No agregues abstracciones "por si acaso".** Este sitio tiene 3 páginas.
- **Listas repetidas van como array + `map`** en el frontmatter, no markup copiado. Menos inconsistencias y un solo lugar que editar.
- **Prefiero código aburrido y explícito** por sobre código ingenioso.
- Si algo que te pido rompe una regla de este archivo, **dímelo en vez de obedecer**.
- Si una regla te parece equivocada, dilo. No es sagrado, pero se cambia acá, a propósito, no en silencio.
- **Cuando cambie algo estructural o un dato de §12, actualiza este archivo en el mismo cambio.** Un CLAUDE.md desactualizado hace que la próxima sesión "corrija" el sitio hacia atrás.

---

## 11. Definición de terminado

Una página está lista cuando, todo junto:

1. Cumple el presupuesto de §4, **medido** contra el deploy, no estimado.
2. Cero errores en consola. Cero warnings de Astro.
3. Se ve y funciona a 360px de ancho.
4. Navegable completa con teclado, con foco visible (incluidas las bandas azules).
5. Ninguna palabra de la lista prohibida.
6. Cada afirmación tiene un número medido detrás, o fue borrada.
7. Le pasé el sitio a alguien que no es desarrollador y entendió qué vendo y cuánto cuesta en menos de 40 segundos.

El punto 7 es el único que importa de verdad. Los otros seis son piso.

---

## 12. Datos de contenido aprobados — usar tal cual, no inventar

Decididos. No los cambies, no los redondees, no inventes lo que falte. Si algo no está acá, es `TODO:` y se pregunta.

### Catchline (h1 del home)
> Le hago a tu negocio un sitio que carga en menos de un segundo y te trae clientes por WhatsApp.

### Precios — rótulo obligatorio: "precio de lanzamiento, mis primeros 3 proyectos"

| Servicio | Precio |
|---|---|
| Una página | 3 UF |
| Sitio: Inicio + Sobre mí + Catálogo | 5 UF |
| Custom (desde 4 páginas) | 7 UF, más 2 UF por página extra |

- Precios en **UF**. Se puede mostrar el equivalente aproximado en pesos como referencia secundaria, rotulado "aprox." y notando que la UF varía a diario. **No hardcodear un valor de UF en pesos.**
- UF de referencia al construir: ~$40.845 (jul 2026). Solo para dimensionar textos.

### Planes de mantención mensual

**Soporte estándar — 1 UF/mes**
- Hosting, dominio y respaldos administrados
- Hasta 2 cambios menores al mes (textos, precios, fotos)
- Respuesta en 48 horas hábiles
- Sitio siempre actualizado y seguro

**Soporte prioritario — 3 UF/mes**
- Todo lo del plan estándar, sin tope de cambios menores
- Respuesta el mismo día hábil
- Reporte mensual: visitas, de dónde llegan, qué buscan
- Una mejora al mes (sección nueva, ajuste de textos, campaña)

**Prohibido escribir "24/7"** o cualquier promesa de disponibilidad nocturna o festiva. El compromiso es en horas y días hábiles. El reporte mensual es lo que sostiene el plan prioritario: sin él, la mantención se siente como cobrar por nada.

### Testimonio (permiso explícito concedido)

Texto exacto, no editar:

> Trabajar con Camilo Flores fue una experiencia excelente. Fue muy proactivo, dedicado y creativo en todo el proceso de desarrollo y perfeccionamiento del sitio web de GVE Sistemas. Siempre aportó ideas claras y soluciones efectivas, cumpliendo los plazos establecidos y superando las expectativas.

Atribución: **Gonzalo Toro · CEO, ITQ Internacional.**

El sitio de GVE Sistemas ya no existe (la empresa cerró). **No se enlaza, no se muestra captura, y no se insinúa que siga en línea.** Tampoco se explica en el sitio: si preguntan, se dice la verdad.

### Empresa donde trabajo
Referir siempre como "una empresa de tecnología chilena con presencia internacional". Sin nombre, sin logo, sin cargo específico, hasta nuevo aviso.

### Sitio de demostración (sección "Ejemplo")

- Proyecto: **Encuentro PyME Aconcagua**, seminario **ficticio** para dueños de negocios del valle.
- URL: `TODO:` confirmar (hoy en `*.workers.dev`; pendiente subdominio propio, que se ve mucho más profesional).
- Métricas mostradas: `TODO:` medir con PageSpeed contra el demo desplegado y usar los números reales. No publicar cifras sin medir.
- Rótulo obligatorio: se dice que es un ejemplo/demostración y que el evento es inventado. Frase aprobada: *"El evento es inventado; el trabajo, no."*
- El enlace abre en pestaña nueva, con aviso `sr-only`.
- Captura: AVIF < 50 KB, bajo el pliegue, `loading="lazy"`, tamaño declarado.

### WhatsApp
Número y mensaje pre-cargado tal como están hoy en el código. Los botones dicen "Escríbeme por WhatsApp".

---

## 13. Qué falta — y no es código

El sitio está terminado. El cuello de botella es comercial. En orden:

1. **Punto 7 de §11** — mostrarle el sitio a alguien que no sea desarrollador y confirmar que entiende qué vendo y cuánto cuesta en menos de 40 segundos. Es el único chequeo que de verdad importa.
2. **Consistencia de entidad** — mismo nombre, URL y descripción en LinkedIn, GitHub y Google Business Profile. Es lo que más mueve la aguja para que un modelo me cite, más que cualquier schema.
3. **Los primeros 3 clientes.** El plan: elegir negocios concretos del valle con sitios lentos, correrles PageSpeed a mano, grabar un video corto mostrando qué está roto y cuánto les cuesta, y mandárselo. Cada auditoría sirve aunque no compren.
4. **Subdominio propio para el demo**, antes de que lo vea mucha gente.

Regla de reparto de tiempo: **60% conseguir clientes, 40% el sitio.** No al revés. Si una sesión empieza con ganas de tocar código sin que haya una conversación de venta pendiente, esa es justamente la señal de alarma.