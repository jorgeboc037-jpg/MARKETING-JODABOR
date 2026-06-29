# CLAUDE.md

Guía para Claude Code en este repo. Este repo no tiene código de producto: es la caja de herramientas de marketing/prospecting para Jodabor (negocio de páginas web, ver hermano `jodabor-web`).

## Qué hay aquí

Skills de marketing instaladas en `.claude/skills/` desde [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) (MIT). Incluye `cold-email`, `prospecting`, `copywriting`, `seo`, `cro`, `ads`, `emails`, `social`, etc. Se invocan automático por contexto o con `/nombre-skill`.

## En qué estamos usando esto: prospecting por WhatsApp

Jorge (dueño de Jodabor) encuentra leads navegando Facebook (páginas de negocios guatemaltecos: ventas de propiedades, hoteles, academias, tiendas) y le pide a Claude que redacte el primer mensaje de WhatsApp en frío, aplicando los principios del skill `cold-email` adaptados a un mensaje corto de WhatsApp en vez de un email.

### Proceso por lead

1. **Jorge manda screenshot del Facebook del lead** (seguidores, publicaciones, bio, tipo de inventario que manejan).
2. **Encontrar el ángulo específico**, no genérico. No es "no tenés sitio web", es la limitación concreta de depender solo del feed de Facebook para ese negocio en particular: no se puede filtrar por propiedad/chalet/cuarto, no hay catálogo con fotos y precios por unidad, no se puede reservar directo, etc.
3. **Elegir el tier de Jodabor que calza** (ver `jodabor-web/src/sections/Precios.jsx` para specs exactas):
   - **Vitrina (Q3,250)** — presencia básica, catálogo estático. Para leads simples (un solo lugar/producto, ej. un hotel con cuartos fijos).
   - **Negocio (Q7,000)** — catálogo dinámico + panel admin para que ellos mismos suban/actualicen cada unidad (propiedad, chalet, producto). Para leads con inventario variable que cambia seguido.
   - **Pro (Q10,500)** — agrega cotizaciones B2B, ideal para distribuidoras/proveedores, no aplica a la mayoría de estos leads.
4. **Redactar el mensaje** (estructura tipo Observación → Problema → Propuesta → Ask, comprimida a 3-4 líneas de WhatsApp):
   - Abre con "Hola, soy Jorge de Jodabor, hago páginas web para negocios" y sigue directo con la observación específica (seguidores + qué manejan), así queda claro desde el inicio qué se está ofreciendo.
   - Conecta la observación al problema real que tiene esa limitación.
   - Propone el tipo de sitio nombrando explícitamente "página web" (no quedarse en "catálogo propio" o "algo propio" de forma ambigua), sin necesariamente mencionar precio si el lead amerita el tier más caro: subestimar con un precio bajo "ancla" mal vendido le hace flaco favor al cierre.
   - Cierra con un CTA de baja friction: "¿Te interesa ver un ejemplo?" / "¿Te paso un ejemplo rápido?" — nunca pedir llamada en el primer mensaje.
   - Evitar frases que suenen a juicio sobre cómo se ve el negocio hoy (ej. "se vería más profesional"): puede leerse como insulto. Enfocar el beneficio en la experiencia del cliente final del lead, no en una crítica a su imagen actual.
5. **El precio se menciona en el mensaje solo si el tier es Vitrina** (oferta simple, precio bajo no ahuyenta). Si el lead necesita Negocio o Pro, el precio se reserva para cuando contesten interesados, así no se subvende el trabajo real.

### Ejemplos ya redactados

- **Casas de Playa en Monterrico** (16k seguidores, varias propiedades) → tier Negocio, sin precio en el primer mensaje.
- **Hostelería el Diamante** (2k seguidores, varios chalets privados) → tier Vitrina, con precio "Desde Q3,250" incluido.
- **Casas y chalet Monterrico** (4.8k seguidores, 94% recomendado, varias casas + chalet, solo Messenger) → tier Negocio, sin precio en el primer mensaje. **Contestaron** (única respuesta real hasta ahora): dijeron que pasarían la propuesta a alguien del equipo, preguntaron "¿Será página web?", Jorge confirmó con detalle + precio Q7,000 + link de ejemplo (detalleskairos.vercel.app). Luego contestaron: "Revisaremos esta propuesta y la enviaré a mis superiores" → está escalado internamente, en espera de respuesta. No se fuerza nada más por ahora, solo seguimiento cordial si preguntan algo.
- **Casa La Perla GT Monterrico** (13k seguidores, 782 publicaciones, agente de bienes raíces, varias casas) → tier Negocio, sin precio. Mismo nicho (Monterrico, casas de playa) que los dos leads anteriores: ya son 3 de esta categoría.
- **Casa vacacional Alma Del Mar** (Taxisco/Madre Vieja, una sola propiedad, precio $$$, sin contador de seguidores visible) → tier Vitrina, con precio Q3,250 incluido. Ángulo distinto a los anteriores: no es "catálogo disperso", es que cobran premium ($$$) pero no tienen presencia propia que respalde ese nivel.
- **Villas Vista Mar** (Monterrico, 692 seguidores, sin calificación, solo 1 opinión, confirmado: es una sola casa) → tier Vitrina, con precio Q3,250. Ángulo: página chica y nueva compitiendo en un nicho donde ya hay competidores con miles de seguidores, necesita generar confianza desde el primer vistazo.
- **Blue Bay Monterrico** (3.4k seguidores, 116 publicaciones, "alquiler de casas de vacaciones" en plural, solo 2 opiniones, contestan en algunas horas) → tier Negocio, sin precio. Ya son 4 leads del mismo nicho (Monterrico, casas de playa).
- **Chalet Los Arenales** (Hawaii Monterrico, anuncio pagado de Instagram, una sola propiedad) → tier Vitrina, con precio. Ángulo: ya pagan por el anuncio pero el funnel se rompe en el mismo post (gente pregunta precio/disponibilidad en comentarios en vez de reservar directo). 5to lead de Monterrico/casas de playa.
- **Print Factory** (Instagram, 108 seguidores, DTF textil/stickers/placas) → tier Negocio, sin precio. Ángulo fuerte: el botón de WhatsApp del perfil tira "Enlace incorrecto", problema activo y urgente, no solo "mejorarías con web".
- **BYK Publicidad** (Instagram, 2,078 seguidores, rotulación comercial e industrial, precios por volumen) → tier propuesto Pro (cotizaciones B2B) o Negocio si Jorge prefiere bajarlo, pendiente de confirmar con Jorge cuál usar. Nicho nuevo probado: imprenta/publicidad gráfica.
- **Foto Roma** (Facebook, 2.4k seguidores, fotos para título y carnets, local físico en zona 10, solo 2 opiniones) → tier Vitrina, con precio. Ángulo (corregido en la sesión: Jorge encontró la página vía Google, así que sí rankea): el clic cae directo a un perfil de Facebook con anuncios y sin precios claros, no falta de visibilidad en buscadores.
- **Encuadre Films GT** (Instagram, 2,416 seguidores, 320 publicaciones, foto/video de bodas y eventos sociales, "Guatemala & Centro America") → tier Negocio, sin precio. Ángulo: portafolio sin organizar en el feed, pesa más con clientela internacional comparando fotógrafos para boda destino.
- **Weddings & Princess** (anuncio pagado de Instagram, paquetes de foto/video para bodas y XV años "Desde Q2,495") → tier Vitrina, con precio (ya publican el suyo). Mismo patrón de funnel roto que Chalet Los Arenales.
- **Edgar Solar** (Instagram, @edgarsolar_, fotógrafo individual, 2,494 seguidores, weddings and events photography) → tier Vitrina, con precio. Ángulo limpio: su propia bio dice literal "DM for booking", evidencia directa sin inferir nada.
- **Innova Empresarial** (Facebook, 127 publicaciones, 87 seguidores, PBX, botón "Cotiza", productos promocionales: redes deportivas, camisetas con marca, tarjetas) → tier propuesto Pro (cotizaciones B2B), igual que BYK queda abierto a bajarlo a Negocio. Ángulo: dicen literal "Solicita nuestro catálogo!", no lo muestran de una vez. 3er lead de imprenta/publicidad gráfica.
- **Le Beau Guatemala** (Instagram, 13.3k seguidores, 1,064 publicaciones, 1,377 siguiendo, medicina estética/anti-aging + salón de uñas y cabello, teléfono y WhatsApp visibles en bio, posts de tratamientos tipo NAD+ y promos de temporada) → tier Negocio, sin precio. Ángulo distinto a los leads anteriores: NO es falta de alcance (13.3k seguidores, contenido activo), es que con tanto catálogo de tratamientos disperso en cientos de posts/highlights, cualquier precio o cita requiere escribir o llamar uno por uno. Nicho nuevo: medicina estética/spa.

**Nota de patrón (Monterrico):** 5 leads del mismo nicho (casas de playa). Considerar armar un trigger-template reusable para ese ángulo específico en vez de redactar cada uno desde cero (decisión pendiente, Jorge prefiere seguir uno por uno por ahora para no aumentar el margen de error).

**Nota de patrón (fotografía/eventos):** 4 leads el mismo día (Foto Roma, Encuadre Films, Weddings & Princess, Edgar Solar) — nicho nuevo con tracción real, igual que pasó con Monterrico. Vigilar si sigue apareciendo para decidir si amerita su propio ángulo reusable.

**Nota de patrón (imprenta/publicidad gráfica):** ya son 3 leads (Print Factory, BYK Publicidad, Innova Empresarial) — tercer nicho con tracción real el mismo día que Monterrico y fotografía/eventos.

**Canal de contacto: WhatsApp vs DM de Instagram.** No es un cambio general de canal, depende del lead: si el negocio muestra botón o número de WhatsApp (la mayoría), seguir por WhatsApp porque es el canal ya validado (la única respuesta real vino por ahí). Si el lead solo ofrece "Enviar mensaje"/llamada y no muestra WhatsApp, o su bio pide explícitamente "DM for booking" (ej. Edgar Solar, Encuadre Films), mejor contactarlo por DM de Instagram en vez de forzar WhatsApp — coincide con el canal que ellos mismos señalan, aunque el DM de alguien que no te sigue puede caer en "Solicitudes" y perderse más fácil.

## Codex como segundo canal para el mismo proceso

Jorge también usa Codex (en terminal) para hacer lo mismo: mandar screenshot de un lead y recibir ángulo + tier + mensaje. Se le dio un prompt autocontenido (tiers, reglas de precio, estructura Observación → Problema → Propuesta → Ask, convenciones de copy, un ejemplo) ya que Codex no lee este `CLAUDE.md` automáticamente. Si se ajusta el proceso acá (tiers, reglas de precio, convenciones), hay que actualizar también ese prompt en Codex a mano.

## Para considerar a futuro: agentes de sales de msitarzewski/agency-agents

Repo externo (MIT) con 232 agentes tipo Claude Code. Revisados dos de la división de sales/specialized, no instalados todavía (decisión de Jorge: guardar en memoria, no actuar hasta que aplique). Son overkill para el volumen/canal actual (un canal, leads manuales), pero tienen piezas puntuales que sí van a servir:

- **`sales/sales-outbound-strategist.md`** — secuencias multi-touch (8-12 toques), tiering de cuentas, señales de compra. Útil si el volumen de leads escala más allá de prospección manual uno por uno.
- **`specialized/sales-outreach.md`** — cadencia de 7 toques/21 días, *playbook de objeciones* (explorar con preguntas, no rebatir), etapas de pipeline (Prospecting → Engaged → Discovery → Proposal → Negotiation → Closed), email de "breakup" como último toque.

**Disparadores para sugerirlo proactivamente:**
1. Cuando Jorge necesite escribir un **follow-up** porque un lead no contestó el primer mensaje → usar la lógica de "cada toque agrega algo nuevo" + breakup message, adaptado a WhatsApp.
2. Cuando un lead **conteste con una objeción** (precio, "déjame pensarlo", "no tengo tiempo") → usar el playbook de objeciones (preguntas curiosas, no defender el precio).
3. Si Jorge empieza a manejar **muchos leads a la vez** y pierde el tracking por solo capturas de pantalla → proponer las etapas de pipeline simples de `sales-outreach.md`.

## SEO: decisión y estado (2026-06-24)

Se usó el skill `ai-seo` para pedir un plan de 90 días para `jodabor-web`. Hallazgos técnicos del análisis:

- El sitio es un SPA de una sola página con navegación por hash (`#precios`, `#proyectos`, etc.), sin React Router activo pese a estar instalado. Hoy no existen URLs separadas indexables más allá de `/`. Cualquier plan de "páginas de servicio" requiere primero rutear de verdad + prerenderizado (ej. `vite-react-ssg` o `react-snap` post-build).
- Inconsistencia de precio: `jodabor-web/public/llms.txt` dice Vitrina = **Q3,000**, pero `Precios.jsx` (fuente real) dice **Q3,250**. Pendiente de corregir en `llms.txt` (importa para AI-SEO: agentes leen ese archivo literal para cotizar).

**Decisión (Jorge):** pausar el plan grande (rutear el sitio, prerender, escribir páginas de nicho como `/paginas-web-para-alquiler-de-casas-de-vacaciones`, `/paginas-web-para-tiendas`, etc.) hasta cerrar más clientes. Razón: el dominio tiene días, el outbound por WhatsApp ya es el canal validado con tracción real (1 lead escalado a superiores), y las páginas de nicho convencen más después de tener un caso real cerrado en ese nicho que antes.

**Sí se hace ahora** (barato, no compite con tiempo de prospección):
1. **Completar Google Business Profile** — checklist completo ya entregado a Jorge (categoría "Diseñador de sitios web", negocio de área de servicio cubriendo Guatemala, descripción de 750 caracteres, servicios con precio Vitrina/Negocio/Pro, FAQ seedeada, primer post, fotos). Estado: pendiente que Jorge lo pegue en el panel.
2. **Pedir reseña + backlink ("hecho por Jodabor" en footer) a Kairos y DanceLab** — son los dos clientes con sitio live (`detalleskairos.vercel.app`, `dancelabgt.vercel.app`). Pendiente: redactar los dos mensajes de WhatsApp cuando Jorge lo pida.

Todo lo demás (rutas, prerender, páginas de nicho) queda pausado hasta 2-3 clientes cerrados o más tiempo libre.

## Estrategia social IG/FB (2026-06-25)

Cuentas @jodaborweb (IG) y página de FB casi en cero (sin seguidores/posts reales). Plan completo y persistido en `docs/estrategia-social-ig-fb.md`; resumen vivo acá:

**Decisiones de Jorge:** talento on-camera sin decidir todavía (modelo vs Jorge vs mezcla) → arrancar con Jorge en cámara para validar barato, decidir modelo solo si valida. Capacidad real 3-5h/semana, sin equipo. Se permite presupuesto chico de ads (boost desde ~Q30) pero solo para amplificar lo que ya funcionó orgánicamente, nunca para sustituir validación.

**Pilares de contenido:** (1) "Tu negocio vive de Facebook y te cuesta ventas" 35% — agitar el problema, requiere talento; (2) "Así vende un negocio con web propia" (Kairos/DanceLab) 30% — screen record + voz en off, agnóstico a talento; (3) Tips rápidos de negocio digital 25% — carrusel estático o reel texto+voz; (4) Casos de éxito con testimonio 10% (sube cuando haya cierres reales). Los ángulos de nicho ya probados en outbound (Monterrico, fotografía/eventos, imprenta) no se replican igual en contenido social: el contenido público se queda en el dolor genérico transversal, no nombra nichos específicos sin un caso cerrado de ese nicho.

**Cadencia (3-5h/semana):** 1 reel + 1 post estático + 2-3 stories por semana. Publicar primero en IG, espejar el Reel en FB sin producir doble.

**Plan 30/60/90 días (metas honestas, cuenta en cero):** día 30 → 50-150 seguidores, ≥1 reel con >40% completion, 1 DM/comentario con intención real. Día 60 → 150-400 seguidores, identificar el pilar que más retiene, 2-3 DMs con intención. Día 90 → 400-800 seguidores, 1ra pieza boosteada, 1 lead atribuible a contenido social.

**Reglas de boost (~Q30):** solo si completion >40% Y hay comentario/share genuino (no de Jorge); nunca boostear con completion <20%; prioridad de boost a piezas del Pilar 2 (Kairos/DanceLab); máximo 1 boost activo por semana.

**Acceso a herramientas (2026-06-25):** Jorge ya dio acceso a integraciones de Canva y Gmail en esta sesión de Claude Code. Canva sirve para producir de verdad los carruseles/posts estáticos del Pilar 3 (ya no solo el guion en HTML, sino el diseño final). Gmail puede usarse si algún lead/cliente prefiere contacto por correo en vez de WhatsApp (poco común hasta ahora, pero queda disponible).

## Posicionamiento de marca: pain point y villano (2026-06-26)

Se separaron dos cosas que antes estaban mezcladas en el contenido:

- **Pain point (el argumento racional, ya usado en cada mensaje de outbound):** el negocio depende de que alguien escriba y de que el dueño conteste, para algo que debería poder verse y decidirse solo (catálogo disperso, precio a ciegas, todo pasa por una sola persona).
- **Villano (la pieza que faltaba en el contenido social, sobre todo Pilar 1):** el conformismo, no la postergación. No es que el dueño tenga la intención de arreglarlo "después", es que ya normalizó la fricción como el costo de tener negocio en redes: "así nos ha funcionado, así se hacen las cosas aquí." Se descartó imitar el molde de Nike (villano = falta de acción/decisión) porque para pymes guatemaltecas pega más fuerte la resignación que la procrastinación activa.

**Cómo se usa:** el pain point sigue siendo la base de cada mensaje de outbound (ya funciona así). El villano (conformismo) se mete en los hooks del Pilar 1 para generar urgencia real sin sonar a cliché motivacional, señalando que algo que se siente "normal" en el negocio en realidad es un hábito que nadie cuestionó. Ejemplos de hook con este ángulo: "Llevás años contestando lo mismo en los comentarios y le decís que 'así es como funciona'", "No es que tu negocio esté mal, es que te acostumbraste a que funcione a medias", "Si hace 2 años te preguntaban precio en comentarios y hoy también, no es normal, es que nadie lo cambió."

## Contenido orgánico: reels y posts

Guiones para IG/FB: reels (video) en `content/reels/`, piezas estáticas (carrusel) en `content/posts/`. Formato HTML con shot list (encuadre, cámara, acción, audio, overlay), caption, notas técnicas y nota de precio/pilar.

- **`content/reels/guion-reel-esto-te-esta-costando-ventas.html`** — primer reel, Pilar 1, ángulo Problema → Solución, 30 seg, talento: modelo (no Jorge). Hook con comentario real de "¿cuánto cuesta?", agita con venta perdida + catálogo disperso en Facebook, solución mostrada con screen record de Kairos/DanceLab, CTA con precio Vitrina (Q3,250) porque es contenido masivo de awareness, no outreach 1:1.
- **`content/reels/guion-reel-asi-sube-productos-sin-llamarme.html`** — segundo reel, Pilar 2, 25 seg, 100% screen record + voz en off, sin talento on-camera (se puede producir sin esperar la decisión de talento). Muestra el panel admin de Kairos: sube un producto y aparece en el catálogo público al instante. Sin precio, ángulo es la capacidad del panel (tier Negocio).
- **`content/posts/carrusel-3-senales-facebook.html`** — primer carrusel estático, Pilar 3, 5 slides, 100% Canva sin grabación. "3 señales de que tu Facebook ya no aguanta tu negocio" (preguntas de precio repetidas, catálogo regado en posts viejos, no se puede filtrar/reservar/cotizar). Pieza "comodín" cuando la semana anda corta de tiempo.

## Convenciones de copy (heredadas de jodabor-web)

- Voseo guatemalteco (`vos`, `tenés`, `querés`).
- Sin raya larga (—) a media frase.
- Quetzales en formato `Q3,250` (coma de miles).
- Mensajes de WhatsApp: cortos, sin jerga, sin sonar a plantilla.
