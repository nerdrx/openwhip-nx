# OpenWhip NX

![Whip divider](assets/divider.png)

Sometimes Claude Code is going too slow, and you must whip him into shape.

Fork of [GitFrog1111/OpenWhip](https://github.com/GitFrog1111/OpenWhip) that works on
**KDE Wayland** and targets the **Claude Code desktop app** (the upstream macro only
worked against the CLI on X11).

## What's different

- Keyboard injection goes through **ydotoold** (uinput) on Wayland sessions;
  `xdotool` is still used on X11.
- Sends **Esc** instead of Ctrl+C — Esc interrupts a running turn in both the
  Claude Code CLI and the desktop app, where Ctrl+C is just "copy".
- No injected Alt+Tab "refocus" on Wayland (tray clicks don't steal focus there,
  and it would switch away from the Claude window).

## Install

Grab the AppImage from [Releases](https://github.com/nerdrx/openwhip-nx/releases)
— or install it through [NX Hub](https://github.com/nerdrx/nx-hub).

On Wayland you also need the ydotool daemon (one-time setup, Arch-likes):

```bash
sudo pacman -S --needed ydotool
sudo cp ydotoold.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable --now ydotoold.service
```

The bundled [ydotoold.service](ydotoold.service) runs the daemon with a socket at
`/run/ydotoold.sock` owned by uid 1000 — adjust `--socket-own` if your uid differs.

## Run from source

```bash
npm install
npm start
```

## Controls

- Click tray icon: spawn whip.
- Click: drop whip.
- Whip him 😩💢
- It interrupts Claude (Esc) and types one of 5 encouraging messages!

## Credits

All the whip physics, art, and the original idea belong to
[GitFrog1111/OpenWhip](https://github.com/GitFrog1111/OpenWhip).
