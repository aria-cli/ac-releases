---
license: other
license_name: openrail-m
---

# live-voice-m1/coreml — voice M1

One voice for live voice conversion (RVC v2, 48 kHz, HiFi-GAN NSF), as Core ML for macOS 15 / iOS 18.

| file | what |
|---|---|
| `m1.mlmodelc` | The generator. Two functions sharing weights: `b50` (50 ms blocks; P 61, 11 frames → 5280 samples) and `b100` (100 ms; P 66, 17 frames → 8160 samples). Inputs `phone` f32 [1, P, 768], `pitch` i32 [1, P] (1…255), `nsff0` f32 [1, P] Hz, `z_noise` f32 [1, 192, P], `nsf_noise` f32 [1, frames·480, 1]; output `audio` f32 [1, 1, frames·480] at 48 kHz, clipped to ±1. f16, with the NSF sine source in f32. |
| `m1.index.f16` | Retrieval features: raw little-endian f16 [N, 768] |
| `m1.index.json` | `{N, dim, dtype, index_rate, target_median_f0_hz}` |

Measured on the GPU against PyTorch with the same noise: 47.6 dB (b50) / 48.1 dB (b100) SNR.
The whole converter differs from PyTorch by 0.07–0.68 dB of log-mel. PyTorch differs from itself
by 1.6–2.2 dB under another noise seed.

## Use restrictions

M1 was trained on speech rendered by **Supertonic-3** (catalog voice M1), licensed under
**OpenRAIL-M**. This voice carries the same use restrictions (its Attachment A), including:
**do not use it to impersonate any person without their consent**, and do not use it to deceive
anyone about who is speaking.

The generator was fine-tuned from the RVC v2 48 kHz pretrained base, itself trained on VCTK
(CC-BY 4.0; Yamagishi, Veaux, MacDonald — The Centre for Speech Technology Research, University
of Edinburgh).
