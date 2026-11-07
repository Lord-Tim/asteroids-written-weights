# Asteroids / Written Weights

A downloadable Windows x64 player with an inspectable, separate game-model JSON file.

## Download and play

Open this repository's **Releases** section and download **Asteroids-Windows-Player-W1.zip** from the release assets. GitHub's automatically generated source archives are not the Windows game download.

1. Right-click the downloaded ZIP and choose **Extract All**. Keep all extracted files and folders together.
2. Open **ModelPlayer-W1.exe**.
3. Click **Load model JSON...**, select **model/Asteroids-R2.model.json**, and click **Start**.

Python, a browser, an account, and an internet connection are not required to play. The bundled runtime is in the `_internal` folder. This is a Windows x64 build, not a macOS or Linux application.

The executable is unsigned. If Windows or your security software blocks it, do not disable security protections. Only run files from a source you trust.

## Controls

- Turn: **Left / Right** or **A / D**
- Thrust: **Up** or **W**
- Fire: **Space** or **X**
- Hyperspace: **H** or **Shift**
- Reset: **Enter** or **R**

Sound starts off. Switching away from the window or minimizing it pauses play. Click **Resume** when you return.

## What's included

- `ModelPlayer-W1.exe`: the Windows player.
- `model/Asteroids-R2.model.json`: sparse game weights, interface metadata, and stored PCM audio.
- `_internal/`: the bundled Python/Tk runtime and native libraries.
- `licenses/`: the third-party license notices included with this build.
- `README.txt`: quick-start instructions.

Optional inspection controls can zero weights or disconnect an input in memory without changing the saved model file. Load only trusted model files.

This release packages the player and model for download. It is not a complete source-code distribution or a reproducible build kit.

## Model provenance

The model identifies `Asteroids-Written-Weights-R2.html` as its source. The game graph was copied unchanged during separation, and the constant audio graph was losslessly decoded to Float32 PCM. No model training was performed during that separation or the Windows port. Historical training provenance has not been independently established by the artifact.

## Testing and limitations

The executable, runtime, and model are unchanged from the Windows-tested W1 build. The cleaned ZIP passed an archive-integrity check in the cloud; the cleaned package was not retested in a Windows GUI. Physical audio output and behavior on other computers remain untested.

The application is designed to make no network requests. This is not an operating-system-enforced network sandbox.

## Verify the download

File: `Asteroids-Windows-Player-W1.zip`  
Size: **13,744,034 bytes**  
SHA-256:

```text
1dc174b8f4a5654aa1b44fabb8d959cb15770b643d4bb70796295b175d6d736c
```

In PowerShell, run:

```powershell
Get-FileHash .\Asteroids-Windows-Player-W1.zip -Algorithm SHA256
```

## License notices

The bundled third-party components retain their respective licenses and notices. No new project-wide license is granted by this repository. Public availability alone does not grant permission to reuse or redistribute every component.
