---
title: "Your First Session"
weight: 2
---

The single most important thing tmux does: **your shells keep running after you leave.** This chapter covers just that: start a session, leave it, and come back.

## The three layers

```text
tmux server
└── session  "work"          ← a workspace (usually one per project)
    ├── window 1 "editor"    ← like a browser tab
    │   ├── pane 1           ← a split inside a window
    │   └── pane 2
    └── window 2 "server"
        └── pane 1
```

- A **session** is a named collection of windows. You *attach* to it to see it and *detach* to leave it running in the background.
- A **window** fills the whole screen. Your status bar lists them as `1:zsh 2:vim …`.
- A **pane** is one shell. A window can be split into several.

## Start a named session

Always give sessions names. Names are what make switching between them fast later.

```bash
tmux new -s practice
```

The status bar shows window `1:zsh`. Your terminal's title bar shows `practice: zsh`. That's the `set-titles-string "#S: #W"` line in the config.

## Detach

Press **`prefix d`**.

You're back in your normal shell, and tmux printed `[detached (from session practice)]`. The session is **still running**. Prove it:

```bash
tmux ls
```

```text
practice: 1 windows (created Sun Nov  8 10:00:00 2026)
```

## Reattach

```bash
tmux attach -t practice    # short form: tmux a -t practice
```

Everything is exactly where you left it, including anything that was running.

{{< callout type="info" >}}
`tmux a` with no name reattaches to the most recently used session. That's handy when you only have one.
{{< /callout >}}

## Prove it survives

{{% steps %}}

### Start something long-running

Inside the `practice` session:

```bash
top
```

### Detach

`prefix d`

### Close the terminal entirely

Quit the terminal app. Yes, really.

### Open a new terminal and reattach

```bash
tmux a -t practice
```

`top` is still running. That's the core idea of tmux: the session lives on the tmux server, not in your terminal window.

{{% /steps %}}

## The prefix habit

Every tmux command starts with `Ctrl+a`. Two habits to build now:

1. **Press, then release.** `Ctrl+a`, let go, *then* the command key. You don't need to rush; tmux waits for the second key.
2. **Mistakes are cheap.** If you hit the prefix by accident, press `Esc` or any unbound key and nothing happens.

{{< callout type="info" >}}
**Lost?** `prefix ?` lists every key binding. Press `q` to close it. `prefix /` then a key tells you what that one key does.
{{< /callout >}}

## Ending a session

- Type `exit` in the last shell and the session ends.
- From outside: `tmux kill-session -t practice`.
- Nuclear option: `tmux kill-server` ends **all** sessions.

## Practice

{{% steps %}}

### Detach and reattach three times

`tmux new -s practice` → `prefix d` → `tmux ls` → `tmux a -t practice`. Repeat until you don't have to think about it.

### Run something and walk away

Start `ping 1.1.1.1` in the session, detach, wait 10 seconds, reattach. The ping counter kept going. Stop it with `Ctrl+c`.

### Clean up

`tmux kill-session -t practice`, then `tmux ls` should say `no server running`.

{{% /steps %}}
