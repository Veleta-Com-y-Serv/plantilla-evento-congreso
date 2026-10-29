# Plantilla NoExpertise · Evento y congreso

Web festiva a todo el ancho para congresos, jornadas, ferias, festivales y encuentros: portada como un cartel con la
fecha y el lugar en grande, cifras, el evento con sus ejes, programa por días en pestañas, ponentes en un mosaico de
colores, entradas como acreditaciones, galería de borde a borde, el lugar con cómo llegar, patrocinadores por nivel,
preguntas frecuentes, llamada a la acción y contacto con formulario.

- Sectores: evento, congreso, feria, festival, jornadas. Estilo: festivo. Plan mínimo: presencia.
- Secciones: hero, cifras, sobre, programa, ponentes, entradas, galeria, lugar, patrocinadores, preguntas, cta,
  contacto (+ `texto` genérico).
- Campos propios:
  - `hero.fecha` (las cifras del principio salen enormes), `hero.lugar`, `hero.etiquetas` (cadena con «;»).
  - `programa.programa[]` {dia, hora, titulo, texto, ponente, sala, categoria}: `dia` agrupa en pestañas y
    `categoria` da el color de la etiqueta.
  - `ponentes.personas[]` {nombre, cargo, foto, texto}: `texto` es el título de su charla.
  - `entradas.entradas[]` {nombre, precio, texto, incluye, destacado, url}, `entradas.boton`, `entradas.nota`.
  - `lugar.direccion` (si falta, la de contacto) y `lugar.items[]` {titulo, texto, icono: tren|bus|coche|avion}.
  - `patrocinadores.clientes[]` {nombre, nivel, imagen, url}: `nivel` agrupa; `imagen` es el logo (en gris).
  - `contacto.motivos` (cadena con «;» para el desplegable) y `contacto.boton`.
- Diseño: cobalto + rosa + crema + tinta índigo en bandas a todo el ancho con cortes en diagonal, títulos en sans del
  sistema a 900, monoespaciada para horas y antetítulos, botones en paralelogramo, fotos a sangre con bordes oblicuos,
  cabecera fija transparente sobre la portada, pie cobalto con el nombre gigante. Brief completo en `DISEÑO.md`.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio y de las preguntas frecuentes,
  `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos en `template.yaml`; reglas para el agente en `CLAUDE.md`; fotos a
  generar en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`).
Imágenes de relleno (`public/placeholders/`) dibujadas para esta plantilla, sin licencias de terceros.
