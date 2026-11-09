---
title: "6. Copy Mode"
weight: 6
---

Copy mode lets you scroll back through a pane's output, search it, and copy text, all from the keyboard. The config keeps **10,000 lines** of history per pane and uses **vi keys**.

## Enter and leave

| Key | Action |
|---|---|
| `prefix v` | enter copy mode (from the config) |
| `prefix [` | also enters copy mode (tmux default) |
| scroll the mouse wheel up | enters copy mode and scrolls |
| `q` | leave copy mode |

In copy mode, a position indicator such as `[0/1234]` appears in the top-right corner of the pane.

## Moving around (vi keys)

| Key | Move |
|---|---|
| `h` `j` `k` `l` | left, down, up, right |
| `w` / `b` / `e` | next word / previous word / end of word |
| `0` / `$` | start / end of line |
| `Ctrl+u` / `Ctrl+d` | half page up / down |
| `g` / `G` | top / bottom of history |

## Search

| Key | Action |
|---|---|
| `/` then text, `Enter` | search **down** (toward newer output) |
| `?` then text, `Enter` | search **up** (toward older output) |
| `n` / `N` | next / previous match |

{{< callout type="info" >}}
Most searches should start with `?`. The output you want is usually *above* you, because it's older than where you are.
{{< /callout >}}

## Select and copy

These are tmux's **default** vi copy-mode keys. They're not vim's keys, and your config doesn't change them:

| Key | Action |
|---|---|
| `Space` | start a selection |
| `V` | select the whole line |
| `v` | toggle **rectangle** (block) selection. This does *not* start a selection |
| `Enter` | copy the selection and leave copy mode |
| `Esc` | clear the selection (stay in copy mode) |
| `prefix ]` | paste the most recent copy into the current pane |

{{< callout type="warning" >}}
**If you use vim:** in tmux copy mode `v` does *not* start a selection and `y` does *not* copy. Use `Space` and `Enter`. If you'd rather have vim keys, add these to your config and press `prefix r`:

```bash
bind -T copy-mode-vi v send -X begin-selection
bind -T copy-mode-vi y send -X copy-selection-and-cancel
```

The rest of this tutorial sticks with the defaults.
{{< /callout >}}

## Mouse selection

With `mouse on`, dragging over text in a pane selects it **in tmux** and copies it to the tmux buffer when you let go (paste with `prefix ]`). It doesn't automatically go to your system clipboard.

To get your terminal's **normal** selection back (so `Cmd+C` works), hold a modifier while you drag:

| Terminal | Hold while dragging |
|---|---|
| iTerm2 | `Option` |
| Terminal.app | `fn` |
| Ghostty, most Linux terminals | `Shift` |

## Getting copies into the system clipboard

Whether `Enter` in copy mode also reaches your macOS or Linux clipboard depends on your terminal. Many modern terminals (iTerm2, Ghostty, kitty, WezTerm) accept tmux's clipboard escape sequence. Terminal.app does not.

To make it work everywhere, tell tmux which command to send copies to:

{{< tabs >}}
  {{< tab name="macOS" >}}
```bash
set -s copy-command 'pbcopy'
```
  {{< /tab >}}
  {{< tab name="Linux (Wayland)" >}}
```bash
set -s copy-command 'wl-copy'
```
  {{< /tab >}}
  {{< tab name="Linux (X11)" >}}
```bash
set -s copy-command 'xclip -selection clipboard'
```
  {{< /tab >}}
{{< /tabs >}}

This is optional and isn't in the base config.

## Practice

{{% steps %}}

### Generate some history

```bash
tmux new -s copy
seq 1 500
```

### Scroll and jump

`prefix v`. Press `g` (top of history, line 1), `G` (bottom), `Ctrl+u` a few times, then `q`.

### Search

`prefix v`, then `?` `250` `Enter`. Press `n` a couple of times to find older matches. Press `q`.

### Copy and paste a line

`prefix v`, `?` `42` `Enter`, `V` (select the line), `Enter` (copy). Type `echo ` (with a trailing space) and press `prefix ]`. You've pasted `42` onto the command line.

### Try the mouse

Scroll up with the wheel (copy mode starts), drag over some numbers, let go. Then press `prefix ]` at an empty prompt.

{{% /steps %}}
