# Siempre Mate: página de pedidos

Página de una sola pantalla con los mates, sus fotos y un botón que abre WhatsApp con el pedido ya escrito.

## Qué hay en esta carpeta

- `index.html`: la página completa (diseño, textos y lista de productos).
- `img/`: el logo y las fotos de producto.
- `productos.csv`: la misma lista de productos, lista para importar a Google Sheets.

## 1. Cargar el número de WhatsApp

Abrí `index.html`, buscá `whatsapp: ""` (está al principio del bloque `CONFIG`) y poné el número entre las comillas, solo dígitos:

    whatsapp: "549XXXXXXXXXX",

El formato es 549 + código de área sin el 0 + número sin el 15. Mientras esté vacío, los botones abren WhatsApp pero sin destinatario.

## 2. Publicar en GitHub Pages

1. Creá un repositorio público y subí **el contenido** de esta carpeta (que `index.html` quede en la raíz, no dentro de otra carpeta).
2. En el repositorio: Settings > Pages > Source: "Deploy from a branch", rama `main`, carpeta `/ (root)`.
3. En un par de minutos la página queda en `https://TU-USUARIO.github.io/NOMBRE-DEL-REPO/`.

## 3. Cambiar productos, precios y el destacado

Cada producto tiene estos datos:

| Columna | Qué va |
|---|---|
| `activo` | `si` o `no`. Con `no` el producto se oculta sin borrarlo. |
| `seccion` | `destacado` (uno solo, va arriba de todo), `principal` (tarjetas grandes) o `catalogo` (grilla "Más modelos"). |
| `nombre` | Nombre del producto. |
| `precio` | Solo el número, sin puntos ni signo: `39900`. |
| `etiqueta` | Texto corto en naranja, por ejemplo `¡Bombilla de regalo!`. |
| `blonda` | Texto del medallón que va sobre la foto, por ejemplo `Oferta especial`. Vacío = sin medallón. |
| `blonda_estilo` | Opcional. Color: `celeste`, `verde` o `naranja` (vacío = marrón kraft). Agregá `izquierda` para ponerla del otro lado de la foto. Ejemplo: `celeste izquierda`. |
| `frase` | Una frase opcional. |
| `caracteristicas` | Separadas por una barra vertical: `Algarrobo \| Virola de acero`. |
| `variantes` | Colores, separados por barra vertical: `Blanco \| Rosa`. La primera variante usa la primera foto, la segunda la segunda, y así. |
| `fotos` | Nombres de archivo dentro de `img/`, separados por barra vertical. La primera es la principal. |

El orden de las filas es el orden en la página. Si la cantidad de productos `principal` es impar, el último se muestra en la banda verde de ancho completo.

**Para cambiar el destacado de temporada:** poné `destacado` en el producto nuevo y pasá el anterior a `principal`, `catalogo` o `activo: no`.

**Fotos nuevas:** subilas a `img/` en formato vertical 4:5 (como las de Instagram), idealmente JPG de 960 x 1200 px, con nombres sin espacios ni acentos.

### Opción A: editar desde Google Sheets (recomendada)

1. En Google Sheets: Archivo > Importar > Subir, y elegí `productos.csv`.
2. Archivo > Compartir > Publicar en la web. Elegí la hoja y el formato "Valores separados por comas (.csv)". Publicar y copiar el enlace.
3. En `index.html`, pegá ese enlace en `planilla: ""`.

Desde ese momento los cambios de la planilla se ven en la página sin tocar el código. Google puede tardar unos minutos en reflejarlos. No cambies los nombres de las columnas.

### Opción B: editar en el código

Sin planilla, la página usa la lista `PRODUCTOS` que está en `index.html`, con los mismos campos.
