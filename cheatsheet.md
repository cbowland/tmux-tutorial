---
title: "Cheat Sheet"
weight: 9
---

`prefix` = press and release **`Ctrl+a`**, then the key. Keys marked ★ come from your config; everything else is a tmux default.

## Sessions

| Key / command | Action |
|---|---|
| `tmux new -s NAME` | new session |
| `tmux new -A -s NAME` | attach if it exists, otherwise create |
| `tmux new -d -s NAME -c DIR` | create in the background, starting in DIR |
| `tmux ls` | list sessions |
| `tmux a -t NAME` | attach |
| `tmux kill-session -t NAME` | kill one session |
| `tmux kill-server` | kill everything |
| `prefix s` | session picker |
| `prefix L` | last session (toggle) |
| `prefix (` / `prefix )` | previous / next session |
| `prefix $` | rename session |
| `prefix d` | detach |
| `prefix :` → `new -s NAME` | new session from inside tmux |

## Windows

| Key | Action |
|---|---|
| `prefix c` | new window |
| `prefix ,` | rename window |
| `prefix 1` … `9` | go to window N ★ (numbered from 1) |
| `prefix n` / `prefix p` | next / previous window |
| `prefix l` | last window (toggle) |
| `prefix w` | tree of all sessions and windows |
| `prefix f` | find a window by text |
| `prefix .` | move window to a new number |
| `prefix &` | kill window |

## Panes

| Key | Action |
|---|---|
| `prefix \|` | split side by side ★ (same directory) |
| `prefix -` | split top / bottom ★ (same directory) |
| `prefix ←↑→↓` | move to pane (repeatable) |
| `prefix o` | next pane |
| `prefix q` then `N` | jump to pane N ★ (numbered from 1) |
| `prefix z` | zoom / unzoom |
| `prefix Ctrl+arrow` | resize by 1 (repeatable) |
| `prefix Alt+arrow` | resize by 5 (repeatable) |
| `prefix Space` | cycle layouts |
| `prefix {` / `prefix }` | swap with previous / next pane |
| `prefix !` | break pane out into a new window |
| `prefix x` | kill pane |
| mouse | click to focus, drag a border to resize ★ |

## Copy mode (vi)

| Key | Action |
|---|---|
| `prefix v` | enter copy mode ★ (also `prefix [`, or scroll the mouse wheel) |
| `h j k l` `w b e` `0 $` | move |
| `Ctrl+u` / `Ctrl+d` | half page up / down |
| `g` / `G` | top / bottom of history |
| `?` / `/` | search up / down |
| `n` / `N` | next / previous match |
| `Space` | start selection |
| `V` | select line |
| `v` | toggle rectangle selection |
| `Enter` | copy and leave |
| `Esc` | clear selection |
| `q` | leave copy mode |
| `prefix ]` | paste |

## Misc

| Key | Action |
|---|---|
| `prefix r` | reload `~/.tmux.conf` ★ |
| `prefix Ctrl+a` | send a literal `Ctrl+a` (start of line, or the prefix to a nested tmux) ★ |
| `prefix :` | tmux command prompt |
| `prefix ?` | list all key bindings |
| `prefix /` then a key | describe one key |

## If you read other tmux docs

| Default tmux | Your config |
|---|---|
| `Ctrl+b` | `Ctrl+a` |
| `prefix %` | `prefix \|` |
| `prefix "` | `prefix -` |
| window 0 | window 1 |
