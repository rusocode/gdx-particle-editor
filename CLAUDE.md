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

Single-module Gradle project (`core`). Entry point: `Lwjgl3Launcher` → `Core` (libGDX `ApplicationAdapter`).

**Key versions:** libGDX 1.12.1, Java 11, Lombok 1.18.36

### Execution Flow

`Lwjgl3Launcher.main()` creates an LWJGL3 application with `Core` as the application listener. `Core` initializes all static singletons (Stage, SpriteBatch, Camera, Skin) and bootstraps the UI.

### Layer Model

`Core` manages multiple Scene2D Stages rendered in priority order: main UI → popups → tooltips. All UI is Scene2D.UI — no Swing or AWT.

### Package Map

| Package | Responsibility |
|---------|----------------|
| `com.ray3k.gdxparticleeditor` | App core: `Core`, `Settings`, `PreviewSettings`, `FileDialogs`, `Utils`, `ParticlePreview` |
| `lwjgl3` | `Lwjgl3Launcher` entry point and macOS M1 startup helper |
| `widgets` | Custom Scene2D.UI components (sliders, graphs, carousels, toast notifications) |
| `widgets.tables` | Top-level screen layouts: `WelcomeTable`, `ClassicTable`, `WizardTable` |
| `widgets.panels` | Major editor panels: preview, emitter list, emitter properties |
| `widgets.subpanels` | Per-property editors (count, range, tint, spawn, images, graph) |
| `widgets.poptables` | Modal dialogs (settings, export, confirm, errors) |
| `runnables` | Command implementations for file I/O and mode switching |
| `shortcuts` | Keyboard shortcut system (`ShortcutManager`, `Shortcut`, `KeyMap`) |
| `undo` | Undo/redo stack (`UndoManager`) with 24 `Undoable` implementations |

### Undo System

Every user action that mutates state creates an `Undoable` and pushes it to `UndoManager`. The 24 undoable types cover emitter lifecycle (add/delete/rename/move/merge) and all property value changes. When adding new editor interactions, follow this pattern.

### Asset Handling

Assets live in `/assets` (particle files, images, skins, icons). User preferences and logs are written to `~/.gdxparticleeditor/`. When loading external `.p` particle files, image paths are resolved relative to the `.p` file's location (see `Utils`).

### CI/CD

`.github/workflows/release.yml` builds the fat JAR and creates a GitHub release when a version tag is pushed. PRs should target the `dev` branch.