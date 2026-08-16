# La Cantina del Delfín — Carta web

Sitio estático (HTML/CSS, sin dependencias de build) con la carta completa del restaurante, listo para publicarse gratis en GitHub Pages.

## Cómo publicarlo en GitHub Pages

1. Creá un repositorio nuevo en GitHub (por ejemplo `menu-delfin`).
2. Subí estos dos elementos a la raíz del repositorio:
   - `index.html`
   - la carpeta `assets/` (contiene el logo)
3. En el repositorio, andá a **Settings → Pages**.
4. En "Source" elegí la rama `main` y la carpeta `/ (root)`. Guardá.
5. GitHub te va a dar una URL del estilo `https://tu-usuario.github.io/menu-delfin/`. Puede tardar 1-2 minutos en activarse.

## Editar precios o platos

Todo el contenido está en `index.html`, dentro de bloques `<section class="menu-section" id="...">`. Cada plato es una línea `<li class="item">...</li>` con el nombre y el precio. Podés editar el archivo directamente desde GitHub (lápiz de "Edit" en cada archivo) sin necesidad de programas especiales.

## Notas sobre la carga de datos

- Los precios que en el Word original figuraban como "$0000,00" (sin definir) se muestran como **"Consultar"**.
- Las dos tablas de "Sugerencias" y las dos de "Vinos Finos" que estaban repartidas en distintas páginas del Word se unificaron cada una en una sola sección, para que la navegación web tenga sentido.
