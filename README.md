# Asteroids / Written Weights

A playable experiment in encoding an Asteroids-style game as a **hand-constructed numerical graph**, loaded by a separate player.

In the latest Linux S4 version, the graph produces gameplay, score digits, labels and line geometry. It also maps raw key inputs, initializes from zero state and handles reset. The host supplies numerical evaluation, state storage, timing, keyboard input, window management and line drawing.

This is a deterministic affine/ReLU circuit, not a trained AI model. Both the graph connections and its weights/biases encode behavior. A generic runtime is still required.

## Download and play

- **[Linux x86-64: S4 player](https://github.com/Lord-Tim/asteroids-written-weights/releases/download/linux-s4/Asteroids-Linux-x86_64-S4.tar.gz)** (6.7 MiB, silent). [Release notes and checksums](https://github.com/Lord-Tim/asteroids-written-weights/releases/tag/linux-s4).
- **[Windows x64: W1 player](https://github.com/Lord-Tim/asteroids-written-weights/releases/download/windows-w1/Asteroids-Windows-Player-W1.zip)** (13.1 MiB, earlier version). [Windows release notes](https://github.com/Lord-Tim/asteroids-written-weights/releases/tag/windows-w1).
- **[S4 source, model compiler and tests](https://github.com/Lord-Tim/asteroids-written-weights/releases/download/linux-s4/Asteroids-S4-Source.zip)** (2.0 MiB, optional). Not needed to play.

Download the named player asset for your operating system. GitHub's automatic **Source code** ZIP/tar.gz files are not the ready-to-run player.

### Linux S4

1. Extract the entire archive and keep its files together.
2. Open a terminal in the extracted folder and run `./Start-Player`.
3. Click **Load model JSON...**, choose `app/model/Asteroids-S4.model.json`, then **Start**.

You can also launch directly:

```sh
./Start-Player app/model/Asteroids-S4.model.json
```

Requires **Linux x86-64, glibc 2.38+ and X11/XWayland**, with the usual X11/Xft/Xss/fontconfig graphics libraries. Python and Tcl/Tk are bundled. No account, browser, system Python installation or internet connection is required to play. **There is no sound in S4.** Native Wayland, Windows, macOS and ARM are not supported by this Linux package. The project owner has tested this S4 build on Omarchy and reported that it plays well; this is not a compatibility guarantee for every Linux system.

See [full Linux requirements and instructions](LINUX-S4.md). If extraction lost the executable bit, run `chmod +x Start-Player`.

### Windows W1

1. Right-click the ZIP and choose **Extract All**.
2. Open `ModelPlayer-W1.exe`.
3. Click **Load model JSON...**, choose `model/Asteroids-R2.model.json`, then **Start**.

Keep the executable, `_internal/` and `model/` together. Python is bundled. The executable is unsigned; do not disable security protections to run it. Sound starts off. W1 is the earlier Windows version, not a Windows port of S4. Its existing release is unchanged. See [Windows instructions and verification limits](WINDOWS-W1.md).

## Controls

- Turn: **Left / Right** or **A / D**
- Thrust: **Up** or **W**
- Fire: **Space** or **X**
- Hyperspace: **H** or **Shift**
- Reset: **Enter** or **R**

Leaving or minimizing the window pauses play and clears held keys. Click **Resume** to continue.

## Inspect the model

The player and model are separate. Load only trusted model files.

In S4, enable **Show model inspection and ablation controls** to try changes in memory:

- Zero all weights and biases: gameplay and labels disappear.
- Disconnect raw key slot **32**: Space loses its influence, while X can still fire through its separate input.
- Restore **Normal**, then **Apply and restart**, to play again.

These experiments do not change the saved JSON. **Unload** returns to the empty player.

The optional S4 source archive includes the player source, native evaluator, preserved input graph, model compiler, final model and repeatable tests. Its compiler regenerates the shipped model byte-for-byte. It does not include a complete reproducible build recipe for the bundled third-party Python/Tk runtime.

## Verification and limits

Before publication, S4 passed 3,601 original-reference frames, bit-exact original gameplay state and geometry checks (with the intentional HUD offset), raw-key mapping, reset, zeroing, malformed-input checks, model regeneration and player-archive checksums. See [verification scope](S4-VERIFICATION.md).

These are bounded checks, not exhaustive game fidelity or a broad operating-system certification. S4 is silent. The applications are designed to make no network requests; they are not operating-system-enforced network sandboxes.

## Verify downloads

Download `SHA256SUMS.txt` from the same release. For Linux S4:

```sh
sha256sum Asteroids-Linux-x86_64-S4.tar.gz
```

Expected SHA-256:

```text
115be87c0dac5a9e40d5a1e8a3cf0fc85ac9112e026bea86613f2ad440e40550
```

## License notices

Bundled third-party components retain their respective licenses and notices. Preserve those notices when redistributing. No new project-wide or game/model license is granted by this repository. Public availability alone does not grant permission to reuse or redistribute every component.
