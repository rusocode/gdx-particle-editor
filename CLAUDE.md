# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Build & Run

```bash
# Run the application
./gradlew core:run

# Build fat JAR (output: core/build/lib/gdx-particle-editor.jar)
./gradlew core:jar

# Build distributable image (requires JDK 14+)
./gradlew core:jpackageImage

# Clean
./gradlew clean
```

Run the built JAR directly:
```bash
java -jar core/build/lib/gdx-particle-editor.jar
```

There are no automated tests — this is a GUI application tested manually through the UI.

## Architecture

Single-module Gradle project (`core`). Entry point: `Lwjgl3Launcher` → `Core` (libGDX `ApplicationAdapter`). All UI is Scene2D.UI — no Swing or AWT. See `docs/CODEMAPS/` for detailed architecture documentation.

### Asset Handling

Assets live in `/assets` (particle files, images, skins, icons). User preferences and logs are written to `~/.gdxparticleeditor/`. When loading external `.p` particle files, image paths are resolved relative to the `.p` file's location (see `Utils`).

## Codemaps

Detailed architecture documentation lives in `docs/CODEMAPS/`:

- `architecture.md` — execution flow, render loop, stage layers, static singletons, edit data flow
- `frontend.md` — screen layouts, panel/subpanel hierarchy, custom widgets, dialogs, vendored shims
- `dependencies.md` — all runtime/compile dependencies with versions, vendored classes