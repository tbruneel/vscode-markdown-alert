# VS Code Markdown Alert

Support [GitHub style alerts](https://github.com/orgs/community/discussions/16925) for VS Code Markdown preview and in notebook powered by [markdown-it-github-alerts](https://github.com/antfu/markdown-it-github-alerts).

## Fork Modifications (`tbruneel/vscode-markdown-alert`)

This fork refines [`markdown-alert.css`](markdown-alert.css) for cleaner vertical spacing in VS Code's built-in Markdown preview (paired with [`tbruneel/vscode-markdown-stylesheets`](https://github.com/tbruneel/vscode-markdown-stylesheets) and [`tbruneel/vscode-markdown-html`](https://github.com/tbruneel/vscode-markdown-html)):

1. **Tighter Spacing Between Alert Title and Content (`margin-bottom: 6px`):**
   - **Why:** Upstream renders the alert header as `<p class="markdown-alert-title">` without overriding `margin-bottom`, causing it to inherit VS Code's default `p { margin-bottom: 16px; }` and leaving a large gap between the alert title and body text.
   - **What:** Added `margin-bottom: 6px;` to `.markdown-alert .markdown-alert-title` for compact spacing between the header and content.
2. **Suppress Empty Leading Paragraphs (`.markdown-alert > p:empty`):**
   - **Why:** When an alert marker (`> [!IMPORTANT]`) is followed by a blank `>` line before the body text, stripping the `[!IMPORTANT]` token leaves an empty `<p></p>` element under the title.
   - **What:** Added `.markdown-alert > p:empty { display: none; }` so alerts render with identical spacing whether or not a blank `>` line follows the marker.

---

![preview](https://raw.githubusercontent.com/kejunmao/vscode-markdown-alert/main/docs/preview.png)

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
