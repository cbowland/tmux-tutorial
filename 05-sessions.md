---
title: "5. Sessions"
weight: 5
---

This is the chapter that makes tmux pay off. The goal: **one session per project**, and switching between projects as quickly as switching windows.

```text
tmux server
├── session "api"     (1:edit 2:run 3:git)
├── session "web"     (1:edit 2:dev 3:test)
└── session "notes"   (1:notes)
```

When you switch to `api`, everything is exactly how you left it: same windows, same panes, same directories, same scrollback. That's what makes tmux worth the effort.

## Creating sessions

### From outside tmux

```bash
tmux new -s api                 # create and attach
tmux new -s web -c ~/code/web   # create, starting in that directory
tmux new -d -s notes            # create in the background (-d = detached)
```

### From inside tmux

Running `tmux new -s foo` **inside** tmux fails with *"sessions should be nested with care"*. Instead, create the session in the background and switch to it:

```bash
tmux new -d -s web -c ~/code/web    # create it detached
tmux switch-client -t web           # jump to it
```

Or use the tmux command prompt:

1. `prefix :` opens a prompt in the status bar.
2. Type `new -s web` and press `Enter`.

From the command prompt, tmux creates the session and switches you into it.

### "Attach if it exists, otherwise create"

```bash
tmux new -A -s api
```

This is the one command to remember. It's safe to run whether or not `api` already exists.

## Switching sessions

This is where muscle memory matters most.

| Key | Action |
|---|---|
| `prefix s` | **s**ession picker: a list of sessions with live previews |
| `prefix (` / `prefix )` | previous / next session |
| `prefix L` | **l**ast session: toggle between the two most recent |
| `prefix w` | tree of every session *and* window (jump straight to a window) |

### `prefix L` is the session version of `prefix l`

- `prefix l` (lowercase) toggles between the last two **windows**.
- `prefix L` (uppercase, `Shift+l`) toggles between the last two **sessions**.

Learn them together. They cover about 80% of moving around.

### Using the session picker

`prefix s` shows something like:

```text
(1)  + api: 3 windows
(2)  + notes: 1 windows
(3)  + web: 3 windows (attached)
```

- `↑` / `↓` or `j` / `k` to move, `Enter` to switch
- Press the **number or letter in parentheses** to jump straight to that session
- `→` expands a session to show its windows
- `x` kills the highlighted session (asks first)
- `q` / `Esc` cancels

## Renaming, detaching, killing

| Do this | How |
|---|---|
| Rename the current session | `prefix $` |
| Detach (leave everything running) | `prefix d` |
| List sessions from a shell | `tmux ls` |
| Attach to one | `tmux a -t api` |
| Kill one from a shell | `tmux kill-session -t api` |
| Kill one from the picker | `prefix s`, highlight it, `x`, `y` |

{{< callout type="info" >}}
Killing the session you're **in** detaches you back to your plain shell, even if other sessions are still running. To avoid that, switch away first (`prefix L`), then kill the old session from the picker.
{{< /callout >}}

## Naming conventions that help

- **Short and lowercase:** `api`, `web`, `infra`, `notes`. You'll type them in `tmux a -t …`.
- **Use the same names every day** so your fingers learn `tmux a -t api`.
- **Name windows the same way in every project** (`edit`, `run`, `git`). Then `prefix 1` always means the editor, no matter which session you're in.

## Practice

This is the most important practice block in the tutorial. Do it twice.

{{% steps %}}

### Create three sessions from outside tmux

From a plain shell (not inside tmux):

```bash
tmux new -d -s api   -c ~
tmux new -d -s web   -c /tmp
tmux new -d -s notes
tmux ls
```

You should see three sessions listed.

### Attach to one and give it windows

`tmux a -t api`. Rename window 1 to `edit`, then create `run` and `git` (`prefix c`, `prefix ,`).

### Switch with the picker

`prefix s` → choose `web` → `Enter`. Rename its window 1 to `edit` and create a `dev` window.

### Toggle sessions

Press `prefix L` four times. You should bounce between `api` and `web`. Watch your terminal title change.

### Cycle all of them

Press `prefix )` three times and `prefix (` three times. You should cycle through `api` → `notes` → `web` in alphabetical order.

### Create one from inside tmux

`prefix :` then `new -s scratch`, `Enter`. You're now in `scratch`. Press `prefix L` to go back where you were.

### Rename and kill

Switch to `scratch` (`prefix L`), press `prefix $`, and rename it to `tmp`. Then `prefix L` again to leave it, and `prefix s`, highlight `tmp`, `x`, `y`. Killing it from *another* session keeps you attached.

### Detach and come back

`prefix d`. In your shell: `tmux ls`, then `tmux a -t web`. Your windows are still there.

### Clean up

```bash
tmux kill-server
```

{{% /steps %}}
