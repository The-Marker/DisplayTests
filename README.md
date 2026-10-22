# DisplayTests

Sitio web con herramientas para probar y diagnosticar pantallas de móviles, computadoras y televisores. Es un único archivo, `index.html`, sin dependencias ni paso de compilación.

## Uso

Abre `index.html` en un navegador (doble clic) o publícalo en cualquier hosting estático, por ejemplo GitHub Pages. Toca una miniatura para abrir la prueba a pantalla completa.

Para medir, fija el brillo de la pantalla, usa pantalla completa y, en las pruebas de negro, un cuarto oscuro. Los colores mostrados son una aproximación.

## Funciones destacables

**Herramientas de prueba**

| Herramienta | Categoría | Para qué sirve |
| --- | --- | --- |
| SMPTE barras | Color | Revisar color, brillo y niveles de negro |
| Escala de grises | Color | Ver si se distinguen tonos oscuros y claros |
| Contraste | Color | Bloques de 5 % a 95 % con nivel ajustable |
| Blanco y Negro | Uniformidad | Manchas, viñeteo, fuga de luz y nubosidad |
| Gris ajustable | Uniformidad | Bandas y manchas en tonos medios, de 5 % a 95 % |
| RGB | Uniformidad | Uniformidad por canal de color |
| Píxeles muertos | Uniformidad | Color único con cambio manual, sin parpadeo automático |
| Ghosting | Movimiento | Estelas por tiempo de respuesta lento; pasada de 2 a 6 s |
| Geometría | Nitidez | Cuadrícula, círculo y diagonales para proporciones y enfoque |

**Sitio**

- **Responsivo:** 2 columnas en móvil, 3 en tabletas, 4 en escritorio con filtros en barra lateral y 5 en televisores con texto más grande.
- **Visor a pantalla completa:** cada prueba se adapta a la proporción real de la pantalla. Los controles se ocultan con `H` o tocando la pantalla, para no contaminar las pruebas de uniformidad.
- **Navegación con teclado y control remoto:** flechas para moverse entre miniaturas, `←` `→` para cambiar de prueba en el visor, `Esc` para salir, y foco siempre visible.
- **Tema automático:** sigue el modo claro u oscuro del sistema en Android, iPhone, Windows, macOS y Linux. Si el dispositivo no lo informa, usa el tema claro.
- **Cambio de tema desactivable:** los botones Claro y Oscuro fijan el tema y desactivan el seguimiento del sistema. La preferencia se recuerda en el navegador.
- **Filtros por categoría:** Color, Uniformidad, Movimiento y Nitidez.
- **Seguridad:** aviso para personas fotosensibles, movimiento sin destellos y animación desactivada con `prefers-reduced-motion`.

## Compatibilidad

Navegadores actuales en Android, iPhone, Windows, macOS y Linux, y navegadores de televisores inteligentes con soporte moderno de CSS y JavaScript.

## Colaborar

Consulta [AGENTS.md](AGENTS.md) para la estructura, las convenciones y cómo añadir una herramienta nueva.

## Licencia

GNU GPL v3. Consulta [LICENSE](LICENSE).
