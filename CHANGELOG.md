# Changelog

All notable changes to Nebula Nova are listed here.

## 4.0.0

Built for Zen 1.24.

- Glass follows Zen 1.24's new rendering path, so the compact sidebar, URL bar and library blur the page again.
- The find bar and the open URL bar are now see-through glass instead of solid panels.
- Glance and split-view buttons get dark glass.
- With transparent browsing on (`browser.tabs.allow_transparent_browser`, used by Transparent Zen and Zen Internet), the sidebar, URL bar, find bar, library and Glance glass no longer show sharp page text through them, and Settings pop-ups are frosted.
- Opening the URL bar now dims and zooms the page instead of blurring it, which uses noticeably less GPU. The old look is still available as **Blur (heavier on the GPU)**.
- New setting: **Show the icon glow behind the selected Essential** (Zen's `zen.theme.essentials-favicon-bg`).
- Lighter on the CPU and GPU: no per-frame URL bar tracking, no duplicate blur on the URL bar, and the loading animation no longer restyles the window on every tab change.
- Fixed: the downloads preview no longer slides under the page, downloads show one "open in folder" button (Zen's own), and extensions dropped above the pins in Customize Toolbar stay there.
- Renamed from Zen-Nebula to Nebula Nova.
- Reorganized the settings by what they change (Appearance, Tabs and sidebar, Toolbar, Motion and media), with clearer labels. Settings that don't apply stay hidden: the font name until a system font is chosen, the artwork style until artwork is on, popup blur outside Windows, and colors until **Customize colors** is ticked. Saved settings carry over.
- With transparent browsing on, glass edges no longer darken, and the compact sidebar no longer shows a black edge while it slides in or out.
