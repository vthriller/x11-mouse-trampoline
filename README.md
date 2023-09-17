# X11 mouse trampoline

Quick and dirty alternative to [mouse jump feature from Microsoft PowerToys](https://learn.microsoft.com/en-us/windows/powertoys/mouse-utilities#mouse-jump).

## Usage

```sh
pipe=${XDG_RUNTIME_DIR:-$HOME/.local}/mouse-trampoline.pipe
# or wherever you want to put this file

# start the daemon
mouse-trampoline $pipe

# show the window
echo > $pipe
```

## Dependencies

- Tkinter
- Pillow
- python-xlib

## Limitations

Should run as daemon for quicker response times. If you're a suckless.org fanatic and rather concerned about saving as much free PIDs as possible, `git checkout v1.0`.

This uses 3 (yes, three) connections to X server: one for Tk, one for python-xlib (to get/set cursor position), one for Pillow to take screenshot of the screen. Theoretically it's possible to reduce this number to 2 without complete rewrite, but `blt::winop query` yields `X Error of failed request:  BadWindow (invalid Window parameter)` for some reason.

Not tested with multiple monitors.

Good luck writing similar thing for bazillion of Wayland compositors.
