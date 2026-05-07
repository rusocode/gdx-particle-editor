<!-- Generated: 2026-05-07 | Files scanned: 120 | Token estimate: ~700 -->

# Architecture

## System Overview

Single-module Gradle desktop application. All UI via libGDX Scene2D.UI (no Swing/AWT).

```
Lwjgl3Launcher.main()
  └─ StartupHelper.startNewJvmIfRequired()   (macOS M1 fix)
  └─ new Lwjgl3Application(Core, config)
       └─ Core.create()
            ├─ SkinLoader.loadSkin()
            ├─ ShortcutManager + KeyMap init
            └─ Core.populate(screen)
                 └─ WelcomeTable | ClassicTable | WizardTable
```

## Render Loop

```
Core.render()
  ├─ stage.act() + stage.draw()          (main UI)
  ├─ ParticlePreview.render()            (particle viewport)
  └─ foregroundStage.act() + draw()      (popups, tooltips)
```

## Layer Model

| Stage | Contents |
|-------|----------|
| `stage` | Main editor UI (panels, subpanels) |
| `foregroundStage` | Dialogs, tooltips, toasts |
| `previewViewport` | Particle rendering (orthographic camera) |

## Static Singletons (Core.java)

All initialized in `Core.create()`, accessed globally:

```
Core.stage, .foregroundStage, .spriteBatch, .skin
Core.particleEffect, .selectedEmitter, .activeEmitters
Core.shortcutManager, .keyMap, .preferences
Core.openFileFileHandle, .shapeDrawer, .sprites, .fileHandles
Core.unsavedChangesMade, .toastQueue, .tooltips
```

## Data Flow: User Edit

```
User input
  → Actor.listener (Scene2D event)
  → new XxxUndoable()
    → undoable.start()          (apply mutation)
    → UndoManager.add()
    → Core.unsavedChangesMade = true
    → Utils.refreshUndoButtons()
```

## Key Subsystems

```
shortcuts/   Keyboard input → ShortcutManager → KeyMap → Shortcut.runnable.run()
runnables/   File I/O and mode switch commands
undo/        UndoManager stack + 23 Undoable implementations
widgets/     All UI: panels, subpanels, dialogs, custom components
```