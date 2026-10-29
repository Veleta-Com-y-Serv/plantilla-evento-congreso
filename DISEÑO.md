# Evento y congreso: brief de diseño

Plantilla `evento-congreso` creada el 29/10/2026 a partir de `eventos-bodas` con `php artisan plantillas:nueva` y
rediseñada entera (tanda «ancho completo», fila 32 del brief). Este fichero se queda en el repo: es lo que lee quien
(persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: organizadores de congresos, jornadas profesionales, ferias, festivales y encuentros de un fin de
  semana (`evento, congreso, feria, festival, jornadas`). Quien entra quiere saber cuándo y dónde es, qué hay en el
  programa, quién habla y cuánto cuesta la entrada.
- **Qué tiene que conseguir la web**: que se inscriban (botón «Inscríbete» de la cabecera y fichas de entradas con su
  enlace a la venta o al formulario) y que escriban grupos, prensa y patrocinadores (formulario con motivo).
- **Tono y estilo** (`festivo`): vivo, gráfico, de cartel. Sí: el cartel de un congreso o de un festival de verano,
  la acreditación colgada del cuello, el panel de horarios de una sala. No: la caja centrada estrecha con tarjetas
  blancas, la serif romántica de `eventos-bodas`, la condensada nocturna de `musica-espectaculos`.
- **Concepto**: «cartel de congreso en bloques diagonales». Cada banda llega de borde a borde y muchas entran con un
  corte en diagonal (`.corte`, `clip-path`) que deja ver un triángulo de la anterior; la portada es un cartel con la
  fecha en cifras enormes dentro de un bloque rosa inclinado, el lugar al lado y una cinta cobalto inclinada con los
  temas; los botones, etiquetas y pestañas son paralelogramos; las horas y antetítulos van en monoespaciada como en
  una acreditación; las entradas son acreditaciones con su agujero y su cinta; los ponentes, un mosaico de bloques de
  color de borde a borde.
- **Paleta de ejemplo**: primario `#2b35e0` (cobalto: cifras, lugar, pie, entrada destacada), acento `#ff4d88` (rosa:
  botones, fecha, horas, llamada a la acción), fondo `#fff6e9` (crema), texto `#14123a` (tinta índigo). Derivados con
  `color-mix`: noche (texto + primario, bandas oscuras), violeta (primario + acento), crema rosada, cielo (fondo +
  primario), rosa legible sobre claro. Texto sobre rosa: tinta; sobre cobalto, noche y violeta: crema.
- **Tipografía** (del sistema, sin descargas): títulos en sans muy pesada (Segoe UI Variable Display / Segoe UI 900,
  SF Pro Display, Roboto) con interletrado −0,035 a −0,05 em, de 2,5-2,75 rem en móvil a 5,75-7,25 rem en escritorio;
  texto en system-ui; antetítulos, horas, rótulos y etiquetas en monoespaciada del sistema (Cascadia, SF Mono,
  Consolas) en mayúsculas con 0,12-0,14 em, con una línea inclinada de color delante del antetítulo.
- **Ritmo de bandas** (ejemplo): portada noche con foto a sangre a la derecha y cinta cobalto → cifras cobalto (corte)
  → el evento crema 50/50 con foto a sangre a la izquierda → programa noche (corte inverso) → ponentes crema + mosaico
  de colores a sangre → entradas cielo (corte) → galería noche con mosaico de borde a borde → lugar cobalto 50/50 con
  foto a sangre a la derecha → patrocinadores crema → preguntas crema rosada (corte inverso) → llamada a la acción rosa
  (corte) con bloque cobalto y la fecha hueca → contacto noche → pie cobalto (corte) con el nombre gigante.
- **Apartados** en orden:
  1. `hero`: `antetitulo`, `titulo`, `fecha` (las cifras del principio salen enormes: «15—17» + «de abril de 2027»),
     `lugar`, `texto`, `cta`, `cta_secundario`, `imagen`, `etiquetas` (cadena con «;» para la cinta).
  2. `cifras` (`items`: titulo = cifra, texto): banda cobalto, 2/4 columnas. Sin cifras no sale.
  3. `sobre` (`texto` en párrafos, `imagen`, `items` = ejes numerados, `cta`).
  4. `programa` (`programa: [{dia, hora, titulo, texto, ponente, sala, categoria}]`, `cta`): pestañas por día (sin
     JavaScript, todos los días seguidos), filas a todo el ancho, etiqueta de color por categoría.
  5. `ponentes` (`personas: [{nombre, cargo, foto, texto = su charla}]`): mosaico 2/3/4 columnas sin márgenes; la
     última ficha ocupa el hueco de su fila.
  6. `entradas` (`entradas: [{nombre, precio, texto, incluye, destacado, url}]`, `boton`, `nota`, `cta`).
  7. `galeria` (`galeria`, `cta`): mosaico de borde a borde.
  8. `lugar` (`texto`, `direccion`, `imagen`, `items` = cómo llegar con icono `tren|bus|coche|avion`, `cta`).
  9. `patrocinadores` (`clientes: [{nombre, nivel, imagen, url}]`, `cta`): celdas por nivel; el primero, más grandes.
  10. `preguntas` (`preguntas`): titular fijo a la izquierda y acordeón.
  11. `cta` (`antetitulo`, `titulo`, `texto`, `cta`, `cta_secundario`).
  12. `contacto` (`texto`, `motivos` con «;», `boton`): teléfono y correo enormes y formulario con entidad y motivo.
- **Fotos** (`fotos.json`, 11): nave portuaria convertida en sala de congresos para la portada, vestíbulo en la pausa,
  fachada de la nave junto al muelle, y ocho de la edición anterior (sala llena de espaldas, acreditaciones sin texto,
  mesa redonda, taller con notas, visita guiada de espaldas, degustación en la terraza, micrófono, vestíbulo). Sin
  texto legible, sin logotipos, sin personas reconocibles. Los ponentes llevan la silueta `/placeholders/persona.svg`.
- **Qué no hacer**: tarjetas blancas con sombra en una columna estrecha, esquinas redondeadas, serif, cursivas,
  degradados suaves, más colores que los cuatro de `site.yaml` y sus mezclas.

## Hecho

- [x] `site.yaml` de ejemplo (Jornadas Litoral, Tarragona), todo activo, al menos un elemento por lista, precios
  entre comillas, listas planas.
- [x] Secciones nuevas (`cifras`, `sobre`, `programa`, `ponentes`, `entradas`, `lugar`, `patrocinadores`, `cta`) y
  `hero`, `galeria`, `preguntas`, `contacto` y `texto` rediseñadas; `index.astro` sin tocar.
- [x] `template.yaml` con sectores `[{id, nombre}]`, secciones, estilo, orden y guion `asistente:` (11 pasos).
- [x] `fotos.json` (11) y placeholders (`hero.svg`, `foto.svg`, `persona.svg`).
- [x] `README.md`, `CLAUDE.md`, `aviso-legal.astro` y `404.astro` con el diseño.
- [ ] Fotos definitivas y previews con fotos: las genera el paso de fotos.
