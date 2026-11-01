# VS Code Markdown Alert (`tbruneel/vscode-markdown-alert`)

## Key Takeaways

> [!IMPORTANT]
> **How this extension brings native GitHub Alerts to VS Code's Markdown Preview and Notebooks:**
> - **GitHub Primer Callouts in Live Preview & Notebooks:** Renders all five official [GitHub-style blockquote alerts](https://github.com/orgs/community/discussions/16925) (`[!NOTE]`, `[!TIP]`, `[!IMPORTANT]`, `[!WARNING]`, and `[!CAUTION]`) with official Primer border colors, title colors, and inline Octicon SVGs, powered by [`markdown-it-github-alerts`](https://github.com/antfu/markdown-it-github-alerts).
> - **Consistent `16px` Title-to-Body Spacing (Fork Fix):** Refines [`markdown-alert.css`](markdown-alert.css) with `.markdown-alert > p:empty { display: none; }` so alerts render with identical GitHub spacing (`16px` / `1rem` below the title) whether or not a blank `>` line follows the `[!TYPE]` marker.
> - **Part of a Three-Extension Markdown Suite:** Designed to work alongside [`tbruneel/vscode-markdown-stylesheets`](https://github.com/tbruneel/vscode-markdown-stylesheets) (`902px` GitHub layout & selectable themes) and [`tbruneel/vscode-markdown-html`](https://github.com/tbruneel/vscode-markdown-html) (self-contained `.md.html` exporter and viewer).

## 1. Quick Start & Alert Syntax

Write any of the five GitHub alert markers at the start of a Markdown blockquote (`>`). Both **compact** syntax (body text on the very next `>` line) and **spaced** syntax (a blank `>` line after the marker) render with identical spacing:

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

### Live Rendered Output

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

## 2. Supported Alert Types & Primer Color Palette

| Alert Marker | Octicon Icon | Light Theme Color | Dark Theme Color | Intended Purpose |
| :--- | :--- | :---: | :---: | :--- |
| `> [!NOTE]` | `octicon-info` | `#0969da` *(Blue)* | `#2f81f7` *(Blue)* | Background context, implementation details, or helpful notes when skimming. |
| `> [!TIP]` | `octicon-light-bulb` | `#1a7f37` *(Green)* | `#3fb950` *(Green)* | Best practices, shortcuts, or optional advice that helps the reader succeed. |
| `> [!IMPORTANT]` | `octicon-report` | `#8250df` *(Purple)* | `#a371f7` *(Purple)* | Key takeaways, essential requirements, or critical setup steps. |
| `> [!WARNING]` | `octicon-alert` | `#9a6700` *(Amber)* | `#d29922` *(Amber)* | Potential pitfalls, compatibility caveats, or actions requiring attention. |
| `> [!CAUTION]` | `octicon-stop` | `#d1242f` *(Red)* | `#f85149` *(Red)* | High-risk actions, destructive operations, or security warnings. |

## 3. Companion Extensions Ecosystem

This repository is part of a three-extension setup that gives VS Code's Markdown Preview and `.md.html` exports a consistent GitHub Primer appearance with zero manual CSS configuration:

| Extension Repository | Role in the VS Code Markdown Suite |
| :--- | :--- |
| **[`tbruneel/vscode-markdown-alert`](https://github.com/tbruneel/vscode-markdown-alert)** *(this repo)* | Registers the `markdown-it-github-alerts` plugin and [`markdown-alert.css`](markdown-alert.css) for live VS Code Markdown Previews and Jupyter Notebooks. |
| **[`tbruneel/vscode-markdown-stylesheets`](https://github.com/tbruneel/vscode-markdown-stylesheets)** | Applies the `902px` centered container (`838px` content width), table scrollbars, code-block copy-button gutter, and selectable themes (`auto`, `vscode-light2026`, `vscode-dark2026`, `github-light`, `github-dark`) via `"markdown.styles"`. |
| **[`tbruneel/vscode-markdown-html`](https://github.com/tbruneel/vscode-markdown-html)** | Exports `.md` $\rightarrow$ self-contained `.md.html` files (with built-in GitHub Alerts, KaTeX math, and inlined theme CSS) and provides a rendered `*.md.html` viewer inside VS Code. |

## 4. Technical Overview & Fork Modifications

### 4.1 Why `.markdown-alert > p:empty` Is Needed

When authors write a blockquote alert in Markdown, two conventions are common in the wild:

| Markdown Convention | Generated HTML Inside `<div class="markdown-alert">` | Rendering Without Fix |
| :--- | :--- | :--- |
| **Compact (no blank `>` line):**<br>`> [!IMPORTANT]`<br>`> Body text here.` | `<p class="markdown-alert-title">Important</p>`<br>`<p>Body text here.</p>` | Title `<p>` has `margin-bottom: 16px` (`1rem`), creating standard GitHub spacing before the body text. |
| **Spaced (blank `>` line after marker):**<br>`> [!IMPORTANT]`<br>`>`<br>`> Body text here.` | `<p class="markdown-alert-title">Important</p>`<br>`<p></p>`<br>`<p>Body text here.</p>` | `markdown-it-github-alerts` strips the `[!IMPORTANT]` token from the first paragraph, leaving an empty `<p></p>` element with its own margins under the title. |

Adding `.markdown-alert > p:empty { display: none; }` in [`markdown-alert.css`](markdown-alert.css) suppresses that leftover empty paragraph so both conventions render with the exact same `16px` (`1rem`) spacing below `.markdown-alert-title`.

### 4.2 How Theme Colors Adapt Across Preview Modes

1. **Default `"auto"` Preview Mode:**
   - [`markdown-alert.css`](markdown-alert.css) defines `--color-note`, `--color-tip`, `--color-important`, `--color-warning`, and `--color-caution` with GitHub Light hex values by default and switches to GitHub Dark hex values inside `@media (prefers-color-scheme: dark)`.
2. **Explicit Theme Override Mode (`markdown-stylesheets.theme`):**
   - When you force a specific theme via [`vscode-markdown-stylesheets`](https://github.com/tbruneel/vscode-markdown-stylesheets) (for example, `"github-light"` while running a dark VS Code window), the selected theme stylesheet explicitly sets the alert palette for that theme so alert colors always match the document background.

### 4.3 Building & Packaging from Source

```powershell
# Install dependencies
pnpm install

# Bundle extension (dist/index.js) and notebook renderer (dist/notebook.mjs)
pnpm run build

# Package into a local .vsix archive
pnpm run pack
```
