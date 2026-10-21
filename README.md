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
| `seccion` | `oportunidad` (tarjeta naranja compacta arriba de todo, para ofertas de último momento), `destacado` (uno solo), `principal` (tarjetas grandes), `banda` (franja verde de ancho completo; si hay dos seguidas, la segunda va en verde más oscuro y con las fotos del otro lado), `premium` (vitrina oscura de ancho completo, con filete dorado) o `catalogo` (grilla "Más modelos"). |
| `nombre` | Nombre del producto. |
| `precio` | Solo el número, sin puntos ni signo: `39900`. |
| `etiqueta` | Texto corto en naranja, por ejemplo `¡Bombilla de regalo!`. |
| `aviso` | Opcional. Pastilla naranja de urgencia, por ejemplo `¡Últimas unidades!`. Vacío = sin pastilla. |
| `blonda` | Texto del medallón que va sobre la foto, por ejemplo `Oferta especial`. Vacío = sin medallón. |
| `blonda_estilo` | Opcional. Color: `celeste`, `verde` o `naranja` (vacío = marrón kraft). Agregá `izquierda` para ponerla del otro lado de la foto y `mover` para que se balancee todo el tiempo. Ejemplo: `celeste izquierda mover`. |
| `frase` | Una frase opcional. |
| `caracteristicas` | Separadas por una barra vertical: `Algarrobo \| Virola de acero`. |
| `variantes` | Colores, separados por barra vertical: `Blanco \| Rosa`. La primera variante usa la primera foto, la segunda la segunda, y así. |
| `fotos` | Nombres de archivo dentro de `img/`, separados por barra vertical. La primera es la principal. |
| `agotado` | `si` o `no`. Con `si` el producto pasa a la sección "Agotados" al final, con la foto apagada y sin botón de pedido. |

Para mostrar un agotado como logro (foto a color, sello "Agotado" y un mensaje), poné `exito` en `seccion` y `si` en `agotado`. El mensaje va en `etiqueta` y el sello en `blonda`.

El orden de las filas es el orden en la página. Si la cantidad de productos `principal` es impar, el último se muestra en la banda verde de ancho completo.

**Oportunidad de último momento:** un producto con `oportunidad` en `seccion` aparece en una tarjeta naranja compacta arriba de todo, antes del destacado (usa solo la primera foto). Ahí la `etiqueta` se resalta en una pastilla y el texto de `blonda` va debajo, sin medallón sobre la foto. Cuando termine la oferta, poné `no` en `activo` (o borrá ese producto de la lista) y la banda desaparece. Para compartirla, usá el enlace de la tienda; si querés que lleve directo a la oferta, agregale el ancla, por ejemplo `tiendasiempremate.com.ar/#especial-mama`.

**Línea premium:** cualquier producto con `premium` en `seccion` se muestra en la vitrina oscura, debajo de la banda verde. Con dos fotos se ven las dos a la vez; con una, o con tres o más, usa la galería normal.

**Compartir:** cada producto tiene un botón que comparte su enlace, por ejemplo `tiendasiempremate.com.ar/p/torpedo/`. Ese enlace es una página chica (carpeta `p/`) con la foto del producto como miniatura para WhatsApp, que lleva a la tienda justo en ese producto. El nombre de la carpeta sale del nombre del producto. Si agregás un producto nuevo o le cambiás el nombre o la foto principal, hay que crear o actualizar su página en `p/`; mientras tanto el enlace igual funciona (lo resuelve `404.html`), pero se comparte sin la foto. Para ocultar el botón, poné `compartir: false` en el bloque `CONFIG` de `index.html`.

**Para cambiar el destacado de temporada:** poné `destacado` en el producto nuevo y pasá el anterior a `principal`, `catalogo` o `activo: no`.

**Fotos nuevas:** subilas a `img/` en formato vertical 4:5 (como las de Instagram), idealmente JPG de 960 x 1200 px, con nombres sin espacios ni acentos.

### Opción A: editar desde Google Sheets (recomendada)

1. En Google Sheets: Archivo > Importar > Subir, y elegí `productos.csv`.
2. Archivo > Compartir > Publicar en la web. Elegí la hoja y el formato "Valores separados por comas (.csv)". Publicar y copiar el enlace.
3. En `index.html`, pegá ese enlace en `planilla: ""`.

Desde ese momento los cambios de la planilla se ven en la página sin tocar el código. Google puede tardar unos minutos en reflejarlos. No cambies los nombres de las columnas.

### Opción B: editar en el código

Sin planilla, la página usa la lista `PRODUCTOS` que está en `index.html`, con los mismos campos.

## Grabados personalizados

La sección se arma con el bloque `grabados` dentro de `CONFIG` en `index.html`: título, texto, la lista de fotos (en `img/`) y el mensaje que abre el botón "Consultar". Las fotos se muestran de a pares y la última casilla es la tarjeta de consulta. Para compartir la sección con su propia miniatura: `tiendasiempremate.com.ar/p/grabados/`.
