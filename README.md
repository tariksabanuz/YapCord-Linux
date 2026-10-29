# YapCord for Linux

YapCord is a Vencord-style mod for the Yapper desktop app: plugins, themes and extra
settings on top of the official Yapper client. This guide covers **Linux only** —
how to build a YapCord AppImage yourself from source.

## Requirements

- **Node.js** 18 or newer — install via your distro's package manager, or [nodejs.org](https://nodejs.org).
- An internet connection the first time you build (npm/electron-builder download their own pieces).
- A terminal.

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

## 4. Updating to a new version

Grab the new source, extract it somewhere fresh (don't mix old and new files),
run `npm install` again if `package.json`'s dependencies changed, and repeat
step 2. The new AppImage is a separate file — delete the old one yourself if you
don't need it any more.

## Troubleshooting

| Problem | Fix |
|---|---|
| `npm run dist:linux` fails right away | Run `npm install` first if you haven't, and make sure you're in the folder that directly contains `package.json`. |
| AppImage won't launch, mentions FUSE | Install `fuse`/`fuse2`, or launch with `--appimage-extract-and-run` (see above). |
| "Permission denied" when running the AppImage | `chmod +x` it first — a freshly downloaded/built file often isn't marked executable yet. |
| Build fails downloading electron-builder's pieces | Check your internet connection — the first build needs to fetch some tooling. |
