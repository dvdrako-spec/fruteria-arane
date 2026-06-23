# Frutería Arane — sitio web

Web estática (HTML + CSS + JS, sin frameworks ni build) para Frutería Arane,
Errekalde, Bilbao. Pensada para abrirse en local y, si más adelante quieres
escalarla, migrarla fácilmente a WordPress o a cualquier hosting.

## Probarla en local

No necesitas nada instalado. Hay dos formas:

1. **Doble clic en `index.html`** y se abre en el navegador. Las fuentes de
   Google Fonts necesitan conexión a internet; el resto funciona sin red.
2. (Opcional, recomendado) Servirla con un mini servidor local para que las
   rutas relativas (`css/`, `js/`) se comporten igual que en un hosting real:

   ```bash
   cd fruteria-arane
   python3 -m http.server 8000
   ```

   Y abre `http://localhost:8000` en el navegador.

## Estructura

```
fruteria-arane/
├── index.html        ← todo el contenido y estructura
├── css/style.css      ← estilos (paleta, tipografía, layout)
├── js/script.js        ← menú móvil + año del footer (sin dependencias)
└── images/             ← vacío: aquí van tus fotos reales si quieres añadirlas
```

Está hecho con HTML/CSS "de toda la vida": sin React, sin paso de compilación,
sin dependencias salvo dos tipografías de Google Fonts. Eso es justo lo que
hace fácil moverlo a otro sitio.

## Cómo escalarlo más adelante

Tienes tres caminos según cuánto quieras invertir:

### 1. Quedarte como está, en un hosting estático (el más simple)
Sirve para una web de "ficha de negocio" como esta, sin necesidad de
WordPress. Subes la carpeta tal cual a:
- **Netlify** o **Vercel**: arrastras la carpeta y ya tienes la web online
  con HTTPS gratis.
- **Hosting normal por FTP** (el que ya tenga Lanmedia o uno barato): subes
  los 3 archivos/carpetas a `public_html` y listo.

No hay base de datos, no hay backend, no se rompe con actualizaciones.

### 2. Meterlo dentro de un WordPress ya existente
Si en algún momento quieres que viva dentro de un WordPress (para tener
blog, más páginas, etc.), las opciones de menor a mayor esfuerzo:

- **Página con bloque HTML personalizado**: crea una página nueva, añade un
  bloque "HTML personalizado" y pega el contenido de dentro de `<body>`
  (sin las etiquetas `<header>`/`<html>`). El CSS lo subes como "CSS
  adicional" en *Apariencia → Personalizar → CSS adicional*, o con un
  plugin tipo **Simple Custom CSS and JS** (así puedes meter el `script.js`
  también).
- **Builder visual (Elementor / Divi)**: usan un widget "HTML" donde pegas
  el mismo contenido. Tendrás que recortar el `<header>` y `<footer>` si el
  tema ya pone los suyos.
- **Tema a medida / child theme**: si quieres que sea *la* portada del
  WordPress (no solo una página), conviertes `index.html` en
  `front-page.php`, mueves el CSS a `style.css` del child theme y el JS a
  `functions.php` con `wp_enqueue_script`. Esto ya es trabajo de
  desarrollo, pero el HTML/CSS que tienes aquí se reaprovecha entero, no
  hay que rehacer el diseño.

### 3. Convertirlo en un theme WordPress real
Si el negocio crece (más páginas, tienda online, blog de recetas, etc.),
este HTML/CSS sirve de base visual para un theme propio. La estructura ya
está pensada en secciones independientes (`hero`, `staples`, `schedule`,
`locate`, `footer`), que es exactamente como se organiza una plantilla de
WordPress (`header.php`, `front-page.php`, `footer.php`).

## Qué cambiar tú mismo

- **Horario / teléfono / dirección**: están en texto plano dentro de
  `index.html`, búscalos con Ctrl+F (`9:00`, `606 53 50 82`, `Arane Kalea`).
- **Fotos reales**: si quieres sustituir los iconos dibujados por fotos del
  local, añade tus imágenes a `images/` y dímelo — te preparo el `<img>`
  correspondiente. No he metido fotos de Google Maps directamente para no
  depender de un enlace externo que se puede romper.
- **Colores**: todos están arriba del todo en `css/style.css`, en
  `:root { ... }`. Cambiando esas 6-7 líneas cambia toda la web.
