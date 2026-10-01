---
license: other
license_name: mit-and-apache-2.0
---

# live-voice-shared/coreml

The voice-independent half of live voice conversion, as Core ML for macOS 15 / iOS 18.

| file | what | precision | licence |
|---|---|---|---|
| `contentvec.mlmodelc` | ContentVec (HuBERT-base, layer 12, no final projection): `audio16k` f32 [1, 9760] or [1, 10560] → `features` f32 [1, ⌊(W − 400)/320⌋ + 1, 768] | f16 | MIT |
| `rmvpe.mlmodelc` | RMVPE pitch salience with its log-mel frontend inside (STFT magnitude, 128 htk mels 30–8000 Hz, log clamp 1e-5): `audio16k` f32 [1, 4960] → `salience` f32 [1, 32, 360] | f32 frontend, f16 network | Apache-2.0 |

Exported from Applio `c7665ac` (MIT) with coremltools 9.0. Measured on the GPU (CPU_AND_GPU)
against PyTorch: ContentVec 48.5 dB SNR, RMVPE salience 56.4 dB. The Neural Engine measured
19 dB on ContentVec, so the GPU is the intended compute unit.

Attribution: ContentVec — Qian et al. (MIT). RMVPE — Wei et al. (Apache-2.0). Applio / RVC (MIT).
