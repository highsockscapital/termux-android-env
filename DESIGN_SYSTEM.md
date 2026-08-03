# Neo-Brutalist Material 3 Design System

Standard visual language for Termux Android builds. Bold, flat, and high-contrast,
with hard borders, offset shadows, and a restrained Neo-Brutalist palette.

> Palette is canonical in **templates/colors.xml**. Keep this document in sync with it.

## 1. Palette (canonical)

| Token | Hex | Role |
| --- | --- | --- |
| `nb_background` | `#FFFFF0` | Window / background (Ivory) |
| `nb_text`       | `#161610` | Text primary, icons (Dark Charcoal) |
| `nb_surface`    | `#FFFFFF` | Card surfaces / dialogs (Clean White) |
| `nb_accent`     | `#FF9E43` | Accent — FABs, progress bars, active states (Soft Light Orange) |
| `nb_stroke`     | `#161610` | Strokes & borders (Dark Charcoal) |

### Semantic extensions

| Token | Hex | Role |
| --- | --- | --- |
| `nb_success`         | `#2F9E44` | Positive confirmation |
| `nb_error`           | `#D64545` | Destructive / errors |
| `nb_text_on_accent`  | `#161610` | Text layered on accent (Dark Charcoal on orange) |

## 2. Core rules

- **Flat color.** No gradients, no glassmorphism, no elevation-based depth.
- **Thick strokes.** Apply a solid **1dp or 2dp `#161610`** stroke to all Buttons, Cards,
  Input Boxes, and Dialog borders.
- **Hard offset shadows.** Fake depth with a *zero-blur offset* rectangle, never a blurred
  `box-shadow` or Material elevation tint.
- **High contrast.** `nb_text` on `nb_background` / `nb_surface`; keep text/icons legible.
- **Status bar.** Matches the window (`#FFFFF0`) with dark status-bar icons enabled.
- **Chunky type.** Heavy weights, uppercase labels, tight leading.

## 3. Borders & shadows

```css
/* web example: hard + offset, zero blur */
.card {
  border: 2px solid #161610;
  box-shadow: 6px 6px 0 0 #161610;
}
.card:active { box-shadow: 3px 3px 0 0 #161610; transform: translate(3px, 3px); }
```

```xml
<!-- android layer-list: simulated hard shadow -->
<layer-list>
  <item android:left="6dp" android:top="6dp">
    <shape><solid android:color="@color/nb_stroke"/></shape>
  </item>
  <item>
    <shape android:shape="rectangle">
      <solid android:color="@color/nb_surface"/>
      <stroke android:width="2dp" android:color="@color/nb_stroke"/>
      <corners android:radius="0dp"/>
    </shape>
  </item>
</layer-list>
```

On press/tap, translate the element toward the shadow and shrink the shadow by the same
distance to simulate a physical press. Keep corners **sharp** (0 radius).

## 4. Typography

- **Families:** heavy grotesques (Archivo Black, Anton, Space Grotesk, Bebas Neue).
- **Weights:** `700`–`900` headings, `500`–`700` body.
- **Scale (Android sp):** Display `48`, Heading `32`, Subheading `24`, Body `16`, Caption `12–14`.
- **Rules:** uppercase for labels/buttons, tight letter-spacing, body left-aligned.

## 5. Spacing

Strict 4 dp grid: `4, 8, 12, 16, 24, 32, 48, 64`. Group related content at `8–16 dp`;
separate sections at `24–48 dp`. Card padding ≥ shadow offset + `12 dp`.

## 6. Components

- **Primary button** — FAB: fill `nb_accent`, stroke `2dp nb_stroke`, {text/icons} `nb_text`
  (Charcoal) on orange; hard shadow `4dp`.
- **Secondary button / card** — fill `nb_surface`, stroke `2dp nb_stroke`, text `nb_text`;
  shadow `4–6dp`.
- **Progress bar / active state** — `nb_accent` track/fill on `nb_surface`/`nb_background`.
- **Input box** — fill `nb_surface`, stroke `2dp nb_stroke`, inner (inset) hard shadow.
- **Alert / error** — `nb_error` accent bar or fill, stroke `2dp nb_stroke`.
- **Status / success** — `nb_success` badge, stroke `2dp nb_stroke`.

## 7. Accessibility

- Never rely on color alone; pair with icon/text labels.
- Keep contrast ≥ `4.5:1`. `#161610` on `#FFFFF0`/`#FFFFFF` and on `#FF9E43` passes;
  prefer `#161610` text on the orange accent.
- Keep visible focus states (translate + border are sufficient).

## 8. Android usage

1. Copy **templates/colors.xml** into `app/src/main/res/values/`.
2. Reference tokens as `@color/nb_accent`, `@color/nb_surface`, etc.
3. Implement hard shadows with `layer-list` drawables (see §3), not elevation.
4. Set the status bar to `@color/nb_background` with dark icons (see ENVIRONMENT.md / theme).
