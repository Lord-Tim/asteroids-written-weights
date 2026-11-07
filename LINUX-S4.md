# Asteroids S4: silent model circuit

A minimal Linux player with a separate game-model JSON. This is a new version;
S3 and earlier releases are unchanged. No browser, account, server, installer,
sound device or download is needed during play.

## Play

1. Extract the whole archive and keep its contents together.
2. Run `./Start-Player`.
3. Click **Load model JSON...**, choose `app/model/Asteroids-S4.model.json`,
   then **Start**.

Or open the model directly:

    ./Start-Player app/model/Asteroids-S4.model.json

Left/Right or A/D turn; Up or W thrusts; Space or X fires; H or either Shift
activates hyperspace; R, Enter or keypad Enter resets. Use Pause/Resume in the
window. Leaving the app or minimizing pauses and clears held keys. Click the
canvas to return keyboard focus after using other controls.

## What changed

Score digits, labels, status messages and control hints now come from the graph
as line geometry. The graph maps raw key bits to actions and initializes itself
from zero state. Reset is also handled in the graph. Sound has been removed.

The host has no gameplay engine, font renderer for game labels, key-to-action
mapping or game-specific startup vector. It supplies generic numerical
inference, state storage, timing, raw keyboard input, window management and line
drawing. This is a constructed deterministic circuit, not a trained model or
literally “weights only”: graph connections and coefficients both matter.

**Show model inspection and ablation controls** allows in-memory experiments.
Zero weights and biases removes the game and its labels. Disconnect raw key
slot **32** removes Space's influence; X still fires through its separate input.
Restore **Normal**, then **Apply and restart**, to play again. No test edits the
model file. **Unload** returns to the empty generic player.

The displayed score saturates at 9,999,999; lives/rocks/shots at 99; wave at 9,999;
saucer at 9. Gameplay values are unchanged. The keyboard ABI supports Latin-1 and
X11 special keysyms, including all listed bindings, not arbitrary Unicode keys.

## Requirements

Linux x86-64 with glibc 2.38 or newer and an X11 or XWayland desktop. The usual
system graphics/font libraries are required: X11, Xft, Xss, fontconfig and their
dependencies (FreeType, Xrender, xcb, Xext, png, bz2, brotli, Xau and Xdmcp).
Python 3.13.5, required Python modules, Tcl/Tk 8.6, libffi, zlib and expat are
bundled. No system Python installation or ALSA/audio device is required. This is
not a universal Linux binary. Native Wayland, Windows, macOS and ARM are not
supported by this package.

If the file manager does not open executables, run the terminal command above.
If extraction lost its executable bit, run `chmod +x Start-Player`. The app
installs nothing and does not save scores or Python caches.

## Verification

3,601 original-reference frames passed: original gameplay state is bit-exact,
and gameplay geometry is bit-exact after the HUD's 8-unit vertical offset.
Raw-key mapping, digits, self-initialization/reset, zeroing and malformed-input
checks passed. The actual bundled native player was exercised on a Linux XFCE
cloud desktop, including play, scoring, reset, pause and zero-weight ablation.
This is not a Windows/Omarchy compatibility guarantee or exhaustive fidelity test.
Source, compiler and detailed tests are supplied separately, not required here.
`SHA256SUMS.txt` identifies every file in this runtime bundle.

## Licenses

Preserve `LICENSES/` and runtime copyright notices when redistributing. Python,
Tcl/Tk, libffi, expat and zlib notices and referenced GPL/LGPL texts are retained.
Those cover bundled/upstream runtime components, not the original game or model.
No new downstream game/model license is granted by this preview.
