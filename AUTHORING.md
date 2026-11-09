# Authoring guide for this tutorial

This repo is a tutorial (or learning path) rendered with Hugo using the shared
theme module `github.com/cbowland/tutorial-template` (built on Hextra).
**Only write content and config here — never add layouts, partials, or CSS.**
Theme changes belong in the tutorial-template repo. (Exception: small style tweaks may go in
`assets/css/custom.css`.)

## Structure

- `content/_index.md` — the tutorial's overview page (what you'll learn, prerequisites).
  Keep its `cascade: { type: docs }` front matter.
- A **section** is a folder with an `_index.md` (section intro) plus lesson files:
  `content/01-getting-started/_index.md`, `content/01-getting-started/install.md`.
- A short tutorial can skip sections: lesson files directly in `content/`.
- Max depth: section → lesson. Do not nest sections inside sections.
- Folder/file prefixes (`01-`, `02-`) keep the file tree tidy; they appear in URLs.
- **Order comes from `weight`, not file names.** Use 10, 20, 30… so pages can be inserted later.
- Numbering (1, 1.1, 1.2, 2…) and prev/next links are generated automatically from that order.
  Never type numbers into titles.
- One concept per lesson. Aim for 5–15 minutes of reading/doing per lesson.

## Front matter

```yaml
---
title: Install the CLI          # required; no number prefix
weight: 20                      # required; order within its section
duration: 10 min                # optional; shown under the title
prerequisites:                  # optional; plain text or a page path starting with /
  - A terminal
  - /01-getting-started/install
draft: true                     # optional; hidden from published site
numbered: false                 # optional; e.g. for an appendix
toc: false                      # optional; hide the "On this page" outline
---
```

## Lesson shape

1. One or two sentences: what the reader will do and why.
2. Steps, each with a `##` heading (these feed the "On this page" outline).
3. A "Check your work" section saying what success looks like.

## Content elements

Fenced code blocks — always give a language; a copy button is added automatically:

````markdown
```bash
kubectl get pods
```
````

Inline copyable value (short text inside a sentence):

```markdown
Set the password to {{< copy "s3cr3t-value" >}}
```

Images — put files in `static/images/` (or next to the page in a page bundle).
Either form gives a captioned figure that works locally and on GitHub Pages:

```markdown
![Alt text](/images/dashboard.png "Figure 1: The dashboard")
{{< figure src="images/dashboard.png" alt="Alt text" caption="Figure 1: The dashboard" >}}
```

Callouts (`info`, `warning`, `error`; or omit type for a default note):

```markdown
{{< callout type="warning" >}}
This deletes the namespace.
{{< /callout >}}
```

Numbered step-by-step blocks, tabs (e.g. per-OS commands), and more are available
from Hextra: <https://imfing.github.io/hextra/docs/guide/shortcodes/> (`steps`, `tabs`, `details`, `cards`, `filetree`).

## Accuracy rules

- Every command and code sample must be run and verified before the page is
  marked non-draft. If you could not verify something, say so in your summary
  and leave the page as `draft: true`.
- Pin versions in install commands where it matters, and state the version the
  tutorial was tested with on the overview page.
- Do not invent flags, outputs, or UI labels. Show real output, trimmed if long.

## Previewing

```bash
hugo server        # http://localhost:1313/
hugo server -D     # include drafts
```

## Updating the theme

```bash
hugo mod get -u github.com/cbowland/tutorial-template   # latest release
hugo mod get github.com/cbowland/tutorial-template@v0.2.0   # specific version
hugo mod tidy
```
