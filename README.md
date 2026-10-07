# Routeboy Flatpak

Flatpak packaging for [Routeboy](https://github.com/rubiojr/routeboy).
Uses the Freedesktop 25.08 runtime and Go SDK extension, with native Wayland
and X11 support.

## Build and install

Install Go 1.27.1 or newer, Git, `flatpak` and `flatpak-builder`. Add Flathub:

```sh
flatpak remote-add --user --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

Clone the sources and build:

```sh
git clone https://github.com/rubiojr/routeboy.git
git clone https://github.com/rubiojr/routeboy-flatpak.git routeboy/flatpak
cd routeboy
scripts/flatpak
flatpak install --user dist/co.rbel.routeboy.flatpak
flatpak run co.rbel.routeboy
```

The build installs the required runtime and SDK from Flathub. It snapshots your
working tree and vendors Go dependencies before compiling in Flatpak's offline
sandbox. Application assets come from Routeboy's `assets/` directory.

For a separate packaging checkout, run `ROUTEBOY=/path/to/routeboy ./build`.
Set `OUT` to change the output directory. `./build --sources-only` prepares the
archive and manifest in `OUT/flatpak/` for a later `flatpak-builder` run.

## Tracks

The sandbox can read `~/Tracks`. To use another folder:

```sh
flatpak override --user --filesystem="$HOME/Downloads/gpx:ro" co.rbel.routeboy
flatpak run co.rbel.routeboy -tracks "$HOME/Downloads/gpx"
```

Preferences and cached maps live under `~/.var/app/co.rbel.routeboy/`.
