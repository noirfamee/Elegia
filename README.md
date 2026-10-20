# Elegia

> A PDF highlighter with designer color palettes and image captures of your highlights, right in Chrome.

**English** · [Español](#español)

![Main screen](docs/captura-pantalla.png)

**Elegia** is a PDF reader with a built-in highlighter, delivered as a Chrome extension. It replaces Chrome's default PDF viewer with its own, where you can highlight text using designer color palettes and capture images of what you've marked.

**What it's for:** active reading. You read, mark what matters, then export everything you highlighted as a single image. Useful for studying, quoting, or reviewing without rereading the whole document.

**What sets it apart:**
- Designer color themes (New Order, Francia, Rosa mexicano) instead of the usual yellow.
- Each highlight can be captured as a clean image, ready to share or paste into notes.
- Everything is local: nothing is uploaded to a server, and highlights are stored in your browser.

**What it isn't:** it doesn't edit the PDF or write the marks into the file, and it can't read scanned PDFs (no OCR).

## Contents

- [Install](#install)
- [Quick start](#quick-start)
- [Using Elegia](#using-elegia)
- [Color themes](#color-themes)
- [Keyboard shortcuts](#keyboard-shortcuts)
- [Settings](#settings)
- [Troubleshooting](#troubleshooting)
- [How it works](#how-it-works)
- [Permissions and privacy](#permissions-and-privacy)
- [Limitations](#limitations)
- [Development](#development)
- [Roadmap](#roadmap)
- [License](#license)

## Install

Elegia isn't on the Chrome Web Store yet, so you load it as an unpacked extension (works in Chrome, Edge, Brave and other Chromium browsers):

1. Clone or download this repository. If you downloaded a ZIP, unzip it.
2. Open `chrome://extensions` and turn on **Developer mode** (top right).
3. Click **Load unpacked** and select the project folder, the one that contains `manifest.json`.
4. Click the puzzle icon 🧩 next to the address bar and pin **Elegia**.
5. *(Optional, for PDFs saved on your computer)* open the extension's **Details** and turn on **Allow access to file URLs**.

> Keep the folder where it is. If you move or delete it, Chrome will disable the extension.

## Quick start

1. Open any PDF in Chrome. It loads in Elegia automatically.
2. Select some text. A small floating bar appears over the selection.
3. Click a color. The text is highlighted.
4. Click the camera button to highlight and get an image at the same time, or click an existing highlight to capture, copy or delete it.

## Using Elegia

### Opening a PDF

| Method | How |
|---|---|
| From the web | Open or click a PDF link in Chrome; it redirects to Elegia automatically |
| Toolbar icon | Click the Elegia icon on a tab that shows a PDF |
| Shortcut | `Alt+Shift+S` on the current PDF tab |
| Right-click | On a link: *Abrir PDF con Elegia*. On a PDF page: *Subrayar este PDF con Elegia* |
| From your computer | **Abrir PDF** button, `Ctrl+O`, or drag and drop a file onto the window |

### Highlighting

- **Select, then pick a color** in the floating bar, or press `1`–`3` while the text is selected.
- **Marker mode** (`Auto` button or `M`): every selection is highlighted the moment you release the mouse.
- **Two styles:** a marker block or a thick underline. Switch them in the top bar; if a highlight's menu is open, the style is applied to it.
- Highlights can span several lines and several pages.

### Editing a highlight

Click any highlight to open its menu: change its color, download its capture, copy the capture or its text, or delete it. You can also press `Delete` while it's selected, and undo with `Ctrl+Z`.

### Captures

- **Single highlight:** the camera button in the selection bar (highlights and shows the capture), or the capture button in a highlight's menu or in the sidebar. You get a preview where you can **Copy image** or **Download PNG**.
- **All highlights:** **Capturar todos** in the sidebar builds one sheet with every highlight in reading order, with its page number and color bar. If you filter by color, only that color is exported.
- Captures are rendered at about 2400 px wide, so they stay sharp.

![Sheet with all highlights](docs/ejemplo-capturar-todos.png)

### Sidebar

The right panel lists all highlights of the document in reading order.

- Click one to jump to it in the page.
- Use the color chips to filter the list.
- **Copiar texto** copies the text of all (or the filtered) highlights, with page numbers.
- Toggle the panel with the ☰ button.

### Zoom

`Ctrl` + mouse wheel, `Ctrl +` / `Ctrl −`, the `+` / `−` buttons, or `Ctrl+0` / click the percentage to fit the page to the window width.

### Your highlights are saved

Highlights are stored automatically in your browser, per document. Open the same PDF again later and they're back, even if you moved the file.

## Color themes

Switch themes with the three buttons in the top bar. Each theme has three colors, mapped to keys `1`–`3`. The interface accent color follows the theme.

| Theme | Colors |
|---|---|
| **New Order** — *Movement (1981)* | Aged paper `#D9D4C8` · Steel blue `#657A83` · Charcoal `#292C30` |
| **Francia** — *Parisian Modernism* | Azul marino `#172B55` · Marfil `#F5F0E8` · Rojo burdeos `#C93648` |
| **Rosa mexicano** — *nueva propuesta* | Rosa mexicano `#E4007C` · Rosa chicle `#F5A6C8` · Bugambilia `#7D174D` |

Very dark colors (Charcoal, Azul marino, Bugambilia) are applied with some transparency so they don't hide the text, and very light ones (Aged paper, Marfil) get a thin border so they show on white paper. Existing highlights keep their color when you switch themes.

**Add your own theme:** add an entry to `THEMES` in `viewer.js` with three colors (`hex`, and optionally `alpha`, `edge`, `ui`) and it appears in the top bar.

## Keyboard shortcuts

| Key | Action |
|---|---|
| `1` `2` `3` | Pick a color of the current theme (highlights the selection if there is one) |
| `H` | Highlight the current selection |
| `M` | Toggle marker mode |
| `Delete` | Delete the active highlight |
| `Ctrl+Z` / `Ctrl+Y` | Undo / redo |
| `Ctrl+O` | Open a PDF from your computer |
| `Ctrl` + wheel, `Ctrl +`, `Ctrl −`, `Ctrl+0` | Zoom in / out / fit to width |
| `Esc` | Close the preview or menus and clear the selection |
| `Alt+Shift+S` | Open the current PDF in Elegia |

## Settings

At the bottom of the sidebar:

- **Open Chrome PDFs here automatically:** turn it off if you'd rather keep Chrome's own viewer and open Elegia manually.
- **Ver en el visor normal de Chrome:** sends the current PDF back to Chrome's viewer (for example to print or use Chrome's form filling).

## Troubleshooting

| Problem | Fix |
|---|---|
| *"Manifest file is missing or unreadable"* when loading | You selected the wrong folder. Choose the one that directly contains `manifest.json`, `viewer.html` and `lib/` |
| Local PDFs (`file://`) don't load | Enable **Allow access to file URLs** in the extension's Details, or drag the PDF onto the window |
| A PDF opens in Chrome's viewer instead of Elegia | Click the Elegia icon on that tab, or check that the automatic option is on |
| I can't select any text | The PDF is probably scanned (an image). Elegia needs a text layer; OCR isn't included |
| Highlights are slightly offset on a strange PDF | Some PDFs have unusual text positioning; try another zoom level, or report it with the file if it isn't private |
| The extension stopped working after moving the folder | Chrome tracks the original path. Remove it and load the folder again |
| Highlights disappeared | They live in the browser's extension storage. Clearing extension data or uninstalling the extension removes them |
| "Copy image" fails | Chrome needs the page focused to write to the clipboard; use **Download PNG** instead |

## How it works

Chrome doesn't let extensions modify its native PDF viewer, so Elegia ships its own, built on [PDF.js](https://mozilla.github.io/pdf.js/).

```
manifest.json     Permissions and MV3 configuration
background.js     Service worker: redirects PDFs to the viewer, context menus, shortcut
viewer.html/css   Viewer interface
viewer.js         Page rendering, selection, highlights, captures, storage, themes
lib/              PDF.js (minified build), cmaps and standard fonts
icons/            Icons
docs/             Documentation images
```

- **Selection → highlight:** the real glyph rectangles of the text layer are read, grouped by line and stored **normalized (0–1)** per page, so they survive any zoom level.
- **Highlight layer:** sits between the PDF canvas and the text layer, using `mix-blend-mode: multiply`.
- **Captures:** the page is re-rendered at high resolution, the highlighted region is cropped, and highlights are drawn on top of the canvas.
- **Storage:** key `doc:<PDF fingerprint>` in `chrome.storage.local`, so highlights come back even if the file moves.
- **Preferences:** theme, color, style, marker mode and sidebar state are stored in `prefs`.

## Permissions and privacy

| Permission | Why |
|---|---|
| `storage` | Save highlights and preferences |
| `webRequest` + `<all_urls>` | Detect `application/pdf` responses and open them in the viewer |
| `tabs`, `contextMenus` | Redirect tabs and the right-click menu |
| `clipboardWrite` | Copy images and text |

Everything happens locally. Elegia doesn't send data to any server and doesn't use analytics. The PDFs you open stay on your machine.

## Limitations

- Only PDFs with a text layer. Scanned PDFs need OCR (not included).
- Highlights aren't written into the PDF; they live in the extension.
- Highlights are tied to the browser profile where you made them, not synced between devices.

## Development

There is no build step. Edit the files, then press the reload button of the extension in `chrome://extensions` and refresh the viewer tab.

- All app logic is in `viewer.js`; `THEMES` at the top defines the palettes.
- `window.__subrayador` exposes `state`, `highlightSelection` and `captureHighlight` for testing from the console.
- To update PDF.js, replace `lib/pdf.min.mjs` and `lib/pdf.worker.min.mjs` with the same version of both files.

## Roadmap

- Export highlights to Markdown / JSON.
- Notes attached to each highlight.
- Save a PDF with the annotations embedded.
- OCR for scanned PDFs.
- Sync highlights between devices.

## License

MIT, see [LICENSE](LICENSE). Includes PDF.js (Apache-2.0) in `lib/`.

---

# Español

> Marcatextos para PDFs con paletas de color de diseño y capturas de tus subrayados, directo en Chrome.

**Elegia** es un visor de PDF con marcatextos integrado, hecho como extensión de Chrome. Reemplaza el visor normal de Chrome por uno propio, donde puedes subrayar con paletas de color y sacar capturas en imagen de lo subrayado.

**Para qué sirve:** lectura activa. Lees, marcas lo importante y después sacas en una sola imagen todo lo que subrayaste. Sirve para estudiar, citar o repasar sin releer el documento entero.

**Qué la distingue:**
- Temas de color de diseño (New Order, Francia, Rosa mexicano) en vez del amarillo de siempre.
- Cada subrayado se puede capturar como imagen limpia, lista para compartir o pegar en tus notas.
- Todo es local: nada se sube a un servidor y los subrayados se guardan en tu navegador.

**Lo que no es:** no edita el PDF ni escribe las marcas dentro del archivo, y no lee PDFs escaneados (no tiene OCR).

## Instalación

Elegia aún no está en la Chrome Web Store, así que se carga como extensión descomprimida (funciona en Chrome, Edge, Brave y otros navegadores Chromium):

1. Clona o descarga este repositorio. Si bajaste un ZIP, descomprímelo.
2. Abre `chrome://extensions` y activa **Modo de desarrollador** (arriba a la derecha).
3. Pulsa **Cargar descomprimida** y elige la carpeta del proyecto, la que contiene `manifest.json`.
4. Pulsa el ícono de rompecabezas 🧩 junto a la barra de direcciones y fija **Elegia**.
5. *(Opcional, para PDFs guardados en tu computadora)* en **Detalles** de la extensión activa **Permitir el acceso a las URL de archivo**.

> Deja la carpeta donde está. Si la mueves o la borras, Chrome desactivará la extensión.

## Inicio rápido

1. Abre cualquier PDF en Chrome. Se carga solo en Elegia.
2. Selecciona texto. Aparece una barrita flotante sobre la selección.
3. Elige un color y el texto queda subrayado.
4. El botón de cámara subraya y te da la imagen al mismo tiempo. Si haces clic en un subrayado ya hecho, puedes capturarlo, copiarlo o borrarlo.

## Cómo se usa

### Abrir un PDF

| Forma | Cómo |
|---|---|
| Desde internet | Abre o haz clic en un enlace a un PDF en Chrome; se redirige a Elegia automáticamente |
| Ícono de la barra | Clic en el ícono de Elegia en una pestaña con un PDF |
| Atajo | `Alt+Shift+S` en la pestaña del PDF |
| Clic derecho | Sobre un enlace: *Abrir PDF con Elegia*. En una página PDF: *Subrayar este PDF con Elegia* |
| Desde tu computadora | Botón **Abrir PDF**, `Ctrl+O`, o arrastra el archivo a la ventana |

### Subrayar

- **Selecciona y elige color** en la barra flotante, o pulsa `1`–`3` con el texto seleccionado.
- **Modo rotulador** (botón `Auto` o tecla `M`): cada selección se subraya al soltar el mouse.
- **Dos estilos:** bloque de rotulador o línea gruesa. Se cambian en la barra superior; si el menú de un subrayado está abierto, el estilo se aplica a ese subrayado.
- Un subrayado puede abarcar varias líneas y varias páginas.

### Editar un subrayado

Haz clic en cualquier subrayado para abrir su menú: cambiar el color, descargar su captura, copiar la captura o el texto, o borrarlo. También puedes pulsar `Supr` con el subrayado activo, y deshacer con `Ctrl+Z`.

### Capturas

- **Un subrayado:** el botón de cámara de la barra de selección (subraya y muestra la captura), o el botón de captura en el menú del subrayado o en la barra lateral. Se abre una vista previa donde puedes **Copiar imagen** o **Descargar PNG**.
- **Todos los subrayados:** **Capturar todos** en la barra lateral arma una hoja con todos los subrayados en orden de lectura, con su página y una barra del color. Si filtras por color, solo se exporta ese color.
- Las capturas se generan a unos 2400 px de ancho, así que salen nítidas.

### Barra lateral

El panel derecho lista todos los subrayados del documento en orden de lectura.

- Haz clic en uno para ir a él en la página.
- Usa los chips de color para filtrar.
- **Copiar texto** copia el texto de todos (o de los filtrados) con su página.
- Se muestra u oculta con el botón ☰.

### Zoom

`Ctrl` + rueda del mouse, `Ctrl +` / `Ctrl −`, los botones `+` / `−`, o `Ctrl+0` / clic en el porcentaje para ajustar la página al ancho de la ventana.

### Tus subrayados se guardan solos

Se guardan automáticamente en tu navegador, por documento. Si abres el mismo PDF después, vuelven a aparecer, aunque hayas movido el archivo.

## Temas de color

Se cambian con los tres botones de la barra superior. Cada tema trae tres colores, asignados a las teclas `1`–`3`. El color de acento de la interfaz sigue al tema.

| Tema | Colores |
|---|---|
| **New Order** — *Movement (1981)* | Aged paper `#D9D4C8` · Steel blue `#657A83` · Charcoal `#292C30` |
| **Francia** — *Parisian Modernism* | Azul marino `#172B55` · Marfil `#F5F0E8` · Rojo burdeos `#C93648` |
| **Rosa mexicano** — *nueva propuesta* | Rosa mexicano `#E4007C` · Rosa chicle `#F5A6C8` · Bugambilia `#7D174D` |

Los tonos muy oscuros (Charcoal, Azul marino, Bugambilia) se aplican con transparencia para no tapar el texto, y los muy claros (Aged paper, Marfil) llevan un borde fino para notarse sobre el papel blanco. Los subrayados existentes conservan su color al cambiar de tema.

**Agregar un tema propio:** añade una entrada a `THEMES` en `viewer.js` con tres colores (`hex` y, opcionalmente, `alpha`, `edge`, `ui`) y aparece en la barra superior.

## Atajos de teclado

| Tecla | Acción |
|---|---|
| `1` `2` `3` | Color del tema actual (si hay texto seleccionado, lo subraya) |
| `H` | Subrayar la selección |
| `M` | Activar/desactivar el modo rotulador |
| `Supr` | Borrar el subrayado activo |
| `Ctrl+Z` / `Ctrl+Y` | Deshacer / rehacer |
| `Ctrl+O` | Abrir un PDF de tu computadora |
| `Ctrl` + rueda, `Ctrl +`, `Ctrl −`, `Ctrl+0` | Acercar / alejar / ajustar al ancho |
| `Esc` | Cerrar la vista previa o los menús y quitar la selección |
| `Alt+Shift+S` | Abrir el PDF actual en Elegia |

## Ajustes

Al final de la barra lateral:

- **Abrir PDFs de Chrome aquí automáticamente:** apágalo si prefieres conservar el visor de Chrome y abrir Elegia manualmente.
- **Ver en el visor normal de Chrome:** manda el PDF actual de vuelta al visor de Chrome (por ejemplo para imprimir o llenar formularios).

## Solución de problemas

| Problema | Solución |
|---|---|
| *«Falta el archivo de manifiesto»* al cargar | Elegiste la carpeta equivocada. Escoge la que contiene directamente `manifest.json`, `viewer.html` y `lib/` |
| Los PDFs locales (`file://`) no cargan | Activa **Permitir el acceso a las URL de archivo** en los Detalles de la extensión, o arrastra el PDF a la ventana |
| Un PDF se abre en el visor de Chrome y no en Elegia | Pulsa el ícono de Elegia en esa pestaña, o revisa que la opción automática esté activa |
| No puedo seleccionar texto | El PDF seguramente es escaneado (imagen). Elegia necesita capa de texto; no incluye OCR |
| Los subrayados salen un poco desalineados en un PDF raro | Algunos PDFs posicionan el texto de forma inusual; prueba otro zoom o repórtalo con el archivo si no es privado |
| Dejó de funcionar al mover la carpeta | Chrome recuerda la ruta original. Quita la extensión y vuelve a cargar la carpeta |
| Desaparecieron mis subrayados | Viven en el almacenamiento de la extensión del navegador. Borrar los datos o desinstalar la extensión los elimina |
| «Copiar imagen» falla | Chrome necesita la página enfocada para escribir en el portapapeles; usa **Descargar PNG** |

## Cómo funciona

Chrome no permite que las extensiones modifiquen su visor de PDF nativo, así que Elegia trae uno propio, basado en [PDF.js](https://mozilla.github.io/pdf.js/).

```
manifest.json     Permisos y configuración MV3
background.js     Service worker: redirige los PDFs al visor, menú contextual, atajo
viewer.html/css   Interfaz del visor
viewer.js         Render de páginas, selección, subrayados, capturas, almacenamiento, temas
lib/              PDF.js (build min), cmaps y fuentes estándar
icons/            Íconos
docs/             Imágenes de la documentación
```

- **Selección → subrayado:** se leen los rectángulos reales de los glifos del *text layer*, se agrupan por línea y se guardan **normalizados (0–1)** por página, así sobreviven a cualquier zoom.
- **Capa de subrayados:** va entre el canvas del PDF y el text layer, con `mix-blend-mode: multiply`.
- **Capturas:** la página se re-renderiza en alta resolución, se recorta la zona subrayada y se dibujan los subrayados sobre el canvas.
- **Datos:** clave `doc:<huella del PDF>` en `chrome.storage.local`, así que los subrayados reaparecen aunque cambies el archivo de lugar.
- **Preferencias:** tema, color, estilo, modo rotulador y estado de la barra lateral se guardan en `prefs`.

## Permisos y privacidad

| Permiso | Para qué |
|---|---|
| `storage` | Guardar subrayados y preferencias |
| `webRequest` + `<all_urls>` | Detectar respuestas `application/pdf` y abrirlas en el visor |
| `tabs`, `contextMenus` | Redirigir pestañas y el menú de clic derecho |
| `clipboardWrite` | Copiar imágenes y texto |

Todo ocurre en local. Elegia no envía datos a ningún servidor ni usa analíticas. Los PDFs que abres se quedan en tu computadora.

## Limitaciones

- Solo PDFs con capa de texto. Los escaneados necesitan OCR (no incluido).
- Los subrayados no se escriben dentro del PDF; viven en la extensión.
- Los subrayados están ligados al perfil del navegador donde los hiciste; no se sincronizan entre dispositivos.

## Desarrollo

No hay paso de compilación. Edita los archivos, pulsa el botón de recargar de la extensión en `chrome://extensions` y actualiza la pestaña del visor.

- Toda la lógica está en `viewer.js`; `THEMES` al inicio define las paletas.
- `window.__subrayador` expone `state`, `highlightSelection` y `captureHighlight` para probar desde la consola.
- Para actualizar PDF.js, reemplaza `lib/pdf.min.mjs` y `lib/pdf.worker.min.mjs` con la misma versión de ambos archivos.

## Ideas a futuro

- Exportar subrayados a Markdown / JSON.
- Notas en cada subrayado.
- Guardar un PDF con las anotaciones incrustadas.
- OCR para PDFs escaneados.
- Sincronizar subrayados entre dispositivos.

## Licencia

MIT, ver [LICENSE](LICENSE). Incluye PDF.js (Apache-2.0) en `lib/`.
