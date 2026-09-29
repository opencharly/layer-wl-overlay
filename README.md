# layer-wl-overlay

Fullscreen Wayland overlay windows for OpenCharly desktop containers, via
gtk4-layer-shell.

The `wl-overlay` candy installs gtk4 + gtk4-layer-shell + PyGObject and a
`charly-overlay` helper script under `~/.local/bin` that draws layer-shell
overlay windows (e.g. recording indicators, title cards). It backs the `wl:`
check verb's `overlay-*` methods for screen recordings.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `wl-overlay` |
| Script | `~/.local/bin/charly-overlay` (mode `0755`) |
| Packages | `gtk4`, `gtk4-layer-shell`, `python-gobject` / `python3-gobject` (arch / fedora) |
| Requires | `pod-dbus` |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list:

```yaml
my-desktop-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-wl-overlay:v2026.239.1634'
```

Then draw an overlay from the helper script:

```bash
charly-overlay --help
```

The `wl:` check verb drives overlays declaratively via its `overlay-*` methods
(run with `charly check live <image> --filter wl`).

The candy's `plan:` asserts the helper script is installed and executable and
that the `gtk4-layer-shell` package is present.

## Layout

- `charly.yml` — the `wl-overlay:` candy entity (the `require:`, the per-distro
  packages, the `copy:` plan steps, the `check:` assertions). This repo carries
  **no `skill:` entity**.
- `charly-overlay` — the helper script copied to `~/.local/bin/`.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-selkies:wl-overlay-layer` — the closest existing skill
  (the candy's package/script contract). There is no per-repo owning skill; the
  gap is recorded against opencharly/opencharly#291.
- `/charly-check:wl-overlay` — the `wl: overlay-*` methods that drive the helper
- `/charly-check:wl` — the parent Wayland desktop-automation verb
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
