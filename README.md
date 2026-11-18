# MERKICKS

Showroom estático de MERKICKS: portada con seis destacados, catálogo filtrable por marca y 212 fichas con fotografías y enlaces de contacto por WhatsApp.

## Desarrollo local

Requiere Node.js 20 o posterior. No hay dependencias externas.

```sh
npm run build
npm run check
npm run dev
```

Abre `http://127.0.0.1:4173/MERKICKS/`. El servidor local sirve la carpeta generada `dist/` bajo el mismo prefijo que GitHub Pages.

## GitHub Pages

La URL pública es `https://diego-mercado14.github.io/MERKICKS/`. El workflow `.github/workflows/pages.yml` genera `dist/`, comprueba las 212 fichas y publica el artefacto en cada push a `main`.

En **Settings → Pages → Build and deployment → Source**, usa **GitHub Actions**. No es necesario configurar una rama `gh-pages` ni publicar `dist/` en Git.

El workflow obtiene `SITE_ORIGIN` y `SITE_BASE_PATH` del nombre actual del repositorio. Así publica bajo `/ppp/` mientras el repositorio tenga ese nombre y bajo `/MERKICKS/` después de renombrarlo. `site.config.json` conserva la URL definitiva para el desarrollo local. El generador crea canonical URLs, metadatos Open Graph y `sitemap.xml` con la ruta activa.

No publiques la carpeta `public/` directamente: contiene solo los recursos base. `npm run build` genera `dist/` con la portada, todas las fichas y los recursos.

## Estructura

- `data/catalog.json`: modelos y sus fotos optimizadas.
- `data/scenes.json`: configuración de los seis destacados.
- `public/products/`: 512 fotos únicas en tres tamaños WebP, incluidas en el repositorio para que el build sea reproducible sin servicios externos.
- `merkicks-original.svg`: logo original usado por el sitio.
- `src/`: estilos y comportamiento.
- `scripts/build.mjs`: genera los HTML estáticos y metadatos.
- `scripts/check.mjs`: comprueba rutas, recursos y enlaces.
- `scripts/serve.mjs`: vista previa local.

Para añadir o retirar productos, actualiza `data/catalog.json` y los WebP correspondientes. `npm run build` regenera `dist/` desde cero.
