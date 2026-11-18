<div align="center">

<img src="screenshots/banner.svg" alt="Nebula Nova: a glass theme for Zen Browser" width="100%" />

[![Version](https://img.shields.io/badge/version-4.0.0-302b63?style=flat-square)](CHANGELOG.md)
[![Zen Browser](https://img.shields.io/badge/Zen-1.24-24243e?style=flat-square)](https://zen-browser.app/)
[![Sine](https://img.shields.io/badge/installs%20with-Sine-0f0c29?style=flat-square)](https://github.com/CosmoCreeper/Sine)
[![License](https://img.shields.io/github/license/ItsTatsuya/Nebula-Nova?style=flat-square)](LICENSE)

[Install](#install) · [Features](#features) · [Settings](#settings) · [Troubleshooting](#troubleshooting) · [Changelog](CHANGELOG.md)

</div>

Nebula Nova turns Zen's floating UI into frosted glass: the compact sidebar, URL bar, find bar and media player blur the page behind them instead of covering it. Everything is configurable from Sine's mod settings, with no CSS editing required.

![Nebula Nova in compact mode, with the glass sidebar showing a tab folder, open tabs and the media player](screenshots/base.png)

## Features

- **Real glass.** The compact sidebar, URL bar, find bar, library, Glance and split-view controls blur the page behind them. Blur strength, color boost and glass color are adjustable.
- **Works with transparent browsing.** With Transparent Zen or Zen Internet, the glass stays frosted instead of showing sharp page text through it.
- **Motion.** Tab switch and page loading animations, a dim-and-zoom effect behind the open URL bar, and hover glow on tabs.
- **Your look.** Separate light and dark colors, corner radius, UI font and weight, window button style, workspace and Essentials styling.
- **Media.** Optional artwork behind the media player and an animated sound indicator on tabs.
- **Accessible by default.** Reduced motion turns off the animations; reduced transparency and software rendering swap the glass for solid surfaces.

## Install

**Requirements:** [Zen Browser](https://zen-browser.app/) 1.24 or later and the [Sine](https://github.com/CosmoCreeper/Sine) mod manager.

1. Install Sine by following its [setup guide](https://github.com/CosmoCreeper/Sine).
2. In Zen, open **Settings → Cosine Mods** and install from this repository: `https://github.com/ItsTatsuya/Nebula-Nova`
3. Restart Zen so the styles and the core script load together.

To update, use Sine's update button, then restart Zen.

> [!NOTE]
> The Sine mod ID and folder are still `Nebula`, so installs and saved settings from Zen-Nebula carry over.

## Settings

Open **Settings → Cosine Mods → Nebula Nova → ⚙** to configure the theme. Settings are grouped by what they change:

| Group                | What you can change                                                           |
| -------------------- | ----------------------------------------------------------------------------- |
| **Appearance**       | Glass blur and color boost, corner radius, gaps and shadows, font, and colors |
| **Tabs and sidebar** | Hover and selected-tab glow, pinned tabs, folders, Essentials, workspaces     |
| **Toolbar**          | Window button style and side, address bar suggestions, bookmarks toolbar      |
| **Motion and media** | Tab, page loading and address bar animations, sound indicator, player artwork |

Colors stay hidden until you tick **Customize colors**. Sizes take CSS lengths such as `32px`. If a value is invalid, Nebula Nova uses the default and keeps what you typed.

The full list of settings, with their defaults, is in the [configuration reference](docs/configuration.md).

## Troubleshooting

<details>
<summary><b>The sidebar isn't blurred when it is always shown</b></summary>

Outside compact mode the sidebar sits beside the page, not over it, so there is nothing for it to blur. The glass still applies to floating UI such as the URL bar and find bar. To blur the desktop behind a transparent Zen window, use your system's compositor:

- **Windows 11:** [Mica For Everyone](https://github.com/MicaForEveryone/MicaForEveryone) with an Acrylic backdrop on `zen.exe`
- **KDE Plasma:** [Better Blur DX](https://github.com/xarblu/kwin-effects-better-blur-dx)
- **GNOME:** Blur My Shell's Application Blur

</details>

<details>
<summary><b>The glass turned solid</b></summary>

Windows turns on reduced transparency with Energy Saver, and Zen falls back to software rendering when hardware acceleration is unavailable. In both cases the theme switches to solid surfaces on purpose, since blur is either unwanted or cannot work.

</details>

<details>
<summary><b>A change didn't apply</b></summary>

Restart Zen after installing or updating the theme. **Blur menus and popups** also needs a restart. Other settings apply immediately.

</details>

<details>
<summary><b>The New Tab page looks different from the screenshot</b></summary>

The screenshot uses a custom start page and wallpaper. A start page extension such as [Bonjourr](https://addons.mozilla.org/firefox/addon/bonjourr-startpage/) is optional; Nebula Nova does not install or need one.

</details>

Still stuck? [Open an issue](https://github.com/ItsTatsuya/Nebula-Nova/issues) with your Zen version, OS, and a screenshot.

## Contributing

Pull requests are welcome. The project uses [Bun](https://bun.sh/):

```sh
bun install            # dev tools and the pre-commit hook
bun run check:config   # checks settings against the code and docs
bun run lint           # Prettier and Stylelint
```

Read the [configuration reference](docs/configuration.md) before adding a setting. For quick CSS experiments, see Zen's [live editing guide](https://docs.zen-browser.app/guides/live-editing).

## Credits

Forked from [Zen-Nebula](https://github.com/JustADumbPrsn/Zen-Nebula) by JustAdumbPrsn and maintained by [ItsTatsuya](https://github.com/ItsTatsuya). Inspired by [Natsumi Browser](https://github.com/greeeen-dev/natsumi-browser), [Lacuna](https://github.com/Tanay-Kar/Lacuna), [My Internet](https://github.com/sameerasw/my-internet), [Pineapple Fried](https://github.com/TheBigWazz/Pineapple-Fried), [Advanced Tab Groups](https://github.com/TFFC-Anoms12/Advanced-Tab-Groups) and [NoGaps](https://github.com/Comp-Tech-Guy/No-Gaps).

## License

[GPL-3.0](LICENSE). You are free to fork and adapt Nebula Nova; please credit the project when you share a derivative.
