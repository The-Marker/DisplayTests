# AGENTS.md

Guía para agentes de IA y colaboradores que modifiquen este repositorio.

## Qué es

Sitio estático de una sola página para probar y diagnosticar pantallas (móvil, escritorio y TV). Todo vive en `index.html`: HTML, CSS y JavaScript sin dependencias, sin bundler y sin red.

## Estructura

- `index.html`: el sitio completo.
- `README.md`: descripción y funciones para usuarios.
- `LICENSE`: GPL v3.

Dentro de `index.html`, el script está dividido en secciones comentadas: helpers, herramientas (`TOOLS`), cuadrícula y filtros, visor a pantalla completa, teclado, portada y tema automático.

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
- Todo patrón se dibuja en SVG con `viewBox` y recibe el ancho y alto (`W`, `H`) para adaptarse a la proporción real de la pantalla. La miniatura usa 160×90.
- Accesibilidad: botones reales, `aria-pressed` en los selectores, foco visible, `aria-label` en miniaturas y respeto de `prefers-reduced-motion`.
- Persistencia con `localStorage` siempre dentro de `try/catch`; el sitio debe funcionar sin ella.

## Reglas de seguridad

- Sin destellos ni parpadeo automático. El movimiento es moderado y el aviso de fotosensibilidad debe seguir visible.
- La velocidad del ghosting se limita a 2–6 s por pasada. No bajes de 2 s.
- Los controles del visor deben poder ocultarse, para no contaminar las pruebas de uniformidad.

## Añadir una herramienta

1. Agrega un objeto a `TOOLS` con `id`, `name`, `cat`, `desc`, `p` (parámetros por defecto), `ctl` (controles, vacío si no hay) y `draw(p, W, H, live)` que devuelve el SVG.
2. Si es una categoría nueva, agrégala a `CATS`.
3. Los controles pueden ser `range` (`min`, `max`, `step`, `fmt`) o `choice` (`opts`).
4. Actualiza la tabla de herramientas del `README.md`.
5. Revisa el sitio con la lista de pruebas de arriba.

## Commits

Mensajes cortos en español o inglés, en imperativo, con una línea de resumen. Un cambio por commit cuando sea posible.
