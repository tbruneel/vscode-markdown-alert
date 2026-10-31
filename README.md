# VS Code Markdown Alert

Support [GitHub style alerts](https://github.com/orgs/community/discussions/16925) for VS Code Markdown preview and in notebook powered by [markdown-it-github-alerts](https://github.com/antfu/markdown-it-github-alerts).

## Fork Modifications (`tbruneel/vscode-markdown-alert`)

This fork refines [`markdown-alert.css`](markdown-alert.css) for cleaner vertical spacing and GitHub-compatible page/table geometry in VS Code's built-in Markdown preview (paired with [`tbruneel/vscode-markdown-stylesheets`](https://github.com/tbruneel/vscode-markdown-stylesheets) and [`tbruneel/vscode-markdown-pdf`](https://github.com/tbruneel/vscode-markdown-pdf)):

1. **GitHub-Compatible Page Width & Self-Contained Table Overflow:**
   - **Why:** VS Code's built-in Markdown preview stretches to `100%` of the editor tab width and uses `display: table`, which causes wide tables to overflow the `body` container differently than GitHub.com (`width: 1012px` with `32px` padding).
   - **What:** Added `body { width: 1012px; margin: 0 auto; padding: 32px; box-sizing: border-box; }` (`948px` inner content width) and `table { display: block; width: max-content; max-width: 100%; overflow: auto; }` so VS Code's live preview renders with the exact same line wrapping, container width, and table scrolling behavior as GitHub.com and `Markdown PDF` exports.
2. **Tighter Spacing Between Alert Title and Content (`margin-bottom: 6px`):**
   - **Why:** Upstream renders the alert header as `<p class="markdown-alert-title">` without overriding `margin-bottom`, causing it to inherit VS Code's default `p { margin-bottom: 16px; }` and leaving a large gap between the alert title and body text.
   - **What:** Added `margin-bottom: 6px;` to `.markdown-alert .markdown-alert-title` for compact spacing between the header and content.
3. **Suppress Empty Leading Paragraphs (`.markdown-alert > p:empty`):**
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
