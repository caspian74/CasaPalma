# Casa Palma · sitio web

Sitio estático (HTML + CSS + JS en un solo archivo). No necesita instalar nada ni compilar.

## Estructura
- `index.html`: la página completa (menú, matcha, postres, contacto, SEO local)
- `assets/`: fotos optimizadas
- `favicon.png`, `apple-touch-icon.png`: iconos
- `robots.txt`, `_headers`, `404.html`: configuración para buscadores y Cloudflare

## 1. Subir a GitHub
1. Crea un repositorio nuevo en github.com (por ejemplo `casa-palma`), vacío y sin README.
2. En esta carpeta, en la terminal:
```
git init
git add .
git commit -m "Sitio Casa Palma"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/casa-palma.git
git push -u origin main
```
(O arrastra todos los archivos al repositorio con "Add file → Upload files". Sube también la carpeta `assets`.)

## 2a. Publicar en Cloudflare Workers (pantalla "Set up your application")
El repositorio ya incluye `wrangler.jsonc` y `.assetsignore`. Valores:
- Project name: `casapalma` (debe ser igual al `name` de `wrangler.jsonc`)
- Build command: vacío
- Deploy command: `npx wrangler deploy`
- Preview command: dejar el valor que sugiere Cloudflare

## 2b. Publicar en Cloudflare Pages (alternativa)
1. Entra a dash.cloudflare.com → **Workers & Pages** → **Create** → pestaña **Pages** → **Connect to Git**.
2. Elige el repositorio `casa-palma`.
3. Configuración:
   - Framework preset: **None**
   - Build command: *(vacío)*
   - Build output directory: `/`  (si no lo acepta, escribe `.`)
4. **Save and Deploy**. Quedará en `https://casa-palma.pages.dev` (o similar).

Sin GitHub: Workers & Pages → Create → Pages → **Upload assets**, y arrastra la carpeta completa (con `index.html` en la raíz).

Cada `git push` a `main` actualiza el sitio automáticamente.

## 3. Dominio propio
En el proyecto de Pages → **Custom domains** → **Set up a domain**. Cloudflare indica los registros DNS.

## 4. Después de tener el dominio (importante para SEO)
Reemplaza `https://TU-DOMINIO.com` por el dominio real.

En `index.html`, dentro de `<head>`, agrega:
```
<link rel="canonical" href="https://TU-DOMINIO.com/">
<meta property="og:url" content="https://TU-DOMINIO.com/">
<meta property="og:image" content="https://TU-DOMINIO.com/assets/bebidas-casa-palma.jpg">
```
En `robots.txt`, agrega al final:
```
Sitemap: https://TU-DOMINIO.com/sitemap.xml
```
Crea `sitemap.xml`:
```
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"><url><loc>https://TU-DOMINIO.com/</loc></url></urlset>
```
Luego da de alta el sitio en Google Search Console y envía el sitemap.

## 5. Local SEO (lo que más pesa)
- Reclama y completa el perfil de **Google Business Profile**: mismo nombre, dirección y teléfono que el sitio, horario, fotos y el enlace a la página.
- Agrega la **dirección exacta** (calle y número). Hoy el sitio solo dice "San Marino". Busca `San Marino, Tijuana` en `index.html` y en el bloque `streetAddress` del JSON-LD para actualizarla.

## Cambios frecuentes
- **Precios y menú:** editar en `index.html` las líneas `<li><span>…</span><b>$…</b></li>`.
- **WhatsApp:** el número está como `526643617949` (664 361 7949). Si cambia, reemplázalo en todo el archivo.
- **Fotos:** reemplaza los archivos de `assets/` conservando el nombre.
