# tmux: From Zero to Muscle Memory

A hands-on tmux tutorial for complete beginners and for people who have tried tmux once or twice but never made it a habit. It starts by loading a small `~/.tmux.conf` (prefix `Ctrl+a`, `|` and `-` splits, mouse on, vi copy mode, windows and panes numbered from 1). The rest builds muscle memory for daily work across several sessions, windows, and panes. Every chapter ends with a practice exercise, and the drills chapter has timed rounds and a 7-day plan. Tested with tmux 3.8.

Built with [Hugo](https://gohugo.io/) and the
[tutorial-template](https://github.com/cbowland/tutorial-template) theme module.

## Run locally

Requires Hugo (0.146+) and Go.

```bash
hugo mod tidy      # first time only: download the theme
hugo server        # http://localhost:1313/  (add -D to include drafts)
```

## Starting a new tutorial from this skeleton

1. Copy the `starter/` folder from tutorial-template into a new directory and `git init` it.
2. Edit every `CHANGE ME`: module path in `go.mod`, `title` and footer in `hugo.yaml`, this README.
3. Fetch the theme: `hugo mod get github.com/cbowland/tutorial-template@v0.1.0 && hugo mod tidy`
4. Run `hugo server` and start writing in `content/`. See `AUTHORING.md` for conventions.

## Publishing (optional)

Publishing to GitHub Pages is **off by default**. To turn it on:

1. Settings → Pages → Source: **GitHub Actions**.
2. Settings → Secrets and variables → Actions → Variables: add `PAGES_ENABLED` = `true`.
3. Push to `main` (or run the workflow manually from the Actions tab).

The site will be at `https://<user>.github.io/<repo>/`.

> GitHub Pages sites are **public, even if the repository is private** (unless you
> are on GitHub Enterprise). Keep personal-learning tutorials local, or don't enable publishing.
