# Nebula Nova configuration

Nebula Nova 4.0.0 is maintained by ItsTatsuya.

`preferences.json` is the source for labels, types, defaults and choices. The core script reads that same file at startup. `nebula/config.css` defines the visual tokens and fallback values for CSS-only use. Keep preference keys stable so installed users retain their choices.

## Standard

- Group settings by what they change, and keep every color in the Colors section: Appearance, Tabs and sidebar, Toolbar, and Motion and media. Put an emoji on each group and subsection heading for easy scanning.
- Order light/dark pairs light first and keep them adjacent. Hide controls that depend on another setting with a `-moz-pref()` rule in `nebula/content/mods-page.css` (the preset font, the custom font name, the artwork style, and the color rows behind **Customize colors**). Sine `conditions` are not used: Sine evaluates them before the row is in the dialog, so the row shows on first open. Hide OS-specific controls with `disabledOn`. Use small `text` notes only where a label cannot carry the caveat.
- Use one separator per related set of controls, sentence-style labels, explicit defaults and `12px 0` control margins.
- Dropdown values remain stable; numeric choices appear in numeric order.
- Use paired light/dark colors, CSS lengths for sizes, and percentages for saturation/grayscale.
- Add a consumer and update the audit whenever adding an option. Run `bun run check:config` and `bun run lint`.
- Settings corners follow [concentric radius geometry](https://interactively.info/article/perfect-nested-rounded-corners): keep the configured radius on cards, and add the section's `16px` padding plus `1px` border to its outer radius. Subtract the marketplace grid's extra `2px` inset from its card radius. Native joined rows subtract their border width; previews subtract their actual inset, clamped at zero. Independent controls, dialogs and surfaces with unequal or wide insets keep their own radius. Preserve native pane widths and spacing.
- Browser chrome corners use the scale in `nebula/config.css`. Surfaces such as tabs, cards, the URL bar, panels and the media player use `--nebula-border-radius`. Controls nested in a surface use `--nebula-radius-inner` (radius minus `4px`, at least `4px`). Containers that pad surfaces by `2px`, such as folders and split-view groups, use `--nebula-radius-outer`. Tiny badges use `--nebula-radius-small`. Do not write local offsets such as `calc(var(--nebula-border-radius) - 3px)`. The same file maps Firefox and Zen radius tokens onto this scale and sets `--zen-squircle-value: 1`, so native widgets follow the setting with round corners.

## Behavior and limits

- Custom fonts must be installed. Presets include system fallbacks. An empty or invalid custom family falls back to system UI.
- Invalid CSS inputs use the documented default without erasing the saved input. Changes to visual string preferences are also applied to Settings and the Bookmarks/History documents.
- Saved choices take precedence over startup defaults. The window-control placement and Essentials glow preferences belong to Zen (`zen.view.experimental-force-window-controls-left`, `zen.theme.essentials-favicon-bg`) and keep their native defaults.
- Website tint applies to browsers Zen marks transparent. Nebula does not enable transparent browsing itself.
- Pinned extension styling requires placing extensions beside the address bar as described in the README.
- Media artwork requires an active media session exposing artwork; the artwork style takes effect when media backgrounds are enabled.
- Bookmarks visibility options operate when the bookmarks toolbar is enabled in Zen. Compact mode with its toolbar hidden retains Zen’s native behavior to avoid competing hover panels.
- Reduced-motion mode takes precedence over animation options.
- Reduced transparency (Windows turns it on with Energy Saver) and Zen's software-rendering fallback replace the glass with opaque surfaces, since blur is either unwanted or cannot sample the page.

## Preference audit

All 51 fields have explicit typed defaults and consumers. The automated audit checks that each field has a code consumer outside comments and a row in this table, dropdown variants, metadata, saved-value preservation, runtime defaults and CSS variable registration. GPU blur and native widget appearance still require a live Zen visual check.

| Group            | Preference                                         | Default                        | Consumer                                                                                             |
| ---------------- | -------------------------------------------------- | ------------------------------ | ---------------------------------------------------------------------------------------------------- |
| Appearance       | `var-nebula-glass-blur`                            | `"32px"`                       | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `var-nebula-glass-saturation`                      | `"140%"`                       | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `nebula-blur-popups`                               | `true`                         | `js/nebula.uc.js` (sets `widget.windows.mica.popups`, read by `general-ui.css`)                      |
| Appearance       | `var-nebula-border-radius`                         | `"13px"`                       | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `nebula-nogaps-mod`                                | `false`                        | `nebula/modules/general-ui.css`                                                                      |
| Appearance       | `nebula-tabs-no-shadow`                            | `false`                        | `nebula/modules/general-ui.css`                                                                      |
| Appearance       | `nebula-ui-font`                                   | `"browser"`                    | `nebula/content/better-pdf.css`, `nebula/modules/ui-font.css`, `js/nebula.uc.js`                     |
| Appearance       | `nebula-ui-font-custom-enable`                     | `false`                        | `nebula/content/better-pdf.css`, `nebula/modules/ui-font.css`, `js/nebula.uc.js`                     |
| Appearance       | `nebula-ui-font-custom`                            | `""`                           | `nebula/modules/ui-font.css`, `js/nebula.uc.js`                                                      |
| Appearance       | `nebula-ui-font-weight`                            | `"400"`                        | `nebula/content/better-pdf.css`, `nebula/modules/ui-font.css`, `js/nebula.uc.js`                     |
| Appearance       | `nebula-show-color-settings`                       | `false`                        | `nebula/content/mods-page.css` (shows the color rows in the settings dialog)                         |
| Appearance       | `var-nebula-color-glass-light`                     | `"rgba(255, 255, 255, 0.4)"`   | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `var-nebula-color-glass-dark`                      | `"rgba(0, 0, 0, 0.4)"`         | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `var-nebula-ui-tint-light`                         | `"rgba(255, 255, 255, 0.2)"`   | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `var-nebula-ui-tint-dark`                          | `"rgba(0, 0, 0, 0.2)"`         | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `var-nebula-website-tint-light`                    | `"rgba(255, 255, 255, 0)"`     | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `var-nebula-website-tint-dark`                     | `"rgba(0, 0, 0, 0)"`           | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `var-nebula-color-shadow-light`                    | `"rgba(255, 255, 255, 0.055)"` | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `var-nebula-color-shadow-dark`                     | `"rgba(0, 0, 0, 0.55)"`        | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `var-nebula-tabs-default-light`                    | `"rgba(255, 255, 255, 0.25)"`  | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `var-nebula-tabs-default-dark`                     | `"rgba(0, 0, 0, 0.35)"`        | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `var-nebula-tabs-hover-light`                      | `"rgba(255, 255, 255, 0.35)"`  | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `var-nebula-tabs-hover-dark`                       | `"rgba(0, 0, 0, 0.45)"`        | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `var-nebula-tabs-selected-light`                   | `"rgba(255, 255, 255, 0.45)"`  | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `var-nebula-tabs-selected-dark`                    | `"rgba(0, 0, 0, 0.55)"`        | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `var-nebula-tabs-minimum-light`                    | `"rgba(255, 255, 255, 0.1)"`   | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Appearance       | `var-nebula-tabs-minimum-dark`                     | `"rgba(0, 0, 0, 0.2)"`         | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Tabs and sidebar | `nebula-glow-gradient`                             | `1`                            | `nebula/modules/pinned-extensions.css`, `nebula/modules/tab-styles.css`, `nebula/modules/urlbar.css` |
| Tabs and sidebar | `nebula-active-tab-glow`                           | `0`                            | `nebula/modules/tab-styles.css`, `js/nebula.uc.js`                                                   |
| Tabs and sidebar | `nebula-pinned-tabs-bg`                            | `false`                        | `nebula/modules/tab-folders.css`, `nebula/modules/tab-styles.css`                                    |
| Tabs and sidebar | `nebula-disable-container-styling`                 | `false`                        | `nebula/modules/tab-styles.css`                                                                      |
| Tabs and sidebar | `nebula-folder-styling`                            | `false`                        | `nebula/modules/tab-folders.css`                                                                     |
| Tabs and sidebar | `var-nebula-essentials-width`                      | `"60px"`                       | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Tabs and sidebar | `nebula-essentials-gray-icons`                     | `false`                        | `nebula/modules/essentials.css`                                                                      |
| Tabs and sidebar | `zen.theme.essentials-favicon-bg`                  | `true`                         | `nebula/modules/essentials.css`                                                                      |
| Tabs and sidebar | `nebula-workspace-style`                           | `1`                            | `nebula/modules/workspace-buttons.css`                                                               |
| Tabs and sidebar | `var-nebula-workspace-grayscale`                   | `"100%"`                       | `nebula/config.css`, `js/nebula.uc.js`                                                               |
| Tabs and sidebar | `nebula-remove-workspace-indicator`                | `false`                        | `nebula/modules/workspace-buttons.css`                                                               |
| Toolbar          | `nebula-macos-style-buttons`                       | `false`                        | `nebula/modules/topbar-buttons.css`                                                                  |
| Toolbar          | `zen.view.experimental-force-window-controls-left` | `false`                        | `nebula/modules/topbar-buttons.css`                                                                  |
| Toolbar          | `nebula-hide-search-suggestions`                   | `false`                        | `js/nebula.uc.js`                                                                                    |
| Toolbar          | `nebula-turn-off-zen-menu-icon`                    | `false`                        | `nebula/modules/topbar-buttons.css`                                                                  |
| Toolbar          | `nebula-pinned-extensions-mod`                     | `false`                        | `nebula/modules/pinned-extensions.css`                                                               |
| Toolbar          | `nebula-bookmarks-autohide`                        | `0`                            | `nebula/modules/sidebar.css`                                                                         |
| Motion and media | `nebula-tab-switch-animation`                      | `1`                            | `nebula/modules/tab-animations.css`                                                                  |
| Motion and media | `nebula-tab-loading-animation`                     | `1`                            | `nebula/modules/tab-animations.css`                                                                  |
| Motion and media | `nebula-urlbar-animation`                          | `1`                            | `nebula/modules/urlbar.css`                                                                          |
| Motion and media | `nebula-disable-menu-animations`                   | `false`                        | `nebula/modules/general-ui.css`, `js/nebula.uc.js`                                                   |
| Motion and media | `nebula-default-sound-style`                       | `1`                            | `nebula/modules/sound-icon.css`                                                                      |
| Motion and media | `nebula-media-background-enabled`                  | `false`                        | `js/nebula.uc.js`                                                                                    |
| Motion and media | `nebula-media-background-style`                    | `"blur"`                       | `nebula/modules/miniplayer.css`, `js/nebula.uc.js`                                                   |

## Advanced `about:config` options

These options have no Sine control. Set them as booleans in `about:config`; they are not part of the preference audit above. `nebula/modules/better-pip.css` reads the Picture-in-Picture options and `nebula/content/better-pdf.css` reads the PDF viewer options, which keep the names of the Natsumi PDF styles they came from. `bun run check:config` fails if CSS reads a `nebula` preference that is in neither table.

| Preference                              | Effect                                                                             |
| --------------------------------------- | ---------------------------------------------------------------------------------- |
| `nebula.pip.disabled`                   | Turns off Nebula's Picture-in-Picture styling entirely.                            |
| `nebula.pip.rounded`                    | Rounds the Picture-in-Picture window corners on Windows and macOS (not Linux).     |
| `nebula.pip.tinted-haze`                | Tints the haze background and controls with the primary color.                     |
| `nebula.pip.native-border-radius`       | Keeps the native window radius and tightens the control margins on narrow windows. |
| `nebula.theme.force-dark-shadows`       | Darkens the Picture-in-Picture control shadow color toward black.                  |
| `natsumi.pdfjs.compact`                 | Hides the PDF viewer toolbar until it is hovered or focused.                       |
| `natsumi.pdfjs.compact-dynamic`         | With the compact toolbar, keeps it open while the PDF sidebar is open.             |
| `natsumi.global.highlight-accent-color` | Colors text selection in the PDF viewer with the accent color.                     |

## Glass and blur reference

Since Zen 1.24 the compact sidebar's acrylic is painted on its background layer (`.zen-toolbar-background`), so Nebula puts its blur there and keeps `#titlebar` free of filters. A filter on `#titlebar` made it a backdrop root, which left nested glass such as the downloads preview nothing to sample. Nothing inside the sidebar may use `mix-blend-mode`: Gecko then renders the sidebar offscreen and the blur can no longer see the page. Content browsers get the layering hint (`translate: 0; backface-visibility: hidden`) from `nebula/modules/general-ui.css` so chrome blur can sample web content.

The find bar, the open URL bar and the Glance and split-view controls are real glass with no opaque backing. The open URL bar uses one blur, on `.urlbar-background`, replacing Zen's own acrylic there.

When `browser.tabs.allow_transparent_browser` is on (as with the Transparent Zen mod or the Zen Internet add-on), pages can be see-through, which would leave the sidebar glass showing sharp page text. In that mode every chrome glass surface over the page (sidebar, library panel, downloads preview, open URL bar, find bar, Glance buttons and split-view header) uses an SVG filter that adds an opaque floor under the blur, because Gecko skips CSS filter functions after a `url()` filter. Over opaque pages it looks the same as the plain blur. `js/nebula.uc.js` generates that filter from the glass blur and saturation settings; `nebula/filters/glass-underlay.svg` (32px, 140%) is the fallback when the script is not running or the blur is not in `px`.
