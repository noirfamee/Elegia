# Elegia

Extensión de Chrome (Manifest V3) para **subrayar texto en PDFs con colores vivos** y **sacar capturas en imagen** de lo subrayado.

![Pantalla principal](docs/captura-pantalla.png)

## Características

- **3 temas de color**, cada uno con su paleta de 3 tonos (ver abajo), con mezcla *multiply*: el texto sigue legible.
- Dos estilos: bloque de rotulador o línea gruesa.
- Capturas PNG en alta resolución (página re-renderizada a ~2400 px de ancho): copiar al portapapeles o descargar.
- **Capturar todos**: una sola hoja con todos los subrayados en orden, con el color y la página de cada uno.
- Los subrayados se guardan automáticamente por documento (`chrome.storage.local`).
- Barra lateral con lista, filtro por color, ir al subrayado y copiar texto.
- Deshacer / rehacer, modo rotulador, atajos de teclado.
- Se abre automáticamente con los PDFs de Chrome (se puede desactivar).

![Ejemplo de «Capturar todos»](docs/ejemplo-capturar-todos.png)

## Temas y paletas

Se cambian con los tres botones de la barra superior; cada uno trae 3 colores (teclas `1`–`3`). La interfaz también toma el color de acento del tema.

| Tema | Colores |
|---|---|
| **New Order** — *Movement (1981)* | Aged paper `#D9D4C8` · Steel blue `#657A83` · Charcoal `#292C30` |
| **Francia** — *Parisian Modernism* | Azul marino `#172B55` · Marfil `#F5F0E8` · Rojo burdeos `#C93648` |
| **Rosa mexicano** — *nueva propuesta* | Rosa mexicano `#E4007C` · Rosa chicle `#F5A6C8` · Bugambilia `#7D174D` |

Los tonos muy oscuros (Charcoal, Azul marino, Bugambilia) se aplican con transparencia para no tapar el texto, y los muy claros (Aged paper, Marfil) llevan un borde fino para notarse sobre el papel blanco. Se ajusta en `THEMES` (`alpha`, `edge`) dentro de `viewer.js`; para añadir un tema basta con agregar otra entrada ahí.

Los subrayados guardados conservan su color aunque cambies de tema.

## Instalación

1. Clona o descarga este repositorio.
2. Abre `chrome://extensions` y activa **Modo de desarrollador**.
3. **Cargar descomprimida** → elige la carpeta del repositorio (la que contiene `manifest.json`).
4. Para PDFs locales: en **Detalles** activa **Permitir el acceso a las URL de archivo**.

## Uso

| Acción | Cómo |
|---|---|
| Abrir un PDF | Ábrelo en Chrome, clic en el ícono, `Alt+Shift+S`, clic derecho en un enlace → *Abrir PDF con Elegia*, o arrástralo a la ventana |
| Subrayar | Selecciona texto y elige color en la barra flotante |
| Subrayar + capturar | Botón de cámara de la barra flotante |
| Editar un subrayado | Clic sobre él: color, captura, copiar imagen/texto, borrar |
| Hoja con todo | **Capturar todos** en la barra lateral |

### Atajos

| Tecla | Acción |
|---|---|
| `1`–`3` | Color del tema actual (con texto seleccionado, lo subraya) |
| `H` | Subrayar la selección |
| `M` | Modo rotulador (subraya al soltar el mouse) |
| `Supr` | Borrar el subrayado activo |
| `Ctrl+Z` / `Ctrl+Y` | Deshacer / rehacer |
| `Ctrl` + rueda, `Ctrl +/−`, `Ctrl+0` | Zoom / ajustar al ancho |

## Cómo funciona

Chrome no permite que las extensiones modifiquen su visor de PDF nativo, así que la extensión incluye un visor propio basado en [PDF.js](https://mozilla.github.io/pdf.js/).

```
manifest.json     Permisos y configuración MV3
background.js     Service worker: redirige los PDFs al visor, menú contextual, atajo
viewer.html/css   Interfaz del visor
viewer.js         Render de páginas, selección, subrayados, capturas, almacenamiento
lib/              PDF.js (build min), cmaps y fuentes estándar
icons/            Íconos
docs/             Imágenes de la documentación
```

- **Selección → subrayado:** se leen los rectángulos reales de los glifos del *text layer*, se agrupan por línea y se guardan **normalizados (0–1)** por página, así sobreviven a cualquier zoom.
- **Capa de subrayados:** va entre el canvas del PDF y el text layer, con `mix-blend-mode: multiply`.
- **Capturas:** la página se re-renderiza a alta resolución, se recorta la zona subrayada y se dibujan los subrayados sobre el canvas.
- **Datos:** clave `doc:<fingerprint del PDF>`, así que los subrayados reaparecen aunque cambies el archivo de lugar.

## Permisos

| Permiso | Para qué |
|---|---|
| `storage` | Guardar subrayados y preferencias |
| `webRequest` + `<all_urls>` | Detectar respuestas `application/pdf` y abrirlas en el visor |
| `tabs`, `contextMenus` | Redirigir pestañas y menú de clic derecho |
| `clipboardWrite` | Copiar imágenes y texto |

Todo ocurre en local; la extensión no envía datos a ningún servidor.

## Limitaciones

- Solo PDFs con capa de texto. Los escaneados necesitan OCR (no incluido).
- Los subrayados no se escriben dentro del PDF; viven en la extensión.

## Ideas a futuro

- Exportar subrayados a Markdown / JSON.
- Notas en cada subrayado.
- Guardar un PDF con las anotaciones incrustadas.
- OCR para PDFs escaneados.

## Licencia

MIT — ver [LICENSE](LICENSE). Incluye PDF.js (Apache-2.0) en `lib/`.
