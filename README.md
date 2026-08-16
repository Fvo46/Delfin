# La Cantina del Delfín — Carta web + panel de administración

Sitio estático (HTML/CSS/JS, sin build) con:

- **`index.html`** — la carta pública. Lee el menú desde `menu.csv`, en la misma carpeta.
- **`admin.html`** — panel de administración para editar precios e ítems desde el navegador, sin tocar código. Los cambios se guardan directo en el repositorio de GitHub.
- **`menu.csv`** — los datos del menú. No hace falta editarlo a mano: se edita desde `admin.html`.
- **`assets/`** — logo del restaurante.

## Publicar el sitio en GitHub Pages

1. Creá un repositorio en GitHub (por ejemplo `menu-delfin`). Puede ser público (necesario para Pages gratis con una cuenta personal común).
2. Subí **todos** estos archivos y carpetas a la raíz del repositorio: `index.html`, `admin.html`, `menu.csv`, y la carpeta `assets/` con tus propios `logo.png` y `chef-dolphin.png` adentro (el código ya está preparado para `.png` en vez de `.jpg`).
   - ⚠️ Ojo con mayúsculas/minúsculas: GitHub Pages distingue `Assets/` de `assets/`, y `Logo.png` de `logo.png`. Si algo no carga en la web (como el logo) pero sí funciona en tu PC, esta es la causa más común.
   - Si en algún momento volvés a cambiar el formato de las imágenes (por ejemplo a `.webp`), hay que actualizar el nombre en 4 lugares: el ícono y la imagen del header en `index.html`, la imagen del footer en `index.html`, y el ícono/logo en `admin.html`.
3. En el repositorio: **Settings → Pages** → en "Source" elegí la rama `main` y la carpeta `/ (root)`. Guardá.
4. GitHub te da una URL del tipo `https://tu-usuario.github.io/menu-delfin/`. Puede tardar 1-2 minutos en activarse.

## Crear el token de acceso para el panel de administración

El panel necesita un token de GitHub para poder guardar cambios en el repositorio. Usá uno de permisos acotados, **no tu contraseña ni un token con acceso a todo**:

1. En GitHub: entrá a tu foto de perfil (arriba a la derecha) → **Settings**.
2. En el menú de la izquierda, abajo del todo: **Developer settings**.
3. **Personal access tokens → Fine-grained tokens → Generate new token**.
4. En **Repository access** elegí **Only select repositories** y seleccioná únicamente el repositorio del menú (ej. `menu-delfin`).
5. En **Permissions → Repository permissions**, buscá **Contents** y ponelo en **Read and write**. El resto puede quedar en "No access".
6. Elegí una fecha de expiración (recomendado: 90 días — después hay que generar uno nuevo y volver a pegarlo en el panel).
7. **Generate token** y copiá el valor que empieza con `github_pat_...`. GitHub solo lo muestra una vez.

## Usar el panel de administración

1. Entrá a `https://tu-usuario.github.io/menu-delfin/admin.html` (esta URL no está enlazada desde la carta pública — compartila solo con quien vaya a administrar precios).
2. La primera vez te va a pedir:
   - **Usuario u organización de GitHub** (ej. `tu-usuario`)
   - **Nombre del repositorio** (ej. `menu-delfin`)
   - **Rama**: `main`
   - **Ruta del archivo**: `menu.csv`
   - **Token**: el que generaste arriba
3. Con eso conectado, vas a ver el menú completo organizado por secciones, con cada plato en una fila editable.
4. Podés:
   - Cambiar nombre, precio, segundo precio (para platos con dos precios, como "Pescados a la Parrilla"), o nota de cualquier plato.
   - Agregar o eliminar platos dentro de una sección (**+ Agregar ítem** / botón ✕).
   - Reordenar platos y secciones con las flechas ↑ ↓.
   - Agregar o eliminar secciones completas.
   - Usar el campo **Grupo** solo si querés subagrupar ítems dentro de una sección (así están armados los Vinos Finos, agrupados por bodega).
5. Cuando termines, tocá **Guardar cambios en GitHub**. El cambio queda commiteado en el repositorio al instante; la carta pública (`index.html`) puede tardar uno o dos minutos en reflejarlo, porque GitHub Pages cachea los archivos brevemente.

### Notas de seguridad

- El token queda guardado únicamente en el navegador del dispositivo desde el que entrás al panel (en `localStorage`). No se envía a ningún lado más que a la API de GitHub.
- Si vas a usar el panel desde una computadora compartida, tocá **Cerrar sesión** al terminar — eso borra el token guardado en ese navegador (no lo revoca en GitHub; para eso hay que borrarlo desde Settings → Developer settings en GitHub).
- Si el token se vence o lo perdés, simplemente generá uno nuevo siguiendo los pasos de arriba y pegalo de nuevo en **Configuración** dentro del panel.
- Dado que el sitio es estático (sin servidor propio), no hay forma de tener una contraseña "real" de administrador — la clave de acceso del token cumple ese rol. Por eso conviene mantenerlo acotado a un solo repositorio y con fecha de expiración.

## Formato de `menu.csv` (referencia, normalmente no hace falta tocarlo a mano)

| Columna | Qué es |
|---|---|
| `orden_seccion` | Orden de la sección |
| `seccion` | Nombre de la sección |
| `subtitulo_seccion` | Aclaración opcional en itálica bajo el título |
| `grupo` | Subgrupo opcional dentro de la sección (ej. bodega en Vinos) |
| `orden_item` | Orden del plato dentro de su sección |
| `item` | Nombre del plato |
| `precio` | Precio (vacío = "Consultar") |
| `precio2` | Segundo precio opcional |
| `nota` | Descripción/ingredientes opcional |

## Notas sobre la carga inicial de datos

- Los precios que en el Word original figuraban sin definir se guardaron con el campo `precio` vacío → se muestran como **"Consultar"**.
- Las dos tablas de "Sugerencias" y las dos de "Vinos Finos" que estaban repartidas en distintas páginas del Word se unificaron cada una en una sola sección.
