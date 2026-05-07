<!-- Generated: 2026-05-07 | Files scanned: 120 | Token estimate: ~350 -->

# Dependencies

## Runtime

| Dependency | Version | Role |
|------------|---------|------|
| `com.badlogicgames.gdx:gdx` | 1.12.1 | Core libGDX (rendering, input, files) |
| `com.badlogicgames.gdx:gdx-backend-lwjgl3` | 1.12.1 | LWJGL3 desktop backend |
| `com.badlogicgames.gdx:gdx-platform` (natives-desktop) | 1.12.1 | Native libs (Windows/Linux/macOS) |
| `com.github.raeleus.TenPatch:tenpatch` | 5.2.3 | 9-patch drawable support |
| `com.github.raeleus.stripe:stripe` | 1.4.5 | Extended Scene2D.UI widgets |
| `com.github.raeleus.stripe:colorpicker` | 1.4.5 | Color picker dialog |
| `space.earlygrey:shapedrawer` | 2.5.0 | Anti-aliased shape rendering |
| `com.github.tommyettinger:colorful` | 0.8.4 | Color math utilities |
| `org.lwjgl:lwjgl-tinyfd` + natives | 3.3.2 | Native file chooser dialogs |

## Compile-time Only

| Dependency | Version | Role |
|------------|---------|------|
| `org.projectlombok:lombok` | 1.18.36 | `@Data`, `@Getter`, `@Setter` annotation processing |

## Vendored / Forked

Five libGDX classes are copied locally with patches applied — not managed by Gradle:
- `com.badlogic.gdx.backends.lwjgl3.DefaultLwjgl3Input`
- `com.badlogic.gdx.scenes.scene2d.ui.TextField`
- `com.badlogic.gdx.scenes.scene2d.ui.ScrollPane`
- `com.badlogic.gdx.scenes.scene2d.utils.DragAndDrop`
- `com.badlogic.gdx.scenes.scene2d.utils.DragListener`

Stripe widget extensions (`com.ray3k.stripe.*`) are also vendored in-source.

## External Services

None. The application is fully offline — no network calls at runtime.

## CI/CD

GitHub Actions (`.github/workflows/release.yml`): builds fat JAR on version tag → creates GitHub Release.