# La Cantina del Delfín — Carta web

Sitio estático (HTML/CSS/JS, sin build) que lee el menú **en vivo desde una planilla de Google**, listo para publicarse gratis en GitHub Pages.

## Cómo funciona

`index.html` no tiene los platos escritos adentro: al abrirse, descarga una planilla de Google Sheets publicada como CSV y arma la carta automáticamente (secciones, ítems, precios, notas). Así, para cambiar un precio o agregar un plato, el administrador **solo edita la planilla** — no toca código ni GitHub.

## Paso 1 — Crear la planilla

1. Andá a [sheets.google.com](https://sheets.google.com) y creá una hoja nueva.
2. Importá el archivo `menu.csv` que te dejé en esta carpeta (ya tiene cargado TODO el menú actual): **Archivo → Importar → Subir → Reemplazar hoja de cálculo**.
3. Vas a ver estas columnas — son las que la web entiende:

| Columna | Qué es |
|---|---|
| `orden_seccion` | Número que define el orden de las secciones (Entradas=1, Ensaladas=2, etc.) |
| `seccion` | Nombre de la sección/categoría (ej. "Entradas") |
| `subtitulo_seccion` | Texto opcional en itálica debajo del título (solo hace falta en la primera fila de la sección) |
| `grupo` | Solo se usa en "Vinos Finos", para agrupar por bodega |
| `orden_item` | Orden del plato dentro de su sección |
| `item` | Nombre del plato |
| `precio` | Precio. Si se deja vacío, la web muestra "Consultar" |
| `precio2` | Solo para platos con dos precios (ej. porción individual / para 2 en "Pescados a la Parrilla") |
| `nota` | Descripción/ingredientes opcional, debajo del nombre |

**Para editar el menú:** cambiar un precio es solo tocar el número en la celda. Para agregar un plato nuevo, agregar una fila con esos mismos datos. Para agregar una sección nueva, usar un `orden_seccion` que no exista todavía (ej. 17) y escribir su nombre en `seccion`.

## Paso 2 — Publicar la planilla como CSV

1. En Google Sheets: **Archivo → Compartir → Publicar en la web**.
2. En el primer desplegable elegí la hoja (pestaña) con el menú.
3. En el segundo desplegable elegí **Valores separados por comas (.csv)**.
4. Marcá "Volver a publicar automáticamente cuando se realicen cambios" si aparece esa opción (así no hay que repetir este paso cada vez).
5. Hacé clic en **Publicar** y copiá la URL que te da (empieza con `https://docs.google.com/spreadsheets/d/.../pub?output=csv`).

⚠️ Importante: "Publicar en la web" es distinto de "Compartir". Con este método cualquiera con el link puede *ver* el menú en formato CSV, pero no puede editarlo (para editar sigue haciendo falta acceso a la planilla real, con tu cuenta de Google).

## Paso 3 — Conectar la planilla al sitio

1. Abrí `index.html` con cualquier editor de texto.
2. Buscá esta línea, cerca del final del archivo:
   ```js
   const SHEET_CSV_URL = "REEMPLAZAR_CON_URL_CSV_DE_GOOGLE_SHEETS";
   ```
3. Reemplazá el texto entre comillas por la URL que copiaste en el paso anterior.
4. Guardá el archivo.

## Paso 4 — Publicar en GitHub Pages

1. Creá un repositorio nuevo en GitHub (por ejemplo `menu-delfin`).
2. Subí `index.html` y la carpeta `assets/` (con `logo.png` y `chef-dolphin.png` adentro, en minúsculas) a la raíz del repositorio. El `menu.csv` no hace falta subirlo — ya quedó cargado en Google Sheets.
   - ⚠️ Ojo con mayúsculas/minúsculas: GitHub Pages distingue `Assets/` de `assets/`. Si algo no carga en la web pero sí en tu PC, esta es la causa más común.
3. En el repositorio: **Settings → Pages** → en "Source" elegí la rama `main` y la carpeta `/ (root)`. Guardá.
4. GitHub te da una URL del tipo `https://tu-usuario.github.io/menu-delfin/`. Puede tardar 1-2 minutos en activarse.

## Cómo edita el administrador de ahora en más

Simplemente entra a la planilla de Google (con su cuenta), cambia precios o agrega/quita filas, y los cambios se reflejan solos en la web. Google puede tardar unos minutos en actualizar la versión publicada — si un cambio no aparece enseguida, esperar un par de minutos y refrescar la página con Ctrl+F5 (o Cmd+Shift+R en Mac).

Si por algún motivo la planilla no está disponible (sin publicar, sin internet, etc.), el sitio muestra la última versión que logró cargar guardada en el navegador de cada visitante, para no quedar en blanco.

## Datos de contacto en el header

La dirección y el teléfono que aparecen debajo de "San Clemente del Tuyú" están escritos directamente en `index.html` (no vienen de la planilla). Para cambiarlos, buscá este bloque cerca del principio del `<body>`:

```html
<p class="hero-contact">
  Av. XI 225<br>
  <a href="https://www.google.com/search?q=la+cantina+del+delfin#" target="_blank" rel="noopener">02252 42-3211</a>
</p>
```

## Notas sobre la carga inicial de datos

- Los precios que en el Word original figuraban como "$0000,00" (sin definir) quedaron con la celda `precio` vacía → se muestran como **"Consultar"**.
- Las dos tablas de "Sugerencias" y las dos de "Vinos Finos" que estaban repartidas en distintas páginas del Word se unificaron cada una en una sola sección, para que la navegación web tenga sentido.
