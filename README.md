# VS Code Markdown Alert

## Key Takeaways

> [!IMPORTANT]
> - **GitHub Alerts in Markdown Preview:** Renders all five [GitHub Alert](https://github.com/orgs/community/discussions/16925) callouts (`[!NOTE]`, `[!TIP]`, `[!IMPORTANT]`, `[!WARNING]`, `[!CAUTION]`) in VS Code's live Markdown Preview.
> - **Automatic & Custom Theme Support:** Switches automatically between Light and Dark palettes and supports custom stylesheet overrides via CSS variables.
> - **Companion Extensions:** Works alongside [`vscode-markdown-stylesheets`](https://github.com/tbruneel/vscode-markdown-stylesheets) and [`vscode-markdown-html`](https://github.com/tbruneel/vscode-markdown-html).

## Alert Syntax

Write any of the five GitHub Alert markers at the start of a Markdown blockquote (`>`). Both **compact** syntax (body text on the very next `>` line) and **spaced** syntax (a blank `>` line after the marker) are rendered identically:

```markdown
> [!NOTE]
> Highlights information that users should take into account, even when skimming.

> [!TIP]
> Optional information to help a user be more successful.

> [!IMPORTANT]
>
> Crucial information necessary for users to succeed (with a blank `>` line).

> [!WARNING]
> Critical content demanding immediate user attention due to potential risks.

> [!CAUTION]
> Negative potential consequences of an action.
```

## Alert Styles

The Markdown blockquotes above render as styled GitHub Alert callouts with a colored left border, bold title text, and an inline icon:

> [!NOTE]
> Highlights information that users should take into account, even when skimming.

> [!TIP]
> Optional information to help a user be more successful.

> [!IMPORTANT]
> Crucial information necessary for users to succeed.

> [!WARNING]
> Critical content demanding immediate user attention due to potential risks.

> [!CAUTION]
> Negative potential consequences of an action.

### Custom Alert Styles

Each alert's left border, title text, and icon share a single CSS custom property on `.markdown-alert`:

| Alert Type | CSS Variable | Default Light | Default Dark (`prefers-color-scheme: dark`) |
| :--- | :--- | :--- | :--- |
| `[!NOTE]` | `--color-note` | `#0969da` (Blue) | `#2f81f7` (Blue) |
| `[!TIP]` | `--color-tip` | `#1a7f37` (Green) | `#3fb950` (Green) |
| `[!IMPORTANT]` | `--color-important` | `#8250df` (Purple) | `#a371f7` (Purple) |
| `[!WARNING]` | `--color-warning` | `#9a6700` (Amber) | `#d29922` (Amber) |
| `[!CAUTION]` | `--color-caution` | `#d1242f` (Red) | `#f85149` (Red) |

- **Automatic Theme Detection:** Out of the box, the provided [`markdown-alert.css`](markdown-alert.css) applies the GitHub Light palette when VS Code runs in light mode, and automatically switches to the GitHub Dark palette when VS Code runs in dark mode.
- **Stylesheet Theme Overrides:** Because colors are driven by the above CSS variables, any stylesheet loaded via `"markdown.styles"` can override them. When using [`vscode-markdown-stylesheets`](https://github.com/tbruneel/vscode-markdown-stylesheets), setting a custom stylesheet via `"markdown-stylesheets.theme"` automatically overrides the alert palette so callouts always match the preview background.

## Companion Extensions

This repository is part of a three-extension setup:

| Extension Repository | Role in the VS Code Markdown Suite |
| :--- | :--- |
| **[`tbruneel/vscode-markdown-alert`](https://github.com/tbruneel/vscode-markdown-alert)** *(this repo)* | Provides support for GitHub Alert callouts in VS Code's live Markdown Preview, with support for automatic theme detection and Markdown stylesheet theme overrides. |
| **[`tbruneel/vscode-markdown-stylesheets`](https://github.com/tbruneel/vscode-markdown-stylesheets)** | Provides custom Markdown stylesheet themes that align with GitHub styling (such as a fixed-width centered layout, and blockquotes with horizontal scrollbars and a copy-to-clipboard button). |
| **[`tbruneel/vscode-markdown-html`](https://github.com/tbruneel/vscode-markdown-html)** | Exports Markdown files (`.md`) to self-contained Markdown files (`.md.html`) which are automatically opened by VS Code's built-in web browser. |

## Building & Packaging from Source

```powershell
# Install dependencies
pnpm install

# Bundle extension into dist/
pnpm run build

# Package into a local .vsix archive
npx @vscode/vsce package --no-dependencies
```
