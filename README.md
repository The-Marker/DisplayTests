**English** · [Español](README.es.md) · [Português](README.pt.md) · [Français](README.fr.md) · [Deutsch](README.de.md)

# DisplayTests

A website with tools to test and diagnose screens on phones, computers and televisions. It is a single file, `index.html`, with no dependencies and no build step.

## Usage

Open `index.html` in a browser (double-click) or publish it on any static host, for example GitHub Pages. Tap a thumbnail to open the test full screen.

To measure, set the screen brightness, use full screen and, for black tests, a dark room. The colors shown are an approximation.

## Highlights

**Test tools**

| Tool | Category | What it is for |
| --- | --- | --- |
| SMPTE bars | Color | Checking color, brightness and black levels |
| Color and grayscale scales | Color | Grayscale ramp and six ten-step color scales (red, green, blue, cyan, magenta and yellow). Use the Scale option to show all of them or just one |
| Low blacks | Color | Bars from 0 to 8 % on black to see whether the TV crushes shadows or lifts black (dark room) |
| Peak brightness | Color | White window from 10 to 100 % of the area on black, to measure peak brightness; SDR or HDR range. HDR needs a compatible browser and display, and the viewer explains how to enable it |
| Contrast | Color | Blocks from 5 % to 95 % with an adjustable level |
| Gray uniformity | Uniformity | Gray from 0 to 100 % with shortcuts to black and white: spots, vignetting, light leakage, clouding and banding |
| RGB and CMYK uniformity | Uniformity | One full-screen color at a time (red, green, blue, cyan, magenta, yellow, white and black), chosen by hand. Also useful for finding dead pixels |
| Touch counter | Touch | One numbered colored circle per touch point; the circles stay after release and are cleared when the screen is touched again. Counts simultaneous touches and the maximum |
| Swipe grid | Touch | Adjustable grid that paints the squares crossed by a finger or the mouse, with the percentage covered |
| Pixel unsticker | Pixels | Adaptive square grid whose squares change at random between RGB, CMYK, white and black, each on its own schedule; size (4–25 % of the width) and speed (1–16, from every 10 s to every 0.1 s) are adjustable |
| Local dimming | Motion | Stars of several sizes moving over black to detect halos and local dimming; speed, density and star size are adjustable |
| Ghosting and smearing | Motion | Choose a mode. Ghosting: a block crosses the screen to show trails from slow response (pass from 2 to 6 s). Smearing (VA): a white bar leaves a dark or light trail on VA panels; speed and background are adjustable |
| Moving text | Motion | Lines of text scrolling in opposite directions, horizontally or vertically, with uniform or varied sizes; compare sharpness paused and moving |
| Geometry | Sharpness | Grid, or calibration with a central box inside the circle that combines SMPTE bars, grayscale, RGB and CMYK scales, and contrast, and shows the screen's resolution, density and scale; with the diagonal entered it calculates ppi |
| Convergence | Sharpness | Red, green and blue grids with dots near the corners of each square; misalignment shows as colored edges or dots. For CRT and three-panel projectors; flat single-panel screens have factory convergence |
| Aspect ratio and overscan | Sharpness | Mode: circle and 4:3, 16:9, 21:9 and 32:9 frames, each touching the nearest screen edge and labeled; or Overscan, with frames at 0, 2, 5 and 10 % from the edges to see whether the image is cropped (mainly on TVs) |
| Square tiles | Sharpness | Checkerboard of squares; rectangular tiles reveal uneven scaling |
| Fine lines | Sharpness | One-real-pixel lines to detect scaling, blur and moiré |
| Text sharpness | Sharpness | Text in many sizes, serif, monospace and colored, on white and on black, to check sharpness on white-pixel screens (such as W-OLED) |

**Site**

- **Responsive:** 2 columns on phones, 3 on tablets, 4 on desktops, and 5 on TVs with larger text. Filters are a row of buttons on every screen size, as on phones. The header, the photosensitivity notice and the filters stay at the top while you scroll.
- **Full-screen viewer:** each test adapts to the screen's real aspect ratio. The controls are shown and hidden with `H` or a mouse click (on touch screens, a double tap), and they hide on their own after 5 seconds without input, so they do not contaminate uniformity tests. Moving the mouse does not show them.
- **Several inputs:** keyboard, mouse, touch screens, television remotes, gamepads and joysticks. The control hints in the viewer adapt to the input the site detects, and keys are shown inside a box so they stand out. See the Controls section.
- **Automatic theme:** follows the system's light or dark mode on Android, iPhone, Windows, macOS and Linux. With the system in dark mode it uses the gray dark theme, or pure black if you tick the option in the theme menu. If the device does not report it, it uses the light theme.
- **Theme menu:** a single icon in the header opens a menu with Automatic, Light, Dark and Pure black, and the icon reflects the state (half-filled circle, sun, moon or filled circle). Light, Dark and Pure black fix the theme and turn off system tracking. Below them, the checkbox **Use pure black in dark mode** makes the dark theme use pure black instead, the best choice for OLED screens. The preference is remembered in the browser.
- **Header:** a GitHub link, a button that turns automatic start of motion tests on or off (off by default, and the choice is remembered), and the theme and language menus.
- **Languages:** English, Spanish, Portuguese, French and German. The language is chosen automatically from the system language; if it is not supported or cannot be detected, English is used. The globe icon, to the left of the theme icon, lets you change it manually.
- **Category filters:** Color, Uniformity, Pixels, Motion, Sharpness and Touch.
- **Safety:** a photosensitivity notice, motion without flashes, and a pixel unsticker that starts paused, with random color changes that are independent for each square. From speed 13 (more than 3 changes per second) the grid has at least 8 columns and a warning is shown.

## Controls

The site detects the last input you used and changes the viewer hints accordingly.

| Action | Keyboard | Touch | TV remote | Gamepad or joystick |
| --- | --- | --- | --- | --- |
| Change test | `←` `→` | Swipe sideways, or Previous and Next buttons | `◀` `▶`, `CH+` `CH−` | `◀` `▶`, `LB` `RB` |
| Go to the controls | `↓` (and `↑` to go back) | Tap the control | `▼` (and `▲` to go back) | `▼` (and `▲` to go back) |
| Adjust a control | `←` `→` on a slider | Drag | `◀` `▶` | `◀` `▶` or left stick |
| Show or hide the panel | `H` | Click the screen (touch: double tap) | `OK` or `Info` | `Start` |
| Start or pause | `Space` | Start/Pause button between Previous and Next | `⏯` | `X` |
| Accept | `Enter` | Tap | `OK` | `A` |
| Close | `Esc` | Swipe down | `Back` | `B` |

In the Swipe grid test, swipes do not change the test or close the viewer, and tapping does not hide the panel, so you can paint freely. Use the Close button, `Esc` or `H` there.

On the home page, TV remotes and gamepads move between buttons, filters and thumbnails with the arrows (spatial navigation). On TVs running Tizen, webOS, Android TV, Fire TV and similar systems, the site starts with the TV remote hints. Gamepads are detected when you press any button.

## Compatibility

Current browsers on Android, iPhone, Windows, macOS and Linux, and smart-TV browsers with modern CSS and JavaScript support.

## Contributing

See [AGENTS.md](AGENTS.md) for the structure, conventions and how to add a new tool.

## License

GNU GPL v3. See [LICENSE](LICENSE).
