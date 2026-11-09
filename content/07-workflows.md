---
title: "Workflows"
weight: 7
---

You know the pieces. These scenarios put them together the way you'll use tmux day to day. Each one is a short routine. Run through them a few times until they feel normal.

## Scenario 1: Morning startup

**Goal:** three projects, each in its own session, set up in under a minute.

```bash
tmux new -d -s api   -c ~/code/api
tmux new -d -s web   -c ~/code/web
tmux new -d -s notes -c ~/notes
tmux a -t api
```

Then in each session (`prefix s` to move between them):

1. `prefix ,` → `edit`
2. `prefix c`, `prefix ,` → `run`
3. `prefix c`, `prefix ,` → `git`
4. `prefix 1` to go back to the editor

{{< callout type="info" >}}
**Coming back tomorrow?** If you didn't reboot, your sessions are still running. `tmux ls` and `tmux a -t api` and you're straight back in. tmux sessions don't survive a reboot, so after one you rebuild them; that's what this routine is for.
{{< /callout >}}

## Scenario 2: Editor + server + logs

**Goal:** a window with a big editor pane, a dev server, and a log tail all visible at once.

```text
┌──────────────────┬──────────┐
│                  │  server  │
│      editor      ├──────────┤
│                  │   logs   │
└──────────────────┴──────────┘
```

{{% steps %}}

### Split side by side

In your `edit` window: `prefix |`.

### Split the right side

The new pane is on the right and active. `prefix -`.

### Fill them

- Top right: start your server (`npm run dev`, `python -m http.server`, …).
- Bottom right: `tail -f some.log`.
- `prefix ←` to the left pane and open your editor.

### Make the editor wider

Drag the vertical border right, or press `prefix Alt+→` a few times.

### Focus

When you need the whole screen for the editor, press `prefix z`. Press `prefix z` again to check on the server.

{{% /steps %}}

## Scenario 3: The SSH session that survives

**Goal:** a long job on a remote machine that keeps running if your Wi-Fi drops or your laptop sleeps.

```bash
ssh myserver
tmux new -A -s job      # attach if 'job' exists, otherwise create it
./long-running-thing.sh
# prefix d, then close your laptop
```

Later:

```bash
ssh myserver
tmux new -A -s job      # same command: you land right back in it
```

{{< callout type="warning" >}}
**Nested tmux.** If you run tmux locally *and* on the server, `Ctrl+a` goes to the **outer** (local) tmux. Press **`Ctrl+a Ctrl+a`** to send the prefix to the inner (remote) tmux, e.g. `Ctrl+a Ctrl+a d` detaches the remote session. That's the `bind C-a send-prefix` line in your config at work. (The remote server needs the same prefix for this to work; if it uses the default, press `Ctrl+b` for the remote instead.)
{{< /callout >}}

## Scenario 4: Find it in the scrollback and copy it

**Goal:** a command printed an error 300 lines ago and you need the exact message.

1. `prefix v`
2. `?` `error` `Enter`, and `n` to go further back if needed
3. Move to the start of the message (`0`, `w`), press `Space`, move to the end (`$`), press `Enter`
4. Go to another pane (`prefix →`) or window (`prefix l`) and press `prefix ]` to paste

## Scenario 5: Context switch and back

**Goal:** someone asks a quick question about project `web` while you're deep in `api`.

1. `prefix s` → `web`. Check the thing.
2. `prefix L`. You're back in `api`, on the same window and pane you left.

Two keystrokes there, two keystrokes back. This is the habit that makes tmux feel like a superpower.

## End of day

You don't need to do anything. Close the terminal. Tomorrow, `tmux ls` shows your sessions are all still there (unless the machine rebooted).

To start fresh:

```bash
tmux kill-session -t notes   # one session
tmux kill-server             # everything
```
