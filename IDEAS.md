# IDEAS.md

Todo lo que **no** entra al alcance actual vive acá. Esto no es un backlog para hacer pronto: es el lugar donde una buena idea deja de distraerme del objetivo real, que hoy es **conseguir los primeros 3 clientes que paguen**.

**Regla de entrada:** si una idea me tienta a agrandar el alcance, la escribo acá y sigo. Nada de esta lista se construye hasta tener **al menos un cliente pagando**. El sitio ya está publicado, rápido y con prueba social: no es lo que me falta.

**Antes de sacar algo de acá, pregúntate:** ¿esto me acerca a una conversación de venta, o solo me da algo entretenido que programar? Si es lo segundo, se queda.

---

## Listo (salió de esta lista)

- ~~Testimonio real~~ → publicado: Gonzalo Toro, CEO de ITQ Internacional (GVE Sistemas), con permiso explícito.
- ~~Algo que mostrar~~ → sitio de demostración "Encuentro PyME Aconcagua": landing de seminario ficticio, con formulario real (Worker + Resend), en repo y deploy propios. Enlazado desde la sección "Ejemplo" del home.

---

## Siguiente, cuando toque (orden sugerido)

1. **Subdominio propio para el demo** (ej. `encuentro.camiloflores.cl`). Barato, rápido, y una URL `*.workers.dev` se lee como prueba de programador, no como trabajo profesional. Esto sí conviene hacerlo pronto.
2. **Casos de estudio con números reales.** Antes/después de tiempo de carga, consultas por WhatsApp. Requiere: clientes con métricas y permiso de publicación. Es la prueba que de verdad convierte; el demo es un sustituto mientras tanto.
3. **Los otros dos demos** (consultora legal de 3 páginas, sitio custom de viña u hotel). Solo si el primero demuestra que abre puertas en conversaciones reales. Construir los tres antes de saberlo es refugiarse en el editor.
4. **Auditoría automatizada.** El visitante pega su URL → se corre PageSpeed → se le muestra su tiempo de carga y qué le está costando. **Primero hacerla a mano** con video corto para 5 negocios; automatizar solo cuando ya se sepa que convierte.
5. **Notas / blog.** Contenido de intención de compra: "cuánto cuesta una página web en Chile", "por qué mi sitio carga lento", "WordPress vs sitio hecho a mano". Motor de SEO y GEO. Requiere disciplina de publicación sostenida — no empezar sin poder mantenerlo.
6. **Página del caso de la empresa donde trabajo**, solo si llega permiso explícito para nombrarla.

---

## Ideas sueltas (sin evaluar)

- Google Business Profile + presencia local para el valle. Barato y probablemente de los que más rinden.
- `llms.txt` más elaborado, con preguntas y respuestas para citación por modelos.
- Testimonios en video de los primeros clientes.
- Foto personal en Sobre mí (hoy descartada; ayuda a la confianza, reconsiderar cuando haya una buena).
- Fade sutil de secciones al hacer scroll, respetando `prefers-reduced-motion`. Muy al final, si acaso.
- Contrato/propuesta tipo para los primeros clientes: ahorra tiempo y proyecta seriedad. **Esto es de las pocas que sí ayudan a vender.**

---

## Cementerio (descartadas, y por qué)

Guardar el porqué evita volver a discutirlas en seis meses.

- **Modo oscuro.** No aporta al objetivo. Doble mantención de tokens.
- **Soporte 24/7.** Promesa incumplible con trabajo full-time. Reemplazada por "respuesta el mismo día hábil", que suena igual de sólido y sí se puede cumplir.
- **Formulario de contacto en mi sitio.** El cliente objetivo no llena formularios. WhatsApp gana. (Distinto del demo, donde el formulario *es* la demostración.)
- **Fondo fijo con efecto de movimiento al hacer scroll.** Incompatible con el sistema de bandas opacas: los muros taparían el fondo. Además `background-attachment: fixed` da tirones justo en Android de gama media, que es toda mi audiencia.
- **Patrón de grilla de fondo** (el snippet de papel milimetrado). Es el fondo default de todo clon de SaaS; se lee como plantilla tech, no como señalética del valle. La profundidad la da la textura de cal.
- **Partir los demos desde plantillas de HTMLrev.** Contradice el argumento central ("cada sitio lo construyo a mano"), hereda JS y peso ajenos, tiene líos de licencia, y customizar por completo el código de otro es *más* trabajo que hacerlo de cero. Las plantillas sirven como **referencia visual**, nunca como base de código.
- **Fotos de personas reales para identidades ficticias** (relatores del demo). Atribuirle a una persona real un nombre y cargo inventados no se hace. Se resolvió con monogramas, que además pesan cero.
- **Precios más bajos (2/3/4 UF).** Un precio demasiado bajo no aumenta la conversión: la baja, porque señala baja calidad, y deja por debajo de los molinos de plantillas. Se subió a 3/5/7 UF con rótulo de lanzamiento.