# Plantilla «Evento y congreso» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **festivo**
(«cartel de congreso en bloques diagonales»: bandas a todo el ancho en cobalto, rosa, noche y crema con cortes en
diagonal, títulos en sans del sistema a 900, horas y antetítulos en monoespaciada, botones en paralelogramo, fotos a
sangre). Brief de diseño en `DISEÑO.md`. Todo en castellano de España, frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = cobalto de cifras, lugar, pie y entrada destacada; acento = rosa de botones, fecha y horas; fondo = crema; texto = tinta). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…); los derivados (noche, violeta, crema rosada, cielo, rosa legible) se calculan con `color-mix` en `src/styles/global.css`.
- **Tipografías y aspecto general**: `src/styles/global.css` (`--fuente-texto`, `--fuente-titulos`, `--fuente-mono`, bandas `.banda--noche|azul|rosa|crema|crema2|cielo|violeta`, corte diagonal `.corte` / `.corte--inv`, botones `.btn`/`.btn-sec`, cabecera `.cabecera--congreso`, pie `.pie--congreso`). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Las fotos van en `public/fotos/`; las de respaldo en `public/placeholders/` (`Imagen.astro` cambia a la de respaldo si una foto falta). En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Fotos sin caras reconocibles. Ponentes sin foto: `/placeholders/persona.svg`.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = sello de bloques con la inicial y el nombre.
- **Menú**: `site.yaml → menu` (desde 1180 px en línea; por debajo, menú plegable) y `boton_cabecera` (botón rosa).
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie`.

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`. Un apartado nuevo puede reutilizar un diseño con `tipo: <id>`.
- `hero` → `hero.astro`: cartel a pantalla completa; `antetitulo`, `titulo`, `fecha`, `lugar`, `texto`, `cta`, `cta_secundario`, `imagen`, `etiquetas` («;»). Tiene que ir la primera para que la cabecera sea transparente encima.
- `cifras` → `cifras.astro`: `items` {titulo = cifra, texto}. Sin cifras no se pinta.
- `sobre` → `sobre.astro`: 50/50 con foto a sangre; `texto` (párrafos separados por línea en blanco), `imagen`, `items` (ejes numerados), `cta`.
- `programa` → `programa.astro`: `programa` {dia, hora, titulo, texto, ponente, sala, categoria}, `cta`. Pestañas por `dia`. Sin sesiones no se pinta.
- `ponentes` → `ponentes.astro`: `personas` {nombre, cargo, foto, texto = su charla}. Sin personas no se pinta.
- `entradas` → `entradas.astro`: `entradas` {nombre, precio, texto, incluye, destacado, url}, `boton`, `nota`, `cta`. Sin entradas no se pinta.
- `galeria` → `galeria.astro`: `galeria` (rutas), `cta`. Sin fotos no se pinta.
- `lugar` → `lugar.astro`: 50/50 con foto a sangre; `texto`, `direccion` (si falta, la de contacto), `imagen`, `items` {titulo, texto, icono}, `cta`.
- `patrocinadores` → `patrocinadores.astro`: `clientes` {nombre, nivel, imagen, url}, `cta`. Sin patrocinadores no se pinta.
- `preguntas` → `preguntas.astro`: `preguntas` en acordeón. Sin preguntas no se pinta.
- `cta` → `cta.astro`: banda rosa con `antetitulo`, `titulo`, `texto`, `cta`, `cta_secundario` (y la fecha de la portada de adorno).
- `contacto` → `contacto.astro`: datos de `contacto`, `texto`, `motivos` («;»), `boton`; formulario con entidad y motivo.
- `texto` → `texto.astro`: apartado genérico (`tipo: texto`) con `imagen`, `items`, `cta`.

## Campos propios de esta plantilla (además del esquema común)
- `hero.fecha`: texto libre; si empieza por cifras («15—17 de abril de 2027», «8 y 9 de mayo»), las cifras salen enormes y el resto al lado. `hero.lugar`: una línea. `hero.etiquetas`: UNA cadena separada por «;».
- `programa.programa`: `dia` es el nombre de la pestaña («Jueves 15»); las sesiones del mismo día van juntas en el orden del fichero. `categoria` (Ponencia, Mesa redonda, Taller, Pausa, Visita…) da un color por categoría. Máximo 24 sesiones.
- `entradas.entradas`: `precio` siempre como cadena («45 €», «Consultar»); vacío = no se muestra. `incluye` es UNA cadena separada por «;», nunca una lista. `destacado: true` en una como mucho. `url`: la web de venta de entradas o `/#contacto`.
- `patrocinadores.clientes`: `nivel` agrupa (el primer nivel sale más grande); `imagen` = logo opcional en `public/`; `url` opcional.
- `lugar.items[].icono`: `tren`, `bus`, `coche`, `avion` (o cualquiera de `src/components/ui/Icono.astro`).
- `contacto.motivos`: cadena separada por «;» con las opciones del desplegable (vacía = sin desplegable). `contacto.boton`: texto del botón del formulario.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml` (deja `hero` la primera).
3. **Cambiar textos, teléfonos, horarios, precios, fotos**: solo en `site.yaml`. Si un texto contiene comas o «: » dentro de `{ … }`, ponlo entre comillas. Precios siempre entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista (ni siquiera en `incluye` o `etiquetas`).
5. **No inventes** precios, cifras, ponentes, patrocinadores ni datos: si el cliente no los da, deja `precio: ""` o la lista vacía (`clientes: []`, `items: []`); el componente lo oculta.
6. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro`.
7. **Sección nueva**: mejor un id nuevo con `tipo:` (`texto`, `programa`, `entradas`…). Si hace falta un diseño nuevo, crea `src/components/secciones/<id>.astro` con `seccion(Astro.props.id)`, `Seccion` (con una clase de banda) y `Titular`. `src/pages/index.astro` la recoge sola.
8. **No tocar** `src/pages/index.astro`, `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
9. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real (solo hay el de la cabecera y el de las pestañas del programa), 16 px de margen lateral (`.contenedor`), sin scroll horizontal en móvil, ids `hero` y `contacto`. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altGaleria`, `altSeccion`, `altFicha` de `src/lib/seo.ts`, o el nombre de la persona o del patrocinador); las decorativas, `alt=""` (Imagen.astro les pone `aria-hidden`).
10. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

Fotos: `fotos.json` describe las fotos de `public/fotos/` (se generan aparte, sin caras reconocibles); los SVG de `public/placeholders/` quedan de respaldo.
