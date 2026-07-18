# CLAUDE.md

Instrucciones permanentes para este repositorio. Léelas completas antes de escribir código.

---

## 1. Qué es esto

Sitio web personal de Camilo, desarrollador web en San Felipe, Región de Valparaíso, Chile.

**Objetivo comercial único:** que un dueño de PyME del Valle de Aconcagua que ya habló conmigo (o que recibió una auditoría mía) entre al sitio, confíe, y me escriba por WhatsApp.

**El sitio no es un canal de captación.** Es el cierre. Nadie llega acá por Google. Llega porque le hablé antes. Su trabajo es convertir una conversación tibia en un mensaje.

**Audiencia real:** dueño o dueña de un negocio local — viña, clínica dental, ferretería, turismo, agro. 35-60 años. Entra desde un Android de gama media con datos móviles. No sabe qué es un framework. No le importa. Tiene 40 segundos.

**Audiencia que NO es:** otros desarrolladores, reclutadores, Hacker News.

### Estado honesto del proyecto
No hay casos con clientes todavía. Hay **un** antecedente: trabajo como desarrollador en una empresa de tecnología chilena con presencia internacional. Eso es **credencial**, no portafolio, y va en "Sobre mí", nunca presentado como caso de éxito propio. No se nombra la empresa hasta tener permiso explícito; tampoco se dan detalles que la identifiquen 1:1.

La postura del sitio es explícita: *estoy tomando mis primeros 3 proyectos a precio de lanzamiento*. No inventamos prueba social. No hay testimonios falsos, ni logos de "clientes", ni "+50 proyectos".

---

## 2. Regla de oro

> Ante cualquier decisión, pregunta: **¿esto ayuda al dueño de la viña a decidir, o me hace ver inteligente a mí?**

Si es lo segundo, no va.

Corolario: **la excelencia técnica de este sitio debe ser invisible.** Se percibe como velocidad y claridad, nunca se menciona. El sitio no habla de sí mismo.

---

## 3. Stack — fijo, no negociable

| Capa | Decisión |
|---|---|
| Framework | Astro 5, `output: 'static'` |
| Estilos | TailwindCSS 4 vía `@tailwindcss/vite` |
| Lenguaje | TypeScript, `strict: true` |
| Islas / UI framework | **Ninguno.** Sin React, Vue, Svelte, Solid |
| JS de cliente | Vanilla, inline, mínimo |
| Imágenes | `astro:assets` → AVIF con fallback WebP |
| Tipografías | Self-hosted vía `@fontsource-variable`, subset latino, `woff2` |
| Íconos | SVG inline pegado a mano. Sin librerías de íconos |
| Analítica | Cloudflare Web Analytics (sin cookies) |
| Hosting | Cloudflare Pages, deploy automático desde `main` |
| Dominio | `.cl` |
| Contacto | Link `wa.me` con `?text=` pre-cargado. Sin formularios |
| CMS | Ninguno |

### Prohibiciones de dependencias

**No instales nada sin preguntar primero.** Ni una. Si crees que hace falta un paquete, detente, explica qué problema resuelve, cuánto pesa, y propón la alternativa a mano. Yo decido.

Prohibido explícitamente: librerías de animación (GSAP, Framer Motion, AOS), carruseles, librerías de íconos, librerías de fechas, lodash, jQuery, cualquier UI kit, cualquier cosa que agregue JS al cliente.

`package.json` en v1 debería tener menos de 10 dependencias. Si tiene más, algo salió mal.

---

## 4. Presupuesto de rendimiento — límites duros

Estos números son requisitos, no aspiraciones. Un PR que los rompe no se mergea.

- **JS enviado al cliente: < 2 KB** (comprimido). El objetivo es 0. El único JS permitido en v1 es el medidor del hero.
- **Peso total de la home: < 120 KB** comprimido, incluyendo tipografías e imágenes.
- **LCP: < 1,0 s** en 4G simulado / móvil.
- **CLS: < 0,01.** Toda imagen lleva `width` y `height`. Toda tipografía se precarga.
- **INP: < 100 ms.**
- **Requests en la home: < 12.**
- Lighthouse 100/100/100/100 en móvil es el **piso**, no la meta. Que dé 100 no significa que esté bien.

Reglas derivadas:
- Sin banner de cookies. Nunca. Si algo exige uno, ese algo no entra.
- Sin fuentes de terceros. Sin Google Fonts por CDN.
- Sin embeds de terceros (YouTube, Maps, widgets). Si hace falta un mapa, es un link.
- Máximo **3 archivos de tipografía**.
- Todo el CSS crítico inline; Astro ya lo hace, no lo desarmes.

---

## 5. Dirección visual

**Concepto:** señalética comercial pintada del Valle de Aconcagua. Letrero de esmalte sobre pared encalada. Sobrio, alto contraste, plano, hecho para leerse desde lejos y bajo sol.

**Prohibido** (esto es el look genérico de sitio generado con IA, y usarlo refuta el argumento comercial completo del sitio):
- Fondo oscuro con gradiente violeta/azul
- Fondo crema (~#F4F1EA) con serif de alto contraste y acento terracota
- Cards con `blur`, `glow`, bordes luminosos, glassmorphism
- Inter, Poppins, Montserrat
- Modo oscuro (no se implementa en v1)
- Gradientes de cualquier tipo
- Animaciones al hacer scroll, parallax, scroll-jacking
- Blobs, mallas, patrones de puntos, ruido decorativo
- Emojis como íconos
- Marcadores numerados 01 / 02 / 03 salvo que el contenido sea realmente una secuencia

### Tokens

```css
--cal:      #EFF0EC;  /* fondo — encalado, gris-verdoso frío */
--tinta:    #171A17;  /* texto — casi negro con fondo verde */
--azul:     #0E3FA8;  /* acento único — esmalte de letrero */
--parra:    #4C6B3C;  /* verde parra — estados correctos, cifras buenas */
--rojo:     #C8322D;  /* solo para señalar el problema del cliente */
--borde:    #D5D8D0;  /* líneas hairline */
```

Un solo acento: `--azul`. `--rojo` aparece **únicamente** cuando se muestra el dolor (un sitio lento, una cifra mala). El color codifica verdad, no decora.

Sin sombras. Bordes `1px solid var(--borde)`. `border-radius: 2px` máximo — es un letrero pintado, no una app.

### Tipografía

- **Display:** `Archivo Expanded` (variable, eje de ancho) — titulares y cifras. Peso 700. Uso con moderación: titulares y números, nada más.
- **Cuerpo:** `Source Serif 4` — 400 y 600. Un serif proyecta seriedad ante este cliente y ningún portafolio de dev usa uno.
- Cifras (`0,38 s`, `5 UF`) van siempre en display. Son el protagonista.
- Escala tipográfica explícita, definida en `tailwind.config`. Nada de tamaños arbitrarios.
- **Coma decimal**, no punto. Es Chile.

### Elemento firma

El hero muestra **el tiempo de carga real de esta misma página**, medido en vivo:

```js
// única excepción al presupuesto de JS
const t = (performance.now() / 1000).toFixed(2).replace('.', ',');
document.getElementById('medidor').textContent = t;
```

Es la tesis del negocio demostrada, no afirmada. Todo lo demás en la página se queda callado alrededor de esto. **No agregues un segundo elemento llamativo.** La audacia se gasta una sola vez.

### Piso de calidad
Responsive hasta 360px de ancho. Foco de teclado visible. `prefers-reduced-motion` respetado. Contraste AA mínimo, AAA en cuerpo.

---

## 6. Voz y copy

Español de Chile. Trato de "tú", respetuoso, sin jerga, sin diminutivos, sin humor forzado.

**Palabras prohibidas en todo el sitio:**
apasionado, soluciones digitales, a medida, transformar ideas en realidad, full stack, stack, framework, landing, deploy, responsive, performance, optimizar, escalable, robusto, innovador, sinergia, potenciar, llevar tu negocio al siguiente nivel, Astro, Tailwind, JavaScript.

Los nombres de tecnologías **no aparecen en el home**. Al cliente no le importa. Puede haber una mención sobria en Sobre mí.

**Reglas de escritura:**
- Toda afirmación lleva un número, o se borra.
- Frases cortas. Verbos activos. Sentence case.
- Traduce siempre lo técnico al resultado del cliente: no "SSG con hidratación parcial" sino "carga en menos de un segundo, incluso con señal mala en terreno".
- Los botones dicen qué pasa: "Escríbeme por WhatsApp", no "Contacto" ni "Enviar".
- Precios visibles, en UF. No se ocultan tras "cotiza con nosotros".

---

## 7. Alcance de v1 — cerrado con candado

**Páginas. Solo estas:**
1. `/` — Home
2. `/sobre-mi`
3. `/404`

**Secciones de la home, en este orden:**
1. Hero — promesa + medidor en vivo + CTA WhatsApp
2. El problema — por qué su sitio actual (o su Instagram) le está costando plata
3. Qué hago — 3 servicios, con precio
4. Precios — tramos en UF + plan de mantención mensual
5. Honestidad — ENIAX como credencial + "mis primeros 3 proyectos a precio de lanzamiento"
6. Dudas frecuentes — objeciones reales, marcadas con `FAQPage`
7. Cierre — CTA WhatsApp

**Fuera de alcance en v1. No lo construyas, ni lo propongas:**
blog, casos de estudio, herramienta de auditoría automatizada, i18n, modo oscuro, newsletter, CMS, buscador, animaciones, formulario de contacto, calculadora de precios, sección de "tecnologías".

Si se te ocurre algo bueno, escríbelo en `IDEAS.md` y sigue. El mayor riesgo de este proyecto es que crezca el alcance: hay 5-10 horas por semana disponibles y ningún cliente todavía.

---

## 8. SEO y GEO — línea base, sin obsesión

Nadie busca "desarrollo web San Felipe". No optimizamos para tráfico frío en v1. Solo lo que es barato y correcto:

- Un `<h1>` por página. Jerarquía real de encabezados.
- `<title>` y `meta description` únicos y escritos a mano.
- JSON-LD: `Person` + `ProfessionalService` (con `areaServed`) en el home, `FAQPage` en las dudas frecuentes.
- Consistencia de entidad: mismo nombre, misma URL, misma descripción que en LinkedIn, GitHub y Google Business Profile. **Esto importa más que el schema** para que un LLM me cite.
- `sitemap.xml`, `robots.txt`, `llms.txt`.
- OG image estática, generada una vez.
- HTML semántico y parseable sin JS. Un modelo que no puede leer la página no la puede citar.
- URLs en español, en minúscula, con guiones.

---

## 9. Estructura del repo

```
src/
  pages/          index.astro, sobre-mi.astro, 404.astro
  components/     una carpeta plana, sin anidar
  layouts/        Base.astro
  styles/         global.css (tokens + @font-face)
  assets/
public/           robots.txt, llms.txt, favicon
CLAUDE.md
IDEAS.md          todo lo que queda fuera de alcance
```

Sin `utils/`, sin `lib/`, sin `helpers/` hasta que exista un problema real que los justifique.

---

## 10. Cómo trabajar conmigo

- **Un cambio a la vez.** No refactorices de paso. No "mejores" archivos que no te pedí tocar.
- **Antes de escribir código**, dime en 3 líneas qué vas a hacer y espera. Aplica siempre a cambios estructurales.
- **No instales dependencias sin preguntar.** Repetido a propósito.
- **No inventes contenido.** Si falta un precio, un dato o un texto, déjalo como `TODO:` y avísame. Nunca rellenes con lorem ipsum ni con copy inventado que después se me olvida borrar.
- **No agregues abstracciones "por si acaso".** Este sitio tiene 2 páginas.
- **Prefiero código aburrido y explícito** por sobre código ingenioso.
- Si algo que te pido rompe una regla de este archivo, **dímelo en vez de obedecer**.
- Si una regla de este archivo te parece equivocada, dilo. No es sagrado, pero se cambia acá, a propósito, no en silencio.

---

## 11. Definición de terminado

Una página está lista cuando, todo junto:

1. Cumple el presupuesto de rendimiento de la sección 4, **medido**, no estimado.
2. Cero errores en consola. Cero warnings de Astro.
3. Se ve y funciona a 360px de ancho.
4. Navegable completa con teclado, con foco visible.
5. Ninguna palabra de la lista prohibida.
6. Cada afirmación tiene un número detrás o fue borrada.
7. Le pasé el sitio a alguien que no es desarrollador y entendió qué vendo y cuánto cuesta en menos de 40 segundos.

El punto 7 es el único que importa de verdad. Los otros seis son piso.

---

## 12. Datos de contenido aprobados — usar tal cual, no inventar

Estos valores están decididos. No los cambies, no los redondees, no inventes lo que falte. Si algo no está acá, es `TODO:` y se pregunta.

### Catchline (h1 del home)
> Le hago a tu negocio un sitio que carga en menos de un segundo y te trae clientes por WhatsApp.

### Precios — rótulo obligatorio: "precio de lanzamiento, mis primeros 3 proyectos"

| Servicio | Precio |
|---|---|
| Una página | 3 UF |
| Sitio: Inicio + Sobre mí + Catálogo | 5 UF |
| Custom (desde 4 páginas) | 7 UF, más 2 UF por página extra |

- Los precios se muestran en **UF**. Se puede mostrar el equivalente aproximado en pesos como referencia secundaria, con la nota de que la UF varía a diario. **No hardcodear un valor de UF en pesos** que quede desactualizado: si se muestra pesos, redondear y rotular como "aprox.".
- UF de referencia al construir: ~$40.845 (jul 2026). Solo para dimensionar textos, no para fijarlo en el código.

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

**Prohibido escribir "24/7"** o cualquier promesa de disponibilidad nocturna/festiva. El compromiso es en horas y días hábiles. Ver pilar de honestidad (sección 6).

### ENIAX
Referir siempre como "una empresa de tecnología chilena con presencia internacional". Sin nombre, sin logo, sin cargo específico, hasta nuevo aviso.
