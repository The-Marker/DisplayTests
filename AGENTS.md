# AGENTS.md

Guía para agentes de IA y colaboradores que modifiquen este repositorio.

## Qué es

Sitio estático de una sola página para probar y diagnosticar pantallas (móvil, escritorio y TV). Todo vive en `index.html`: HTML, CSS y JavaScript sin dependencias, sin bundler y sin red.

## Estructura

- `index.html`: el sitio completo.
- `README.md`: descripción y funciones para usuarios.
- `LICENSE`: GPL v3.

Dentro de `index.html`, el script tiene estas partes: helpers, herramientas (`TOOLS`), cuadrícula y filtros, visor a pantalla completa, teclado, portada y tema automático.

## Ejecutar y probar

No hay build. Abre `index.html` en un navegador o sirve la carpeta con `python3 -m http.server`.

Antes de subir cambios, revisa como mínimo:

- No hay errores en la consola.
- Móvil (~390 px), escritorio (~1280 px) y TV (~1920 px) sin scroll horizontal.
- Tema claro, tema oscuro y tema automático. Con el tema automático desactivado, el tema fijo se mantiene.
- Un navegador sin `matchMedia` cae en tema claro.
- Cada herramienta abre a pantalla completa, sus controles responden y `Esc` la cierra.

Playwright con Chromium sirve para automatizar estas revisiones.

## Convenciones

- Un solo archivo, sin dependencias externas ni peticiones de red. Se debe poder abrir con doble clic.
- Texto de la interfaz en español, en minúsculas salvo nombres propios y siglas, y sin signos de exclamación.
- Colores y tema con variables CSS en `:root`. Nunca colores fijos en la interfaz; los patrones de prueba sí usan colores exactos, porque son el producto.
- El tema por defecto es claro. El modo automático depende de `prefers-color-scheme`, con `data-theme="light|dark"` en `<html>` solo cuando el usuario lo fija.
- Los patrones estáticos se dibujan en SVG con `viewBox` y reciben el ancho y alto (`W`, `H`) para adaptarse a la proporción real de la pantalla. La miniatura usa 160×90.
- Los patrones animados (`kind:"cv"`) se dibujan en `canvas` con `init` y `frame`, y su miniatura es un SVG estático (`thumb`).
- Accesibilidad: botones reales, `aria-pressed` en los selectores, foco visible, `aria-label` en miniaturas y respeto de `prefers-reduced-motion`.
- Persistencia con `localStorage` siempre dentro de `try/catch`; el sitio debe funcionar sin ella.
- Los iconos son SVG en línea con `currentColor`. No uses fuentes de iconos ni imágenes externas: el sitio es un solo archivo y debe verse igual abierto con doble clic.
- El tema se elige en un menú desplegable de un icono (`#themeBtn`, `#themeMenu`) con `role="menu"`, teclado (flechas, Esc) y el icono refleja el modo (auto, claro u oscuro).
- El pie de página fue eliminado a propósito. No lo repongas.

## Reglas de seguridad

- Sin destellos ni parpadeo automático. El movimiento es moderado y el aviso de fotosensibilidad debe seguir visible.
- La velocidad del ghosting se limita a 2–6 s por pasada. No bajes de 2 s.
- El desatascador de píxeles empieza en pausa. Cada cuadro cambia de color al azar y por su cuenta, con un intervalo medio que va de 10 s a 0,1 s (velocidades 1–16) y variación de ±40 %, y los cuadros se reprograman al mover la velocidad para que nunca cambien juntos. Por encima de 3 cambios por segundo (velocidad 13 o más) se fuerzan al menos 8 columnas, para que el parpadeo no se concentre en pocos cuadros, y la etiqueta marca "rápido". No quites ese límite ni subas la velocidad sin avisar al dueño del proyecto.
- Los controles del visor deben poder ocultarse, para no contaminar las pruebas de uniformidad.

## Añadir una herramienta

1. Agrega un objeto a `TOOLS` con `id`, `name`, `cat`, `desc`, `p` (parámetros por defecto), `ctl` (controles, opcional) y `draw(p, W, H, live)` que devuelve el SVG. Si es animada, usa `kind:"cv"` con `init`, `frame` y `thumb`.
2. Si es una categoría nueva, agrégala a `CATS`.
3. Los controles pueden ser `range` (`min`, `max`, `step`, `fmt`), `choice` (`opts`), `preset` (atajos a un valor) o `play` (iniciar y pausar).
4. Actualiza la tabla de herramientas del `README.md`.
5. Revisa el sitio con la lista de pruebas de arriba.

## Commits

Mensajes cortos en español o inglés, en imperativo, con una línea de resumen. Un cambio por commit cuando sea posible.
