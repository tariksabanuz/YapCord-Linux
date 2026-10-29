# YapCord for Linux

YapCord is a Vencord-style mod for the Yapper desktop app: plugins, themes and extra
settings on top of the official Yapper client. This guide, and this build, are
**for Linux only** — running these commands on Windows or macOS will not produce
a usable app; use the Windows or macOS build guide instead.

## Requirements

- **A Linux distro** (any — Ubuntu, Fedora, Arch, etc. all work the same way here).
- **Node.js** 18 or newer — install via your distro's package manager (e.g. `sudo apt install nodejs npm`, `sudo dnf install nodejs`, `sudo pacman -S nodejs npm`), or [nodejs.org](https://nodejs.org).
- A terminal.
- An internet connection the first time you build (npm/electron-builder download their own pieces).

Check Node is installed:

```bash
node -v
npm -v
```

## 1. Get the source

Download the YapCord source (zip, or `git clone` the repo) and extract it, then
open a terminal **in the extracted folder** (the one that directly contains
`package.json`). Install dependencies once:

```bash
npm install
```

## 2. Build the AppImage

```bash
npm run dist:linux
```

Output lands at:

```
dist/YapCord-<version>.AppImage
```

This builds a Linux **AppImage** specifically — not an .exe, not a .app. It
will only run on Linux.

## 3. Run it

```bash
chmod +x dist/YapCord-*.AppImage
./dist/YapCord-*.AppImage
```

You can also double-click it from a file manager, once it's marked executable.

> **No FUSE on your system?** Some distros (and most sandboxes/containers) don't
> have FUSE set up, and the AppImage will refuse to run with an error mentioning
> `fuse` or `AppImage`. Either install `fuse`/`fuse2` from your distro's package
> manager, or run it without FUSE like this:
> ```bash
> ./dist/YapCord-*.AppImage --appimage-extract-and-run
> ```

### Optional: add it to your app menu

AppImages don't auto-integrate with your desktop's app menu the way a package
manager install does. If you want a proper menu entry and icon, use a tool like
[AppImageLauncher](https://github.com/TheAssassin/AppImageLauncher) (install it
once via your distro, then just double-click the AppImage and it offers to
integrate it) — this is optional, the AppImage runs fine without it.

## 4. Updating to a new version

Grab the new source, extract it somewhere fresh (don't mix old and new files),
run `npm install` again if `package.json`'s dependencies changed, and repeat
step 2. The new AppImage is a separate file — delete the old one yourself if you
don't need it any more (and re-integrate the new one if you used AppImageLauncher).

## Troubleshooting

| Problem | Fix |
|---|---|
| `npm run dist:linux` fails right away | Run `npm install` first if you haven't, and make sure you're in the folder that directly contains `package.json`. |
| AppImage won't launch, mentions FUSE | Install `fuse`/`fuse2`, or launch with `--appimage-extract-and-run` (see above). |
| "Permission denied" when running the AppImage | `chmod +x` it first — a freshly downloaded/built file often isn't marked executable yet. |
| Double-clicking does nothing in the file manager | Some file managers need "Allow executing" turned on in the file's Properties → Permissions tab, in addition to `chmod +x`. |
| Build fails downloading electron-builder's pieces | Check your internet connection — the first build needs to fetch some tooling. |
