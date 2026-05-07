<!-- Generated: 2026-05-07 | Files scanned: 120 | Token estimate: ~750 -->

# Frontend (Scene2D.UI)

## Screen Layouts (widgets/tables/)

```
WelcomeTable    — Start screen: mode buttons, recent files list
ClassicTable    — Legacy-style split editor
WizardTable     — Step-by-step guided editor
```

`Core.populate(screen)` swaps between them by clearing `root` and adding the chosen table.

## Panel Hierarchy (Classic/Wizard modes)

```
ClassicTable / WizardTable
  ├─ PreviewPanel          — Particle preview + zoom/pan controls
  ├─ EffectEmittersPanel   — Emitter list: add, delete, duplicate, reorder
  ├─ EmitterPropertiesPanel — Collapsible sections, one SubPanel per property
  │    ├─ CountSubPanel
  │    ├─ RangeSubPanel
  │    ├─ SizeSubPanel
  │    ├─ SpawnSubPanel
  │    ├─ ImagesSubPanel
  │    ├─ TintSubPanel
  │    ├─ TransparencySubPanel
  │    ├─ OptionsSubPanel
  │    └─ GraphSubPanel
  ├─ StartPanel            — Mode toggle buttons
  └─ SummaryPanel          — Stats (emitter count, max particles)
```

## Custom Widgets (widgets/)

| Widget | Purpose |
|--------|---------|
| `ColorGraph` | Interactive color-over-time gradient editor |
| `LineGraph` | Value-over-time curve editor |
| `InfSlider` | Unbounded numeric slider |
| `EditableLabel` | Click-to-edit inline text |
| `CollapsibleGroup` | Expand/collapse container |
| `Carousel` | Horizontal option scroller |
| `Toast` | Transient notification overlay |
| `ToggleGroup` | Single-select button group |
| `CardGroup` | Card-style container |

## Dialogs (widgets/poptables/) — all extend PopTable

| Dialog | Trigger |
|--------|---------|
| `PopEditorSettings` | Settings button |
| `PopPreviewSettings` | Preview config button |
| `PopTemplate` | New particle from template |
| `PopExport` | Export action |
| `PopAddProperty` | Add emitter property |
| `PopConfirmClose` | Close with unsaved changes |
| `PopConfirmLoad` | Load with unsaved changes |
| `PopLocateImages` | Missing image path resolution |
| `PopImageError` | Image load failure |
| `PopError` | Generic error |

## Style System

`Skin` loaded by `SkinLoader` from `assets/skins/`. Style holder classes in `widgets/styles/` map skin keys to typed style objects used by custom widgets.

## Forked libGDX Classes (shims)

Local copies with patches applied (in `com.badlogic.gdx.*`):
- `TextField`, `ScrollPane`, `DragAndDrop`, `DragListener`, `DefaultLwjgl3Input`

Stripe widget extensions (`com.ray3k.stripe.*`) are also vendored in-source.