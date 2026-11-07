# S4 verification

Release check: 7 November 2026, Linux x86-64.

Runtime model SHA-256:
`63138be7073495c3346509260c5bdd1d8fad7d4aaf5e43ba1e0d1ce0dc4fb176`

## Repeatable checks

The included `tests/verify.py` passed again before this publication:

- 3,601 frames checked against original R2 reference digests and S3 gameplay. All 373 original recurrent-state values are bit-exact. Gameplay line geometry matches after the intended float32 +8 vertical translation for the HUD.
- Graph-generated HUD digit activations agree with independently formatted meter values across the same frames.
- 26 raw-key alias and multiple-alias OR checks passed.
- Three held-reset frames restore the fresh model state and frame exactly.
- 361 raw-Space disconnection frames match a normal model with Space absent.
- 120 frames with zeroed weights and biases produce all-zero state and line output, including labels.
- Seven malformed graph/key-vector cases are rejected before native evaluation.
- The included model compiler regenerated the shipped JSON byte-for-byte.
- Every file in the unchanged player archive passed its included SHA-256 manifest.

## Interactive checks and limits

The player was previously exercised in an X11 Linux desktop, including model loading, play, scoring, reset, pause and zero-weight ablation. The same S4 player was subsequently reported to play well on Omarchy by the project owner.

The publication check above was headless; it did not repeat interactive testing. These checks are not exhaustive game-fidelity tests or a broad Linux compatibility guarantee. The prebuilt player requires x86-64, glibc 2.38 or newer, and X11/XWayland. Native Wayland, Windows, macOS and ARM are not supported by this Linux package. Sound is deliberately absent.

The graph is a constructed deterministic numerical circuit, not a learned policy. It requires graph structure and coefficients plus the generic runtime.
