---
title: "Windows"
weight: 3
---

Windows are the tabs inside a session. A common setup is one window per task: editor, server, git, logs.

Start a session to follow along:

```bash
tmux new -s win
```

## Create, name, switch

| Key | Action |
|---|---|
| `prefix c` | **c**reate a new window |
| `prefix ,` | rename the current window |
| `prefix 1` … `prefix 9` | jump straight to window N |
| `prefix n` / `prefix p` | **n**ext / **p**revious window |
| `prefix l` | **l**ast window (toggle between the two most recent) |
| `prefix w` | pick a window from a list (all sessions) |
| `prefix &` | kill the current window (asks y/n) |

{{< callout type="info" >}}
**Why numbering from 1 matters.** The config sets `base-index 1`, so window 1 is `prefix 1`, the key at the far left of the number row. With the default (starting at 0), your first window would be on the `0` key, which is far away and out of order.
{{< /callout >}}

### Name every window

Names show up in the status bar (` 1:editor  2:server `) and in your terminal title. Named windows are much easier to find later.

`prefix ,` opens a prompt with the current name already filled in. Delete it, type a new one, and press `Enter`.

{{< callout type="info" >}}
tmux names windows after the running program (`zsh`, `vim`, `top`) until you rename them. Once you rename a window, the name stays.
{{< /callout >}}

## `prefix l`: the toggle you'll use most

Most of the time you're going back and forth between two windows, say the editor and a shell. `prefix l` flips between whichever two you used most recently, so you don't need to remember their numbers.

## The window picker

`prefix w` opens a tree of every session and window, with live previews:

- `↑` / `↓` (or `j` / `k`) to move
- `→` / `←` to expand or collapse a session
- `Enter` to jump there
- `q` or `Esc` to cancel

This is your fallback when you can't remember where something is.

## Gaps in numbering

If you close window 2 out of 1, 2, 3, you're left with **1 and 3**. That's normal. Windows keep their numbers. To renumber, use `prefix .` and type a new number to move the current window, or close and reopen windows.

{{< callout type="info" >}}
If you'd like tmux to close the gaps automatically, add `set -g renumber-windows on` to your config and press `prefix r`. It's optional; this tutorial doesn't assume it.
{{< /callout >}}

## Find a window by content

`prefix f` asks for text and lists the windows whose name, title, or visible content matches it. This is useful once you have a lot of windows.

## Practice

{{% steps %}}

### Build a three-window session

In session `win`:

- Rename window 1 to `edit` (`prefix ,`).
- Create window 2 (`prefix c`) and rename it `run`.
- Create window 3 and rename it `git`.

Your status bar should read ` 1:edit  2:run  3:git `.

### Jump by number

Without looking at the keyboard: `prefix 1`, `prefix 3`, `prefix 2`, `prefix 1`.

### Toggle

Go to `edit`, then `run`. Now press `prefix l` five times. You should bounce between `edit` and `run`.

### Use the picker

`prefix w`, move to `git`, and press `Enter`.

### Kill and observe the gap

On `run`, press `prefix &` then `y`. The status bar now shows ` 1:edit  3:git `. Create a new window with `prefix c`. Which number did it get?

{{% /steps %}}

{{< callout type="info" >}}
**Answer:** the new window takes the lowest free number, **2**.
{{< /callout >}}

Keep the `win` session for the next chapter.
