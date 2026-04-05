## rofi-rec

Minimal rofi-based screen recorder using ffmpeg with support for microphone and system audio.

### Features

* fullscreen recording
* window recording
* area recording
* microphone recording
* system audio capture
* mic + output mixing
* rofi menu control
* direct stop from CLI
* dwmblocks recording indicator
* automatic state cleanup on unexpected recorder exit

---

### Audio

Works with:

* PipeWire via `wpctl`
* PulseAudio via `pactl`
* hybrid setups

I recommend `pactl` because it usually provides more reliable default device detection.

---

### Volume control

* `OUTPUT_VOLUME` - system audio level in the recording
* `MIC_VOLUME` - microphone gain

---

### Rofi theme

The script uses a custom theme:

```bash
~/.config/rofi/rofi-rec.rasi
```

##### Important:
`install-theme.sh` may override your existing rofi config, files like `font.rasi` and `colors.rasi` are examples and may conflict with your setup, using your own theme is recommended.

---

### Keybindings

Menu navigation (vim-like):

```css
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

```bash
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

```bash
git clone https://github.com/Luvrok/rofi-rec
cd rofi-rec
chmod +x ./install-theme.sh rec
./install-theme.sh
sudo mv rec /usr/bin
```

---

### Usage

##### Run menu:
```bash
rec
```
##### Stop active recording directly:
```bash
rec stop
```
##### Available targets:
* fullscreen
* window - requires `xwininfo`
* area - requires `slop`

---

### Notes

* output files are saved to `~/HOME/screen_recordings` (yes i use HOME inside HOME)
* default preset is `ultrafast`
* uses a PID file to track active recording
* recording state is cleaned automatically if ffmpeg exits on its own
* window recording stops automatically if the selected window disappears
* x11 only

---

### Requirements

Required:

* ffmpeg
* rofi
* xdpyinfo
* notify-send
* pactl or wpctl

Optional:

* slop - required for area selection
* xwininfo - required for window selection
* dwmblocks or dwmblocks-async
