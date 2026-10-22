# AGENTS.md

Guía para agentes de IA y colaboradores que modifiquen este repositorio.

## Qué es

Sitio estático de una sola página para probar y diagnosticar pantallas (móvil, escritorio y TV). Todo vive en `index.html`: HTML, CSS y JavaScript sin dependencias, sin bundler y sin red.

## Estructura

- `index.html`: el sitio completo.
- `README.md`: descripción y funciones para usuarios.
- `LICENSE`: GPL v3.

Dentro de `index.html`, el script tiene estas partes: helpers, herramientas (`TOOLS`), cuadrícula y filtros, visor a pantalla completa, teclado, portada, tema automático y efectos (fuego y ERROR).

## Ejecutar y probar

No hay build. Abre `index.html` en un navegador o sirve la carpeta con `python3 -m http.server`.

Antes de subir cambios, revisa como mínimo:

- No hay errores en la consola.
- Móvil (~390 px), escritorio (~1280 px) y TV (~1920 px) sin scroll horizontal.
- Tema claro, tema oscuro y tema automático. Con el tema automático desactivado, el tema fijo se mantiene.
- Un navegador sin `matchMedia` cae en tema claro.
- Cada herramienta abre a pantalla completa, sus controles responden y `Esc` la cierra.
- Los efectos (fuego y ERROR) se mueven en la página. Con el visor abierto, ERROR sigue rebotando por encima y el fuego se pausa.
- Con `prefers-reduced-motion: reduce`, los efectos quedan apagados.

Playwright con Chromium sirve para automatizar estas revisiones.

## Convenciones

- Un solo archivo, sin dependencias externas ni peticiones de red. Se debe poder abrir con doble clic.
- Texto de la interfaz en español, en minúsculas salvo nombres propios y siglas, y sin signos de exclamación.
- Colores y tema con variables CSS en `:root`. Nunca colores fijos en la interfaz; los patrones de prueba y los efectos sí usan colores exactos, porque son el producto o la decoración.
- El tema por defecto es claro. El modo automático depende de `prefers-color-scheme`, con `data-theme="light|dark"` en `<html>` solo cuando el usuario lo fija.
- Los patrones estáticos se dibujan en SVG con `viewBox` y reciben el ancho y alto (`W`, `H`) para adaptarse a la proporción real de la pantalla. La miniatura usa 160×90.
- Los patrones animados (`kind:"cv"`) se dibujan en `canvas` con `init` y `frame`, y su miniatura es un SVG estático (`thumb`).
- Accesibilidad: botones reales, `aria-pressed` en los selectores, foco visible, `aria-label` en miniaturas y respeto de `prefers-reduced-motion`.
- Persistencia con `localStorage` siempre dentro de `try/catch`; el sitio debe funcionar sin ella.
- Los efectos de fondo (fuego y ERROR) están siempre activos, sin opción en la interfaz para apagarlos. La única forma de apagarlos es la preferencia del sistema `prefers-reduced-motion`. No añadas un interruptor sin que lo pidan.
- El pie de página fue eliminado a propósito. No lo repongas.

## Reglas de seguridad

- Sin destellos ni parpadeo automático. El movimiento es moderado y el aviso de fotosensibilidad debe seguir visible.
- La velocidad del ghosting se limita a 2–6 s por pasada. No bajes de 2 s.
- El desatascador de píxeles empieza en pausa, no cambia de color más rápido que cada 0,5 s y desfasa los cuadros para que la pantalla no parpadee completa. Mantén ese límite.
- El fuego queda detrás del visor y se pausa al abrirlo. ERROR se dibuja por encima del visor a propósito (decisión del dueño del proyecto), así que puede contaminar las pruebas de uniformidad; no lo escondas sin que lo pidan.
- Los controles del visor deben poder ocultarse, para no contaminar las pruebas de uniformidad.

## Añadir una herramienta

1. Agrega un objeto a `TOOLS` con `id`, `name`, `cat`, `desc`, `p` (parámetros por defecto), `ctl` (controles, opcional) y `draw(p, W, H, live)` que devuelve el SVG. Si es animada, usa `kind:"cv"` con `init`, `frame` y `thumb`.
2. Si es una categoría nueva, agrégala a `CATS`.
3. Los controles pueden ser `range` (`min`, `max`, `step`, `fmt`), `choice` (`opts`), `preset` (atajos a un valor) o `play` (iniciar y pausar).
4. Actualiza la tabla de herramientas del `README.md`.
5. Revisa el sitio con la lista de pruebas de arriba.

## Commits

Mensajes cortos en español o inglés, en imperativo, con una línea de resumen. Un cambio por commit cuando sea posible.
