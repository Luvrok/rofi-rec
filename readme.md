## rofi-rec

Minimal rofi-based screen recorder using ffmpeg with support for microphone and system audio.

### Features

* screen recording x11
* microphone recording
* system audio recording output
* mic + output mixing
* rofi menu control
* dwmblocks recording indicator

---

### Audio

Works with:

* PipeWire (wpctl)
* PulseAudio (pactl)
* hybrid setups

`pactl` is recommended because it provides more reliable detection of active(default) devices.

---

### Volume control

* `OUTPUT_VOLUME` - system audio level in the recording
* `MIC_VOLUME` - microphone gain

This allows independent control of what the viewer hears, regardless of your local volume.

---

### Rofi theme

The script uses a custom theme:

```
~/.config/rofi/rofi-rec.rasi
```

Important:

* `install-theme.sh` may override your existing rofi config
* files like `font.rasi` and `colors.rasi` are examples and may conflict with your setup
* it is recommended to use your own theme
* `rofi-rec.rasi` itself is minimal and safe to reuse, but check imports

---

### Keybindings

Menu navigation (vim-like):

```
kb-row-up: "Up,k";
kb-row-down: "Down,j";
kb-accept-entry: "Return,l";
kb-cancel: "Escape,q";
```

Can be changed in `rofi-rec.rasi`.

---

### dwmblocks integration

The script can update dwmblocks automatically.

Example block script:

```
#!/bin/sh

PIDFILE="/tmp/recpid"

if [ -f "$PIDFILE" ]; then
  pid="$(cat "$PIDFILE" 2>/dev/null)"
  if [ -n "$pid" ] && kill -0 "$pid" 2>/dev/null; then
    printf ' rec '
  fi
fi
```

---

### Installation

```
git clone https://github.com/Luvrok/rofi-rec
cd rofi-rec
chmod +x ./install-theme.sh rec
./install-theme.sh
sudo mv rec /usr/bin
rec
```

---

### Notes

* output files are saved to `~/HOME/screen_recordings`
* default preset is `ultrafast`
* uses PID file to track active recording

---

### Requirements

* ffmpeg
* rofi
* pactl or wpctl
* notify-send
* xdpyinfo
* (optional) dwmblocks or dwmblocks-async
