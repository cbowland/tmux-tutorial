---
title: "tmux: From Zero to Muscle Memory"
linkTitle: tmux
weight: 1
cascade:
  type: docs
---

tmux lets one terminal window hold many shells, organized into **sessions**, **windows**, and **panes**. Those shells keep running when you close the terminal, lose your SSH connection, or walk away for the weekend.

This tutorial is for two kinds of people:

- **Complete beginners** who have never used tmux.
- **People who have tried tmux a little**, maybe with the default keys, and never made it a habit.

By the end you should be able to manage several projects at once, each in its own session, and move between sessions, windows, and panes without thinking about the keys.

## How this tutorial works

1. **Set up the config once.** Chapter 1 installs tmux and a small config that remaps a few keys to be easier to reach. Every key in the rest of the tutorial assumes that config.
2. **Learn one layer at a time:** sessions → windows → panes → more sessions (the important part) → copy mode.
3. **Practice at the end of every chapter.** Each chapter finishes with a short exercise to do in a real terminal. Do it. Reading about keybindings doesn't build muscle memory.
4. **Drill for a week.** The drills chapter has short, timed rounds. Repeat them for a few days and the keys become automatic.

{{< callout type="info" >}}
**Notation.** `prefix` means *press and release `Ctrl+a`, then press the next key*. So `prefix c` means "Ctrl+a, let go, then c". Don't hold Ctrl down for the second key unless the tutorial says so.
{{< /callout >}}

## Chapters

{{< cards >}}
  {{< card link="01-install-and-config" title="1. Install & Config" icon="cog" subtitle="Install tmux, load the config, check it works." >}}
  {{< card link="02-first-session" title="2. Your First Session" icon="play" subtitle="Start, detach, reattach. The prefix habit." >}}
  {{< card link="03-windows" title="3. Windows" icon="view-boards" subtitle="Tabs inside a session." >}}
  {{< card link="04-panes" title="4. Panes" icon="view-grid" subtitle="Split, move, zoom, resize." >}}
  {{< card link="05-sessions" title="5. Sessions" icon="collection" subtitle="One session per project. Switching between them." >}}
  {{< card link="06-copy-mode" title="6. Copy Mode" icon="clipboard-copy" subtitle="Scrollback, search, copy and paste." >}}
  {{< card link="07-workflows" title="7. Workflows" icon="briefcase" subtitle="Real-world scenarios that use everything." >}}
  {{< card link="08-drills" title="8. Drills" icon="lightning-bolt" subtitle="Timed rounds to build muscle memory." >}}
  {{< card link="cheatsheet" title="Cheat Sheet" icon="document-text" subtitle="Every key on one page." >}}
{{< /cards >}}
