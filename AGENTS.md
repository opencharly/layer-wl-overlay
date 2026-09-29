# AGENTS.md — layer-wl-overlay

Standalone candy repo for the `wl-overlay` layer — the gtk4-layer-shell
fullscreen overlay helper for Wayland desktop recordings. The candy lives in
`charly.yml` at the repo root: the `require:` on `pod-dbus`, the per-distro
packages, the `copy:` plan steps, and the `check:` assertions. This repo carries
**no `skill:` entity**, so there is no owning `/charly-<family>:<name>` skill
projected into the marketplace corpus for it (recorded against
opencharly/opencharly#291).

Canonical files:

- `charly.yml` — the `wl-overlay:` candy entity (the `require:`, the per-distro
  packages, the `copy:` plan steps, the `check:` assertions).
- `charly-overlay` — the helper script copied to `~/.local/bin/charly-overlay`.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-selkies:wl-overlay-layer` — the closest existing skill: the candy's
  package/script contract. There is no per-repo owning skill; the gap is recorded
  against opencharly/opencharly#291.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package/repo
  sections, service declarations). Load before editing any entity field or plan
  step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence — the helper
  script installed at mode `0755` and the `gtk4-layer-shell` package.
- The `copy:` step's `mode: "0755"` and the check's `mode: "0755"` must agree.

## Modify this repo

- Edit the `wl-overlay:` candy entity in `charly.yml`. A change to the helper
  script belongs in `charly-overlay`; the `copy:`/`check:` paths and mode move
  with it.
- Since this repo has no `skill:` entity, there is no projected skill body to
  mirror; the corpus gap is tracked in opencharly/opencharly#291.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge on
  PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the PR
  body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
