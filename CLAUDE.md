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
   - Abre con la observación específica (seguidores + qué manejan), no con "Hola, soy Jorge de Jodabor" como protagonismo.
   - Conecta la observación al problema real que tiene esa limitación.
   - Propone el tipo de sitio (sin necesariamente mencionar precio si el lead amerita el tier más caro: subestimar con un precio bajo "ancla" mal vendido le hace flaco favor al cierre).
   - Cierra con un CTA de baja friction: "¿Te interesa ver un ejemplo?" / "¿Te paso un ejemplo rápido?" — nunca pedir llamada en el primer mensaje.
5. **El precio se menciona en el mensaje solo si el tier es Vitrina** (oferta simple, precio bajo no ahuyenta). Si el lead necesita Negocio o Pro, el precio se reserva para cuando contesten interesados, así no se subvende el trabajo real.

### Ejemplos ya redactados

- **Casas de Playa en Monterrico** (16k seguidores, varias propiedades) → tier Negocio, sin precio en el primer mensaje.
- **Hostelería el Diamante** (2k seguidores, varios chalets privados) → tier Vitrina, con precio "Desde Q3,250" incluido.
- **Casas y chalet Monterrico** (4.8k seguidores, 94% recomendado, varias casas + chalet, solo Messenger) → tier Negocio, sin precio en el primer mensaje.

## Para considerar a futuro: agentes de sales de msitarzewski/agency-agents

Repo externo (MIT) con 232 agentes tipo Claude Code. Revisados dos de la división de sales/specialized, no instalados todavía (decisión de Jorge: guardar en memoria, no actuar hasta que aplique). Son overkill para el volumen/canal actual (un canal, leads manuales), pero tienen piezas puntuales que sí van a servir:

- **`sales/sales-outbound-strategist.md`** — secuencias multi-touch (8-12 toques), tiering de cuentas, señales de compra. Útil si el volumen de leads escala más allá de prospección manual uno por uno.
- **`specialized/sales-outreach.md`** — cadencia de 7 toques/21 días, *playbook de objeciones* (explorar con preguntas, no rebatir), etapas de pipeline (Prospecting → Engaged → Discovery → Proposal → Negotiation → Closed), email de "breakup" como último toque.

**Disparadores para sugerirlo proactivamente:**
1. Cuando Jorge necesite escribir un **follow-up** porque un lead no contestó el primer mensaje → usar la lógica de "cada toque agrega algo nuevo" + breakup message, adaptado a WhatsApp.
2. Cuando un lead **conteste con una objeción** (precio, "déjame pensarlo", "no tengo tiempo") → usar el playbook de objeciones (preguntas curiosas, no defender el precio).
3. Si Jorge empieza a manejar **muchos leads a la vez** y pierde el tracking por solo capturas de pantalla → proponer las etapas de pipeline simples de `sales-outreach.md`.

## Convenciones de copy (heredadas de jodabor-web)

- Voseo guatemalteco (`vos`, `tenés`, `querés`).
- Sin raya larga (—) a media frase.
- Quetzales en formato `Q3,250` (coma de miles).
- Mensajes de WhatsApp: cortos, sin jerga, sin sonar a plantilla.
