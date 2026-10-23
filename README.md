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
| Escala RGB y CMYK | Color | 10 tonalidades por fila en rojo, verde, azul, cian, magenta, amarillo y negro (K) |
| Contraste | Color | Bloques de 5 % a 95 % con nivel ajustable |
| Uniformidad gris | Uniformidad | Gris de 0 a 100 % con atajos a negro y blanco: manchas, viñeteo, fuga de luz, nubosidad y bandas |
| Uniformidad RGB y CMYK | Uniformidad | Un color a pantalla completa a la vez (rojo, verde, azul, cian, magenta, amarillo, blanco y negro), elegido a mano. También sirve para buscar píxeles muertos |
| Desatascador de píxeles | Píxeles | Cuadrícula cuadrada adaptable cuyos cuadros cambian al azar entre RGB, CMYK, blanco y negro, cada uno por su cuenta y en momentos distintos; tamaño (4–25 % del ancho) y velocidad (1–16, de cada 10 s a cada 0,1 s) ajustables |
| Atenuación local | Movimiento | Estrellas de varios tamaños en movimiento sobre negro para detectar halos y atenuación local (local dimming); velocidad y densidad ajustables |
| Ghosting | Movimiento | Estelas por tiempo de respuesta lento; pasada de 2 a 6 s |
| Geometría | Nitidez | Cuadrícula, círculo y diagonales para proporciones y enfoque |
| Geometría y calibración | Nitidez | Lo mismo con un recuadro central dentro del círculo que reúne barras SMPTE, escala de grises, escala RGB y CMYK y contraste, y muestra resolución, densidad y escala de la pantalla; con la diagonal indicada calcula los ppp |

**Sitio**

- **Responsivo:** 2 columnas en móvil, 3 en tabletas, 4 en escritorio con filtros en barra lateral y 5 en televisores con texto más grande.
- **Visor a pantalla completa:** cada prueba se adapta a la proporción real de la pantalla. Los controles se ocultan con `H` o tocando la pantalla, para no contaminar las pruebas de uniformidad.
- **Varias entradas:** teclado, ratón, pantallas táctiles, controles remotos de televisión, gamepads y joysticks. Las pistas de controles del visor se adaptan a la entrada que detecta el sitio, y las teclas se muestran dentro de una caja para que resalten. Consulta la sección Controles.
- **Tema automático:** sigue el modo claro u oscuro del sistema en Android, iPhone, Windows, macOS y Linux. Si el dispositivo no lo informa, usa el tema claro.
- **Menú de tema:** un solo icono en el encabezado abre un menú con Automático, Claro y Oscuro, y el icono refleja el estado (círculo mitad lleno, sol o luna). Claro y Oscuro fijan el tema y desactivan el seguimiento del sistema. La preferencia se recuerda en el navegador.
- **Filtros por categoría:** Color, Uniformidad, Píxeles, Movimiento y Nitidez.
- **Seguridad:** aviso para personas fotosensibles, movimiento sin destellos y desatascador que empieza en pausa, con cambios de color al azar e independientes por cuadro. Desde la velocidad 13 (más de 3 cambios por segundo) la cuadrícula tiene al menos 8 columnas y se muestra un aviso.

## Controles

El sitio detecta la última entrada que usas y cambia las pistas del visor en consecuencia.

| Acción | Teclado | Táctil | Control remoto | Gamepad o joystick |
| --- | --- | --- | --- | --- |
| Cambiar de prueba | `←` `→` | Deslizar a los lados, o botones Anterior y Siguiente | `◀` `▶`, `CH+` `CH−` | `◀` `▶`, `LB` `RB` |
| Ir a los controles | `↓` (y `↑` para volver) | Tocar el control | `▼` (y `▲` para volver) | `▼` (y `▲` para volver) |
| Ajustar un control | `←` `→` en un deslizador | Arrastrar | `◀` `▶` | `◀` `▶` o stick izquierdo |
| Mostrar u ocultar el panel | `H` | Tocar la pantalla | `OK` o `Info` | `Start` |
| Iniciar o pausar | `Espacio` | Botón Iniciar | `⏯` | `X` |
| Aceptar | `Enter` | Tocar | `OK` | `A` |
| Cerrar | `Esc` | Deslizar hacia abajo | `Atrás` | `B` |

En la página principal, los controles remotos y los gamepads se mueven por botones, filtros y miniaturas con las flechas (navegación espacial). En televisores con Tizen, webOS, Android TV, Fire TV y similares, el sitio arranca con las pistas de control remoto. Los gamepads se detectan al pulsar cualquier botón.

## Compatibilidad

Navegadores actuales en Android, iPhone, Windows, macOS y Linux, y navegadores de televisores inteligentes con soporte moderno de CSS y JavaScript.

## Colaborar

Consulta [AGENTS.md](AGENTS.md) para la estructura, las convenciones y cómo añadir una herramienta nueva.

## Licencia

GNU GPL v3. Consulta [LICENSE](LICENSE).
