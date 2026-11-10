[English](README.md) · **Español** · [Português](README.pt.md) · [Français](README.fr.md) · [Deutsch](README.de.md)

# DisplayTests

Sitio web con herramientas para probar y diagnosticar pantallas de móviles, computadoras y televisores. Es un único archivo, `index.html`, sin dependencias ni paso de compilación.

## Uso

Abre `index.html` en un navegador (doble clic) o publícalo en cualquier hosting estático, por ejemplo GitHub Pages. Toca una miniatura para abrir la prueba a pantalla completa.

Para medir, fija el brillo de la pantalla, usa pantalla completa y, en las pruebas de negro, un cuarto oscuro. Los colores mostrados son una aproximación.

## Funciones destacables

**Herramientas de prueba**

| Herramienta | Categoría | Para qué sirve |
| --- | --- | --- |
| Barras SMPTE | Color | Revisar color, brillo y niveles de negro |
| Escalas de color y grises | Color | Escala de grises y seis escalas de color de diez pasos (rojo, verde, azul, cian, magenta y amarillo). Usa la opción Escala para verlas todas o una sola |
| Negros bajos | Color | Barras de 0 a 8 % sobre negro para ver si el televisor aplasta las sombras o levanta el negro (cuarto oscuro) |
| Pico de brillo | Color | Ventana blanca de 10 a 100 % del área sobre negro para medir el pico de brillo; rango SDR o HDR. HDR necesita navegador y pantalla compatibles, y el visor explica cómo activarlo |
| Contraste | Color | Bloques de 5 % a 95 % con nivel ajustable |
| Uniformidad gris | Uniformidad | Gris de 0 a 100 % con atajos a negro y blanco: manchas, viñeteo, fugas de luz, nubosidad y bandas |
| Uniformidad RGB y CMYK | Uniformidad | Un color a pantalla completa a la vez (rojo, verde, azul, cian, magenta, amarillo, blanco y negro), elegido a mano. Sirve también para buscar píxeles muertos |
| Contador de toques | Táctil | Un círculo numerado y de color por punto de contacto; los círculos se mantienen al soltar y se borran al volver a tocar la pantalla. Cuenta los toques simultáneos y el máximo |
| Cuadrícula de deslizamiento | Táctil | Cuadrícula ajustable que pinta los cuadros que cruza el dedo o el ratón, con el porcentaje cubierto |
| Desatascador de píxeles | Píxeles | Cuadrícula adaptativa de cuadros que cambian al azar entre RGB, CMYK, blanco y negro, cada uno con su propio ritmo; tamaño (4–25 % del ancho) y velocidad (1–16, de cada 10 s a cada 0,1 s) ajustables |
| Atenuación local | Movimiento | Estrellas de varios tamaños en movimiento sobre negro para detectar halos y atenuación local; velocidad, densidad y tamaño de estrellas ajustables |
| Ghosting y smearing | Movimiento | Elige un modo. Ghosting: un bloque cruza la pantalla para mostrar estelas por respuesta lenta (pasada de 2 a 6 s). Smearing (VA): una barra blanca deja una estela oscura o clara en paneles VA; velocidad y fondo ajustables |
| Texto en movimiento | Movimiento | Líneas de texto que se desplazan en direcciones opuestas, en horizontal o en vertical, con tamaño uniforme o variado; compara la nitidez en pausa y en movimiento |
| Geometría | Nitidez | Cuadrícula, o calibración con un recuadro central dentro del círculo que reúne barras SMPTE, escalas de grises, RGB y CMYK, y contraste, y muestra resolución, densidad y escala de la pantalla; con la diagonal indicada calcula los ppp |
| Convergencia | Nitidez | Rejillas roja, verde y azul, con puntos en las esquinas de cada cuadro; el desajuste se ve como bordes o puntos de color. Para tubos CRT y proyectores de tres paneles; en pantallas planas de un solo panel la convergencia viene de fábrica |
| Relación de aspecto y overscan | Nitidez | Modo: círculo y marcos de 4:3, 16:9, 21:9 y 32:9, cada uno tocando el borde más cercano y con su nombre; o Overscan, con recuadros a 0, 2, 5 y 10 % de los bordes para ver si la imagen se recorta (sobre todo en televisores) |
| Cuadros cuadrados | Nitidez | Tablero de cuadros; si salen rectangulares, el escalado es desigual |
| Líneas finas | Nitidez | Líneas de un píxel real para detectar escalado, borrosidad y moiré |
| Nitidez de texto | Nitidez | Texto en muchos tamaños, con serif, monoespaciado y en color, sobre blanco y sobre negro, para revisar la nitidez en pantallas de píxel blanco (como W-OLED) |

**Sitio**

- **Responsivo:** 2 columnas en móvil, 3 en tabletas, 4 en escritorio y 5 en televisores con texto más grande. Los filtros son una fila de botones en cualquier tamaño, como en móvil. El encabezado, el aviso de fotosensibilidad y los filtros se quedan arriba al desplazarte.
- **Visor a pantalla completa:** cada prueba se adapta a la proporción real de la pantalla. Los controles se muestran y ocultan con `H` o un clic del ratón (en pantallas táctiles, con doble toque), y también se ocultan solos tras 5 segundos sin uso, para no contaminar las pruebas de uniformidad. Mover el ratón no los muestra.
- **Varias entradas:** teclado, ratón, pantallas táctiles, controles remotos de televisión, gamepads y joysticks. Las pistas de controles del visor se adaptan a la entrada que detecta el sitio, y las teclas se muestran dentro de una caja para que resalten. Consulta la sección Controles.
- **Tema automático:** sigue el modo claro u oscuro del sistema en Android, iPhone, Windows, macOS y Linux. Con el sistema en oscuro usa el tema oscuro gris, o negro puro si marcas la opción del menú de tema. Si el dispositivo no lo informa, usa el tema claro.
- **Menú de tema:** un solo icono en el encabezado abre un menú con Automático, Claro, Oscuro y Negro puro, y el icono refleja el estado. Claro, Oscuro y Negro puro fijan el tema y desactivan el seguimiento del sistema. Debajo, la casilla **Usar negro puro en modo oscuro** hace que el tema oscuro use negro puro, lo mejor para pantallas OLED. La preferencia se recuerda en el navegador.
- **Encabezado:** enlace a GitHub, un botón que activa o desactiva el inicio automático de las pruebas de movimiento (desactivado por defecto; la elección se recuerda) y los menús de tema e idioma.
- **Idiomas:** inglés, español, portugués, francés y alemán. Se elige automáticamente según el idioma del sistema; si no es compatible o no se puede detectar, usa inglés. El icono de globo, a la izquierda del tema, permite cambiarlo a mano.
- **Filtros por categoría:** Color, Uniformidad, Píxeles, Movimiento, Nitidez y Táctil.
- **Seguridad:** aviso para personas fotosensibles, movimiento sin destellos y desatascador que empieza en pausa, con cambios de color al azar e independientes por cuadro. Desde la velocidad 13 (más de 3 cambios por segundo) la cuadrícula tiene al menos 8 columnas y se muestra un aviso.

## Controles

El sitio detecta la última entrada que usas y cambia las pistas del visor en consecuencia.

| Acción | Teclado | Táctil | Control remoto | Gamepad o joystick |
| --- | --- | --- | --- | --- |
| Cambiar de prueba | `←` `→` | Deslizar a los lados, o botones Anterior y Siguiente | `◀` `▶`, `CH+` `CH−` | `◀` `▶`, `LB` `RB` |
| Ir a los controles | `↓` (y `↑` para volver) | Tocar el control | `▼` (y `▲` para volver) | `▼` (y `▲` para volver) |
| Ajustar un control | `←` `→` en un deslizador | Arrastrar | `◀` `▶` | `◀` `▶` o stick izquierdo |
| Mostrar u ocultar el panel | `H` | Clic en la pantalla (táctil: doble toque) | `OK` o `Info` | `Start` |
| Iniciar o pausar | `Espacio` | Botón Pausar/Iniciar entre Anterior y Siguiente | `⏯` | `X` |
| Aceptar | `Enter` | Tocar | `OK` | `A` |
| Cerrar | `Esc` | Deslizar hacia abajo | `Atrás` | `B` |

En la prueba de cuadrícula de deslizamiento, los gestos no cambian de prueba ni cierran el visor, y tocar no oculta el panel, para poder pintar libremente. Usa el botón Cerrar, `Esc` o `H` en esa prueba.

En la página principal, los controles remotos y los gamepads se mueven por botones, filtros y miniaturas con las flechas (navegación espacial). En televisores con Tizen, webOS, Android TV, Fire TV y similares, el sitio arranca con las pistas de control remoto. Los gamepads se detectan al pulsar cualquier botón.

## Compatibilidad

Navegadores actuales en Android, iPhone, Windows, macOS y Linux, y navegadores de televisores inteligentes con soporte moderno de CSS y JavaScript.

## Colaborar

Consulta [AGENTS.es.md](AGENTS.es.md) para la estructura, las convenciones y cómo añadir una herramienta nueva.

## Licencia

GNU GPL v3. Consulta [LICENSE](LICENSE).
