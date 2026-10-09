# IA para restaurantes · carta digital con Claude Code

Plugin para [Claude Code](https://claude.com/claude-code) que arma la **carta digital o la página web de un
restaurante, panadería o negocio de comida**: un solo archivo HTML, bonito, rápido y pensado para leerse en
el celular. La skill `/web-restaurante` encadena 8 skills de diseño, cada una con un solo trabajo.

**Lo que garantiza:** los precios y nombres salen solo de tu carta (nunca se inventan), tus colores y letras
mandan, no inventa fotos y la carta se ve terminada aunque todavía no tengas fotos.

## Qué necesitas en tu carpeta

```
carta/carta.md        tus productos, precios y descripciones
marca/identidad.md    (opcional) cómo es tu negocio, colores, letras, tono
productos/            (opcional) fotos, con el nombre del producto: pizza-margarita.webp
```

## Instalarlo

En la app de Claude (pestaña **Code**): botón **+** junto al cuadro de texto → **Plugins** → **Add plugin**,
y pega `andresarcila600/ia-restaurantes`.

En la terminal:

```
claude plugin marketplace add andresarcila600/ia-restaurantes
claude plugin install ia-restaurantes@ia-university
```

## Usarlo

En la carpeta de tu negocio, escríbele a Claude:

```
/web-restaurante
```

Cuando tengas fotos nuevas: *"ya tengo fotos nuevas, ponlas en la carta"*.

## Qué trae

| Skill | Para qué | Autor · licencia |
|---|---|---|
| web-restaurante | Orquesta todo el proceso | Andrés Arcila |
| ui-ux-pro-max | Paleta y letras según el tipo de negocio | Next Level Builder · MIT |
| taste-skill, soft-skill | Que no parezca hecho por IA · acabado fino | Leonxlnx · MIT |
| emil-design-eng, find-animation-opportunities, animate, review-animations | Detalles al tocar y movimiento justo | Emil Kowalski · MIT |
| impeccable | Revisión final de contraste y accesibilidad | Paul Bakaus · Apache 2.0 |

Las licencias completas están en `licencias/`.

## Regla de seguridad

Antes de instalar cualquier skill o plugin (este incluido), pregúntale a Claude qué hace, quién lo hizo y de
dónde sale. Este paquete es casi todo instrucciones de texto. Trae dos grupos de scripts de sus autores
originales: los de Python de ui-ux-pro-max (busca paletas y letras; `/web-restaurante` los usa) y los de Node
de impeccable (`/web-restaurante` no los corre). No instala nada por su cuenta y pide permiso antes de
instalar cualquier programa.
