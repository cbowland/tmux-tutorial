---
title: "Panes"
weight: 4
---

Panes split one window into several shells, for example an editor on the left and a test runner on the right.

## Split

| Key | Action | Picture |
|---|---|---|
| `prefix \|` | split **side by side** (new pane on the right) | `[ \| ]` |
| `prefix -` | split **top and bottom** (new pane below) | `[ — ]` |

The key looks like the line it draws. Both splits open the new shell **in the current pane's directory**, so if you `cd ~/code/app` and split, the new pane is already in `~/code/app`.

{{< callout type="info" >}}
Default tmux uses `prefix %` (side by side) and `prefix "` (top and bottom), and new panes open in the directory tmux was started from. Those defaults still exist alongside the new keys, but this tutorial only uses `|` and `-`.
{{< /callout >}}

## Move between panes

| Key | Action |
|---|---|
| `prefix ←` `↑` `→` `↓` | move to the pane in that direction |
| `prefix o` | cycle to the next pane |
| `prefix q` then a number | show pane numbers, then press a number to jump to that pane |
| mouse click | click a pane to focus it (the config turns the mouse on) |

{{< callout type="info" >}}
**Arrow keys repeat.** After `prefix ←` you have a moment to press more arrows *without* pressing the prefix again, e.g. `prefix ← ← ↑`.
{{< /callout >}}

Because the config sets `pane-base-index 1`, `prefix q` numbers panes from **1**, the same as windows.

### Spotting the active pane

The config gives active and inactive borders the **same muted color**, so the border won't tell you which pane is active. Look for the **cursor** instead. If you're unsure, press `prefix q`; the active pane's number is shown in a different color.

## Zoom

**`prefix z`** makes the current pane fill the whole window. Press it again to restore the layout. Your config's status bar doesn't show window flags, so there's no "zoomed" marker. If a window looks like it lost its splits, it's probably just zoomed: press `prefix z`.

This is one of the most useful pane keys: split freely, then zoom whichever pane you're focusing on.

## Resize

| Method | How |
|---|---|
| Mouse | drag a border |
| Keys, 1 cell at a time | `prefix Ctrl+←↑→↓` (hold Ctrl for the arrow; repeats) |
| Keys, 5 cells at a time | `prefix Alt+←↑→↓` (hold Option/Alt for the arrow; repeats) |
| Preset layouts | `prefix Space` cycles through built-in layouts |

{{< callout type="warning" >}}
**macOS:** `Ctrl+arrow` is often taken by Mission Control (switching Spaces). Either turn those shortcuts off in *System Settings → Keyboard → Keyboard Shortcuts → Mission Control*, or use the mouse or the `Alt` versions. For `Alt+arrow` to reach tmux, your terminal may need "Use Option as Meta key" turned on (Terminal.app → Settings → Profiles → Keyboard; iTerm2 → Profiles → Keys → *Left Option key: Esc+*).
{{< /callout >}}

## Rearrange and close

| Key | Action |
|---|---|
| `prefix {` / `prefix }` | swap the current pane with the previous / next one |
| `prefix !` | move the current pane out into its own new window |
| `prefix x` | kill the current pane (asks y/n) |
| `exit` or `Ctrl+d` | close the shell, which closes the pane |

## Practice

Use the `win` session from the last chapter (or `tmux new -s win`).

{{% steps %}}

### Build an editor layout

In window `edit`:

1. `prefix |` to split side by side.
2. In the **right** pane, `prefix -` to split it top and bottom.

You now have one tall pane on the left and two stacked on the right.

### Move around without the mouse

`prefix ←` to the left pane. `prefix →` back to the right. `prefix ↓`, `prefix ↑`. Then `prefix q` and press `1`, `3`, `2`, each time pressing `prefix q` again first.

### Zoom in and out

Go to the left pane, `prefix z` to zoom, run `ls`, `prefix z` to unzoom.

### Check the directory follows you

In any pane: `cd /tmp`, then `prefix -`. Run `pwd` in the new pane. It should print `/tmp`.

### Resize

Drag the vertical border left and right with the mouse. Then try `prefix Alt+→` a few times.

### Break one out

In the newest pane, `prefix !`. It becomes its own window. Rename it with `prefix ,`.

### Tear it down

`prefix x` → `y` on panes until one is left in `edit`.

{{% /steps %}}

You can kill this session now: `tmux kill-session -t win`.
