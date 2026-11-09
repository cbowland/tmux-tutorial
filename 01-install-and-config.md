---
title: "1. Install & Config"
weight: 1
---

This chapter is short on purpose: install tmux, load the config, check that it works, and move on. The config is the foundation for every key in the rest of the tutorial.

## Install tmux

{{< tabs >}}
  {{< tab name="macOS" >}}
```bash
brew install tmux
```
  {{< /tab >}}
  {{< tab name="Debian / Ubuntu" >}}
```bash
sudo apt install tmux
```
  {{< /tab >}}
  {{< tab name="Fedora / RHEL" >}}
```bash
sudo dnf install tmux
```
  {{< /tab >}}
{{< /tabs >}}

Check the version:

```bash
tmux -V
```

{{< callout type="warning" >}}
You need **tmux 3.2 or newer**. The config uses `pane-border-lines`, which older versions don't recognize. If your distro ships something older, get a newer build (Homebrew works on Linux too).
{{< /callout >}}

## The config

Save this as `~/.tmux.conf`:

```bash {filename="~/.tmux.conf"}
# --- prefix -------------------------------------------------
unbind C-b                 # drop the default prefix
set -g prefix C-a          # Ctrl+a is closer to home row
bind C-a send-prefix       # press Ctrl+a twice to send a literal Ctrl+a

# --- usability ----------------------------------------------
set -g mouse on            # click panes, drag borders, scroll natively
set -g history-limit 10000 # keep more scrollback than the default 2000
set -g base-index 1        # number windows from 1, not 0
setw -g pane-base-index 1  # number panes from 1 too

# --- copy mode ----------------------------------------------
setw -g mode-keys vi       # vi keys in copy mode
bind v copy-mode           # prefix v to enter copy mode quickly

# --- saner splits -------------------------------------------
bind | split-window -h -c "#{pane_current_path}"  # | splits left/right
bind - split-window -v -c "#{pane_current_path}"  # - splits top/bottom
# both open in the current pane's directory

# --- reload -------------------------------------------------
bind r source-file ~/.tmux.conf \; display "reloaded"

set -g status-style bg=black,fg=white
set -g status-left ""
set -g status-right " %Y-%m-%d %H:%M "

# --- titles -------------------------------------------------
# Enable terminal title updates
set-option -g set-titles on

# Customize what the title actually says
# #S = Session Name, #W = Window Name
set-option -g set-titles-string "#S: #W"


# Style for the tabs themselves
setw -g window-status-format " #I:#W "
setw -g window-status-current-format "#[bg=white,fg=black,bold] #I:#W "

# Clean pane borders (dim inactive, highlight active)
# set -g pane-border-style fg=brightblack
# set -g pane-active-border-style fg=white

# 1. Revert back to proper solid terminal lines
set -g pane-border-lines single

# 2. Force both active and inactive lines to use the exact same muted color
set -g pane-border-style "fg=brightblack"
set -g pane-active-border-style "fg=brightblack"
```

## What each section does

| Section | In one line |
|---|---|
| **prefix** | The "command key" moves from `Ctrl+b` to `Ctrl+a`, which is easier to reach. Pressing `Ctrl+a` twice sends a real `Ctrl+a` to the shell (jump to start of line). |
| **usability** | The mouse works, scrollback is longer, and windows and panes are numbered from **1**, so the numbers match the number row on your keyboard. |
| **copy mode** | Scrolling and selecting use vi keys (`h j k l`, `/` to search). `prefix v` enters copy mode. |
| **saner splits** | `prefix \|` splits side by side and `prefix -` splits top and bottom. The key looks like the line it draws, and the new pane opens in the same directory. |
| **reload** | `prefix r` re-reads the config, so you never need to restart tmux after editing it. |
| **status bar** | Plain black bar: window list on the left, date and time on the right. The current window is shown in reverse colors. |
| **titles** | Your terminal's tab or title bar shows `session: window`. |
| **pane borders** | Thin, muted lines. Active and inactive borders look the same, so the layout stays calm. |

{{< callout type="info" >}}
**Coming from default tmux?** Other docs use `Ctrl+b` as the prefix, `prefix "` for a top/bottom split, and `prefix %` for a side-by-side split. With this config, replace those with `Ctrl+a`, `prefix -`, and `prefix |`. Everything else in other docs still applies.
{{< /callout >}}

## Load it and check it works

{{% steps %}}

### Start tmux

```bash
tmux
```

A fresh tmux server reads `~/.tmux.conf` automatically. If a server was already running from before you saved the config, run `tmux kill-server` first, then `tmux` again.

### Look at the status bar

You should see a **black bar** at the bottom with ` 1:zsh ` (or `1:bash`) in reverse colors on the left, and the date and time on the right. Window **1**, not 0, means the config loaded.

### Test the prefix

Press `Ctrl+a`, let go, then press `|`. The screen should split side by side. Press `Ctrl+a` then `-` and the right-hand pane splits top and bottom.

### Test reload

Press `prefix r`. You should briefly see **reloaded** in the status bar. From now on, whenever you edit the config, `prefix r` applies the change.

### Clean up

Type `exit` in each pane (or press `Ctrl+d`) until tmux closes.

{{% /steps %}}

{{< callout type="warning" >}}
**Reload only works for this file.** The `r` binding hard-codes `~/.tmux.conf`. If you keep your config somewhere else (for example `~/.config/tmux/tmux.conf`), change that path in the `bind r` line.
{{< /callout >}}

## Practice

{{% steps %}}

### Start, split, reload, exit

From a plain shell: start `tmux`, make one `|` split and one `-` split, press `prefix r`, and confirm you see "reloaded". Then exit every pane.

### Feel the double-tap

In any tmux pane, type `echo hello`, then press `Ctrl+a Ctrl+a`. The cursor should jump to the start of the line. That's `send-prefix` passing `Ctrl+a` through to the shell.

{{% /steps %}}
