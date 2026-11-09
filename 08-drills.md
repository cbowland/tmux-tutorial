---
title: "8. Drills"
weight: 8
---

Muscle memory comes from repetition, not from reading. These drills are short, timed rounds. Do **one session a day for a week**, about 10 minutes each.

## Rules

- **Hands on the keyboard.** No mouse during drills. The mouse is great day to day, but here you're training your fingers.
- **Don't look things up mid-round.** If you blank on a key, finish the round however you can, then check the [cheat sheet](../cheatsheet/) afterwards.
- **Time yourself.** Use your phone's stopwatch. Write the times down and watch them fall.
- **Clean up first.** Start every drill from a plain shell with no tmux running: `tmux kill-server`.

## Round 1: Windows

**Target: under 30 seconds.**

{{% steps %}}

### Set up

`tmux new -s d1`

### Do this

1. Rename window 1 to `a`.
2. Create windows `b`, `c`, `d` (create and rename each one).
3. Jump: 3 → 1 → 4 → 2 → 1.
4. Toggle between the last two windows 3 times.
5. Kill window `c`.
6. Detach.

{{% /steps %}}

{{< callout type="info" >}}
**Keys used:** `prefix ,` `prefix c` `prefix 1-4` `prefix l` `prefix &` `prefix d`
{{< /callout >}}

## Round 2: Panes

**Target: under 30 seconds.**

{{% steps %}}

### Set up

`tmux new -s d2`

### Do this

1. Split side by side.
2. Split the right pane top and bottom.
3. Move: left → top right → bottom right → left.
4. Zoom the left pane, run `pwd`, unzoom.
5. Jump to pane 3 using pane numbers.
6. Break pane 3 out into its own window.
7. Go back to window 1 and kill panes until one is left.

{{% /steps %}}

{{< callout type="info" >}}
**Keys used:** `prefix |` `prefix -` `prefix ←↑→↓` `prefix z` `prefix q 3` `prefix !` `prefix 1` `prefix x`
{{< /callout >}}

## Round 3: Sessions

**Target: under 45 seconds.**

{{% steps %}}

### Set up

```bash
tmux new -d -s red
tmux new -d -s green
tmux new -d -s blue
tmux a -t red
```

### Do this

1. Switch to `blue` with the session picker.
2. Toggle back to `red` with last-session.
3. Cycle forward through all sessions back to `red`.
4. Create a session `yellow` from inside tmux.
5. Toggle to `red` and back to `yellow`.
6. Rename `yellow` to `gold`.
7. Kill `green` from the picker.
8. Detach, list sessions, and reattach to `blue` by name.

{{% /steps %}}

{{< callout type="info" >}}
**Keys used:** `prefix s` `prefix L` `prefix )` `prefix :` + `new -s yellow` `prefix $` `prefix s` + `x` `prefix d` `tmux ls` `tmux a -t blue`
{{< /callout >}}

## Round 4: Copy mode

**Target: under 30 seconds.**

{{% steps %}}

### Set up

```bash
tmux new -s d4
seq 1 1000
```

### Do this

1. Enter copy mode and go to the very top, then the very bottom.
2. Search up for `777`.
3. Select that whole line and copy it.
4. Leave copy mode, type `echo `, and paste.

{{% /steps %}}

{{< callout type="info" >}}
**Keys used:** `prefix v` `g` `G` `?777` `V` `Enter` `prefix ]`
{{< /callout >}}

## Round 5: Everything

**Target: under 90 seconds.** Do this one once you're comfortable with rounds 1–4.

{{% steps %}}

### Set up

From a plain shell, nothing running.

### Do this

1. Create detached sessions `api` (in `~`) and `web` (in `/tmp`). Attach to `api`.
2. In `api`: windows `edit`, `run`, `git`. In `edit`, split side by side and split the right side top and bottom.
3. Switch to `web`. Name window 1 `edit` and create window `dev`.
4. Toggle back to `api`. You should land in `edit`, with the three-pane layout intact.
5. Zoom the left pane, unzoom.
6. Toggle to `web`, then go to window 1.
7. Detach. `tmux ls`. Reattach to `api`.
8. `tmux kill-server` from inside tmux. Everything closes.

{{% /steps %}}

## Weekly plan

| Day | Do |
|---|---|
| 1 | Rounds 1 and 2, three times each |
| 2 | Rounds 2 and 3, three times each |
| 3 | Round 3 ×3, round 4 ×2 |
| 4 | Rounds 1–4 once each, timed |
| 5 | Round 5 ×3 |
| 6 | Round 5 ×3, try to beat 60 seconds |
| 7 | No drills. Just use tmux for all your real work today. |

{{< callout type="info" >}}
**You're done when** you've stopped thinking about the keys and only think about *where* you want to be.
{{< /callout >}}
