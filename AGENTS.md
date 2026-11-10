**English** · [Español](AGENTS.es.md) · [Português](AGENTS.pt.md) · [Français](AGENTS.fr.md) · [Deutsch](AGENTS.de.md)

# AGENTS.md

Guide for AI agents and contributors who modify this repository.

## What it is

A static, single-page site for testing and diagnosing screens (phone, desktop and TV). Everything lives in `index.html`: HTML, CSS and JavaScript with no dependencies, no bundler and no network requests.

## Structure

- `index.html`: the whole site.
- `README.md` (and `README.es.md`, `README.pt.md`, `README.fr.md`, `README.de.md`): description and features for users.
- `AGENTS.md` (and `AGENTS.es.md`, `AGENTS.pt.md`, `AGENTS.fr.md`, `AGENTS.de.md`): guide for contributors. Keep all language versions in sync when you change one.
- `LICENSE`: GPL v3.

Inside `index.html`, the script has these parts: helpers, language core (`DICT`, `tr`, `applyLang`), tools (`TOOLS`), grid and filters, full-screen viewer, keyboard and input, home page, theme and language menus, favicon and startup.

## Running and testing

There is no build. Open `index.html` in a browser or serve the folder with `python3 -m http.server`.

Before pushing changes, check at least:

- No errors in the console.
- Phone (~390 px), desktop (~1280 px) and TV (~1920 px) with no horizontal scroll.
- Light, dark, pure black and automatic themes. With automatic off, the fixed theme stays.
- A browser without `matchMedia` falls back to the light theme.
- Each tool opens full screen, its controls respond and `Esc` closes it.
- Geometry, calibration mode: the box is centered inside the circle on phone, desktop and TV, and shows resolution, density and scale (with `H` hiding the panel so you can read it).
- Languages: with the system in an unsupported language the site uses English; the menu lists English first, then the system language, then the rest; the choice persists after a reload.
- Inputs work and hints change: keyboard, touch (swipe), TV remote (`ChannelUp`, `Info`, `GoBack`, and keyCode-only events 37–40/13 with a TV user agent), gamepad (simulate by replacing `navigator.getGamepads`).
- Swipe grid: dragging paints squares and does not change test or close the viewer.

Playwright with Chromium is useful to automate these checks.

## Conventions

- One file, no external dependencies, no network requests. It must open with a double click.
- Interface text goes through `tr(text)`. The key is the Spanish text, in lowercase except proper nouns and acronyms, with no exclamation marks. Translations live in `DICT` (one table per language). A missing translation shows the Spanish text. To add a language: add it to `SUP`, `NATIVE` and `DICT` with every key, and add a README and AGENTS translation.
- Colors and theme use CSS variables in `:root`. Never hard-code colors in the interface; test patterns do use exact colors because they are the product.
- Themes: light, dark (gray), pure black (`data-theme="black"`, background #000) and automatic. Automatic with a dark system uses the gray dark theme. The checkbox **Use pure black in dark mode** in the theme menu swaps dark for pure black (`dt-oled` in `localStorage`); there is no web API to detect OLED, so the user decides.
- The default theme is light. Automatic depends on `prefers-color-scheme`, with `data-theme="light|dark|black"` on `<html>` only when the user sets it.
- Static patterns are drawn as SVG with `viewBox` and receive the width and height (`W`, `H`) so they fit the screen's real aspect ratio. The thumbnail uses 160×90.
- Animated patterns (`kind:"cv"`) are drawn on a `canvas` with `init` and `frame`, and their thumbnail is a static SVG (`thumb`).
- Accessibility: real buttons, `aria-pressed` on selectors, visible focus, `aria-label` on thumbnails, and respect for `prefers-reduced-motion`.
- Persistence with `localStorage` always inside `try/catch`; the site must work without it. It stores the theme (`dt-theme`) and the language (`dt-lang`, `auto` or a code).
- Language: automatic follows `navigator.languages`, with English as fallback. Static elements use `data-i18n`, `data-i18n-aria` and `data-i18n-title`. Changing language calls `applyLang()`.
- Icons are inline SVG with `currentColor`. Do not use icon fonts or external images: the site is one file and must look the same when opened with a double click.
- The theme is chosen in a dropdown menu from one icon (`#themeBtn`, `#themeMenu`) with `role="menu"`, keyboard support (arrows, Esc), and the icon reflects the mode. The language menu (`#langBtn`, `#langMenu`) works the same way.
- The footer was removed on purpose. Do not put it back.
- Touch tests: the touch counter creates one circle per point and clears the old ones when the screen is touched again; the swipe grid paints the squares crossed by a finger or the mouse. In the swipe grid, swipe gestures (navigate, close) and tap-to-toggle-panel are disabled on purpose.
- Peak brightness: HDR mode uses `color(rec2100-pq 1 1 1)` only if `CSS.supports` accepts it; otherwise it shows a notice and SDR white. A tool's `help` field (here `HDR_HELP`) is shown in a collapsible section in the viewer (`#vhelp`).
- `colorScale(x,y,w,h,noGray)` draws the color rows; with `noGray` it omits the gray band. The RGB and CMYK test has a `Scale` selector that uses `ramp1` to show one scale.
- Play/pause: the play button lives in the `#vnav` row between Previous and Next (class `playbtn`), not in the controls panel. `clickPlay()` finds it there.
- The header has no category navigation; the filters are a row of buttons above the grid on every screen size, with no sidebar. Do not add it back.
- Auto-start: `AUTO` (`dt-auto` in `localStorage`) decides whether tests in the Motion category start playing (`showTool` sets `p.play`). The pixel unsticker is excluded and always starts paused.
- Viewer panel: `kick()` hides `#vc` after 5 s without input, except in the swipe grid. Any key or mouse movement shows it again.
- Conditional controls: a control with `when:{k,v}` appears only when `p[k]===v`. A choice with `rb:true` rebuilds the panel when it changes, which is how modes work.
- Shared pattern helpers: `smpteSvg`, `grayStrip`, `colorScale`, `contrastSvg`, `geoBase`, `screenInfo`, `starCount` and `newStar`. Reuse them instead of duplicating drawing code.
- All inputs (keyboard, mouse, touch, TV remote, gamepad and joystick) go through the dispatcher `act(action, native)`, with actions `left`, `right`, `up`, `down`, `confirm`, `back`, `next`, `prev`, `toggle` and `playpause`. To support a new device, map it to those actions; do not add loose handlers.
- `INPUT` stores the last detected input (`keyboard`, `mouse`, `touch`, `remote`, `gamepad`) and is reflected in `data-input` on `<html>`. The viewer hints (`hintHtml`) depend on it. If you add an action, add its hint for every input.
- TV remote keys: `keyAction` accepts the name (`ArrowLeft` or `Left`) and the numeric code (37–40, 13). Some TVs only send the code; do not remove that fallback.
- Photosensitivity notice: the general one sits above the grid. Motion or color-change tests have a `warn` and show it in the viewer (`#vwarn`) with the same `.warn` class as the home page.
- Viewer buttons (`#vc .btn`), the play button and selected buttons use the slider blue `#85b7eb` with black text (other viewer buttons are white with black text). Key hints (`kbd`) are white with black text and flat, with no bottom relief.
- Favicon: a monitor icon like the header one. `setFav()` regenerates it as a `data:` URI according to `prefers-color-scheme` (black in light, white in dark) and updates when the system changes. Do not use `media` on icon links: browsers do not apply it reliably.
- Keys in hints are written with `<kbd>` (classes `r` for remote and `g` for gamepad) so they show inside a box.
- Spatial navigation (`spatial`) only runs with focus on an element (keyboard and mouse) or always (TV remote and gamepad), so keyboard users keep arrow scrolling.

## Safety rules

- No flashes or automatic flicker. Motion stays moderate and the photosensitivity notice must stay visible.
- Ghosting speed is limited to 2–6 s per pass. Do not go below 2 s.
- The pixel unsticker starts paused. Each square changes color at random and on its own, with an average interval from 10 s to 0.1 s (speeds 1–16) and ±40 % variation; squares are rescheduled when the speed changes so they never change together. Above 3 changes per second (speed 13 or more) it forces at least 8 columns so flicker is not concentrated in a few squares, and the label says "fast". Do not remove that limit or raise the speed without telling the project owner.
- The ghosting and smearing test (`respuesta`) starts paused and shows the photosensitivity notice.
- Viewer controls must be hideable, so they do not contaminate uniformity tests.

## Adding a tool

1. Add an object to `TOOLS` with `id`, `name`, `cat`, `desc`, `p` (default parameters), `ctl` (optional controls) and `draw(p, W, H, live)` that returns the SVG. If it is animated, use `kind:"cv"` with `init`, `frame` and `thumb`.
2. If it is a new category, add it to `CATS`.
3. Controls can be `range` (`min`, `max`, `step`, `fmt`), `choice` (`opts`), `preset` (shortcuts to a value) or `play` (start and pause).
4. Add every visible Spanish string to every language in `DICT`, and update the tool table in `README.md` and its translations.
5. Check the site with the test list above.

## Commits

Short messages in English or Spanish, in the imperative, with a one-line summary. One change per commit when possible.
