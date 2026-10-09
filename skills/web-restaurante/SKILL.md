---
name: web-restaurante
description: Arma la carta digital o la página web de un restaurante, panadería o negocio de comida en un solo HTML bonito, encadenando en orden varias skills de diseño (ui-ux-pro-max, taste-skill, soft-skill, emil-design-eng, find-animation-opportunities, animate, review-animations e impeccable). Úsala cuando pidan "hazme la carta digital", "arma la página web del negocio", "que la carta quede bonita" o "mejora el diseño de la carta/web".
---

# Web de restaurante — el orquestador

Encadenas ocho skills de diseño en orden. A cada una le das **un solo trabajo**: el que las otras no hacen.
No las invocas con la herramienta Skill: **lees su archivo** (`${CLAUDE_PLUGIN_ROOT}/skills/<nombre>/SKILL.md` y los
archivos que ese indique) y aplicas solo la parte que te toca en cada paso. Así ninguna se queda cargada
entera ni toma el control.

Argumentos opcionales: `sin-soft` (salta el paso 3) · `sin-python` (salta el script del paso 1).

## Lo que manda sobre todas (en este orden)

1. **La marca del negocio.** Si existen `marca/identidad.md` o `marca/DESIGN.md`, sus colores, letras y
   tono ganan sobre cualquier skill.
2. **Las reglas fijas de abajo.**
3. **En movimiento manda Emil** (pasos 4 y 5). taste-skill y soft-skill piden movimiento constante:
   eso se ignora.
4. **En estética, taste-skill y soft-skill.**

## Reglas fijas

- **Un solo archivo HTML** con el CSS y el JavaScript adentro. Lo único externo permitido: Google Fonts.
  Nada de React, Next, Tailwind, npm ni librerías. Si una skill pide eso, se traduce a CSS y JS simples.
- **Celular primero.** Se diseña para 360 px de ancho; la carta se lee con una mano, en la calle.
- **Precios, nombres y descripciones salen solo de `carta/carta.md`.** No se inventa un ingrediente, una
  descripción, un plato ni un precio. Si el producto no tiene descripción, va sin descripción.
- **Si algo de la carta es ambiguo** (una nota, un "¿?", un precio dudoso), se pregunta antes de armar.
- **Datos del negocio:** si no están horario, dirección y WhatsApp, se le piden al dueño antes de armar.
  Si no los tiene a mano, la carta sale sin ellos (nunca inventados) y se avisa en el informe.
- **Letras solo de Google Fonts, y las escoge el paso 3** (ver ahí). Si una skill propone una letra que
  no está en Google Fonts (Satoshi, Cabinet Grotesk, Clash Display, Geist…), se cambia por una que sí.
- **No se inventan fotos.** Solo se usan las del dueño (ver "Las fotos de los productos").
- **Para instalar cualquier programa, primero se pide permiso**: qué es, para qué y de dónde sale.

## Las fotos de los productos

La carta lleva fotos, pero el dueño las va sacando de a poco (en un día o durante la semana), con
su celular o un fotógrafo. Por eso la carta se diseña **lista para recibirlas**, tenga cero fotos o todas.

- **Dónde están:** en `productos/`. Cada foto se llama como el producto en `carta.md`, en minúsculas y
  con guiones (`huevos-en-cazuelita-de-tomate.webp`). Si una foto no calza con ningún producto, o un
  nombre se presta a dudas, se pregunta: nunca se adivina de quién es una foto.
- **Nombres repetidos:** si dos productos se llaman igual (ej. "Chocolate" pan y "Chocolate" bebida), una
  foto con ese nombre no se pone sin preguntar de cuál es. Pídele al dueño que la renombre
  (`chocolate-pan.webp`, `chocolate-bebida.webp`).
- **Producto con foto:** la foto va arriba de su renglón, en 4:3 recortada al centro, con bordes
  redondeados y `loading="lazy"`. El texto alternativo es el nombre del producto, nada más.
- **Producto sin foto:** queda como renglón normal. **Nunca** un recuadro vacío, un ícono o un "foto
  próximamente". La carta tiene que verse terminada con cero fotos.
- **Peso:** en el celular cada foto debe pesar menos de 300 KB y medir unos 900 px de ancho. Si una pesa
  más, se pide permiso para comprimirla (por ejemplo, instalar Pillow con `pip install pillow`) y se
  guarda en `.webp`. Si no hay cómo, se usa igual y se avisa en el informe.

**Cuando el dueño trae fotos nuevas** ("ya tengo las fotos, ponlas en la carta"): **no se rediseña
nada.** Se corre solo esta sección: emparejar fotos con productos, comprimir si hace falta, insertarlas
y mostrar la lista de qué producto quedó con foto y cuál sigue sin foto.

## Los pasos

### 1 · Sistema de diseño → ui-ux-pro-max
Trabajo: escoger paleta, par de letras y estilo **según el tipo de negocio**.
- Si hay Python, corre `python ${CLAUDE_PLUGIN_ROOT}/skills/ui-ux-pro-max/scripts/search.py "<tipo de negocio> <estilo> <palabras clave>" --design-system -p "<nombre>"`
  (usa `python3` si `python` no existe).
- Si hay `marca/DESIGN.md`: manda la marca. Del resultado tomas solo lo que la marca no define.
- Sin Python (o `sin-python`): sáltalo y avísalo en el informe.
- **Su paleta no sale tal cual:** mide el contraste de cada color de texto (sus grises suaves suelen
  quedar por debajo de 4,5:1) y baja la saturación de sus fondos crema/amarillos de plantilla.
- **Su letra es solo una sugerencia:** la decide el paso 3. Su "estilo" para startups o juegos se ignora.

### 2 · Que no parezca hecho por IA → taste-skill
Trabajo: composición y quitar los "tics de IA". Lee sus secciones 3, 4, 7 y 8.
Ignora la sección 2 (stack React/Next/Tailwind) y el dial de movimiento.

### 3 · Acabado caro → soft-skill (se salta con `sin-soft`)
Trabajo: jerarquía de letras, espacios, sombras y bordes. Escoge el arquetipo que pegue con comida
(cálido, editorial). Los fondos oscuros tipo tecnología solo si la marca lo pide. Lo que repita a
taste-skill, no lo vuelvas a aplicar.
- **Letras (este paso decide):** un par de Google Fonts, una para títulos y otra para nombres y precios.
  La lista de letras "demasiado vistas" de `${CLAUDE_PLUGIN_ROOT}/skills/impeccable/reference/brand.md` es un aviso, no una
  prohibición: Fraunces está ahí y fue la que mejor quedó en las pruebas (títulos con remates suaves que
  recuerdan al pan). Lo que sí se evita: Inter o letras de tecnología para una carta de comida, y letras
  a mano (Amatic, Pacifico) para leer precios. Si la marca ya tiene letra, manda la marca.
- **Espacio entre secciones:** de 56 a 76 px en el celular (soft pide 96+, en una carta la alarga de más).
- **Título principal:** grande pero sin gritar, de 48 a 56 px a 360 de ancho.

### 3b · La barra de secciones (siempre)
Va **abajo, flotando al alcance del pulgar**: la carta se usa con una mano. Botones de ≥ 44 px de alto y
con la etiqueta corta para que quepan todas a 360 px ("Pan" aunque la sección se llame "Pan para
llevar"). Marca la sección donde va leyendo. En computador puede pasar a una columna al lado.

### 4 · Pulido de detalles → emil-design-eng
Trabajo: cómo se siente al tocar: botones con `:active`, hover solo en dispositivos con mouse, estados,
nada aparece desde `scale(0)`, transiciones de propiedades exactas.

### 5 · Movimiento → find-animation-opportunities → animate → review-animations
1. Lee `find-animation-opportunities` y saca la tabla de qué animar y qué **no**.
2. Lee `animate` (y su `RECIPES.md`) e implementa solo lo aprobado.
3. Lee `review-animations` y su `STANDARDS.md`, revisa lo hecho y corrige todo hallazgo HIGH.
Siempre con `prefers-reduced-motion`.

### 6 · Revisión final → impeccable
Trabajo: contraste y accesibilidad. **No corras sus scripts** (piden Node). Lee
`${CLAUDE_PLUGIN_ROOT}/skills/impeccable/reference/audit.md` y `${CLAUDE_PLUGIN_ROOT}/skills/impeccable/reference/color-and-contrast.md` y revisa contra eso:
texto ≥ 4,5:1, botones de ≥ 44 px, nada se rompe a 360 px.

## El informe al terminar (corto, en español, sin jerga)

1. **Qué hizo cada paso**: una línea por skill. Si un paso no aportó nada, dilo.
2. **Lo que no se pudo** (ej. sin Python).
3. **Precios verificados**: tabla producto · precio en `carta.md` · precio en el HTML. Léelos del HTML
   ya guardado, no de memoria.
4. **Fotos:** qué productos quedaron con foto y cuáles siguen sin foto (para que el dueño sepa cuáles
   le faltan por sacar).
5. Dónde quedó el archivo.
